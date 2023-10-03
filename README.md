import { Component, OnInit, Inject } from '@angular/core';
import { Angulartics2LaunchByAdobe, RequestBuilder, MeterData } from 'ui-commons';
import { map, catchError, finalize, tap } from 'rxjs/operators';
import { Observable, of, throwError } from 'rxjs';
import { ActivatedRoute, Router } from '@angular/router';
import { CLAIM_ID_ROUTE_PARAMETER } from '../shared/services/variables';
import { ModalService, ServerErrorModalComponent } from 'ui-commons';
import { ClaimDataService, Constants } from '../../../claims-ui-claims-inquiry-services-module/src/projects';
import { ClaimsCassErrorData, ClaimsInformationResponse } from '../shared/models/claimsInformationResponse';
import { ClaimInquirySummaryResponse, ServicesAndPaymentsSummary, ServicesAndPaymentsTab } from '../shared/models/models';
@Component({
  selector: 'claim-service-tab',
  templateUrl: './service-details-tab.component.html',
  styleUrls: ['./service-details-tab.component.scss']
})

export class ServiceTabComponent implements OnInit {

  serviceTabHeaderContent: {};
  claimsInquiry: Observable<ServicesAndPaymentsSummary>;
  claimSummary: Observable<ClaimInquirySummaryResponse>;
  servicesAndPaymentDetails: ServicesAndPaymentsTab;
  isLoading = false;
  serverError: string = null;
  copayData: ClaimsInformationResponse;
  coinsuranceData: ClaimsInformationResponse;
  deductibleData: ClaimsInformationResponse;
  outOfPocketData: ClaimsInformationResponse;
  cassError: ClaimsCassErrorData;
  // temporary default values
  defaultAmountLimit = 0;
  defaultAmountUsed = 0;
  noDataFound = false;

  showLegacyMessageBanner = false;

  showSystemErrorBanner = false;

  showNoDataBanner = false;

  constructor(@Inject('env') private env: any,
    private adobeAnalytics: Angulartics2LaunchByAdobe,
    private claimDataService: ClaimDataService,
    public requestBuilder: RequestBuilder,
    private router: Router,
    private route: ActivatedRoute,
    public modal: ModalService) { }

  ngOnInit(): void {
    this.adobeAnalytics.eventTrack('cl_click_service_tab');
    this.isLoading = true;
    this.serverError = null;
    const claimIdentifier = this.route.snapshot.parent.paramMap.get(CLAIM_ID_ROUTE_PARAMETER);

    this.claimsInquiry = this.claimDataService
      .dispatchClaimsInquiry('service-payment-details', 'servicePaymentDetails', { claimIdentifier })
      .pipe(map(({ data }) => data),
        tap(data => {
          this.servicesAndPaymentDetails = data;
          this.mappingResponse();
          this.serviceTabHeaderContent = {
            title: "Services & Payments",
            openNewTabLink: false,
            tags: [],
            badges: [{
              name: "View Premier Pricing",
              className: "badge",
              url: this.env.viewPremierPricing,
              analyticsEvent: 'cl_click_view_premier_pricing'
            },
            {
              name: "View Member Accums",
              className: "badge",
              url: this.getViewMemberAccumsLink(data?.cbdRouterIndicator),
              analyticsEvent: 'cl_click_view_member_accums'
            }],
            timeStamp: data.claimsInformationResponse[0].cassError?.timeStamp,
            referenceNumber: data.claimsInformationResponse[0].cassError?.referenceNumber
          }

          if (data?.cbdRouterIndicator === 'K') {
            this.checkSessionStorageData();
          }

          if (data.claimsInformationResponse[0].cassError?.systemError === true) {
            this.showSystemErrorBanner = true;
          }
          else if (data.claimsInformationResponse[0].cassError?.systemError === false) {
            this.showNoDataBanner = true;
          }
        }),
        catchError(error => {
          this.serverError = error.error;
          of(this.openServerErrorModal(error));
          return throwError(error);
        }),
        finalize(() => this.isLoading = false)
      );
  }

  checkSessionStorageData() {
    const clmId = sessionStorage.getItem('ACCUMS_INFO_CLM_ID');
    const queryData = {
      claimIdentifier: this.route.snapshot.parent.paramMap.get(CLAIM_ID_ROUTE_PARAMETER)
    };
    if (!clmId || clmId !== queryData?.claimIdentifier) {
      this.claimDataService
        .dispatchClaimsInquiry('claim-summary', 'claimSummary', queryData).pipe(
          map(({ data: { claimInquirySummaryResponse } }) => claimInquirySummaryResponse),
          catchError(error => of(this.openServerErrorModal(error))),
          finalize(() => this.isLoading = false)
        ).subscribe(data => {
          this.setAccumsSummaryDetailsInSession(data?.patient, queryData?.claimIdentifier);
        });
    }

  }

  setAccumsSummaryDetailsInSession(patientSummary, clmId) {
    const subId = patientSummary?.subscriberId;
    const grpId = patientSummary?.groupId;
    const setAccumsData = {
      corporateEntityCode: patientSummary?.corporateEntityCode.length === 3 ?
        patientSummary?.corporateEntityCode : patientSummary?.corporateEntityCode + '1',
      groupNumber: grpId?.substr(-6),
      memberPartyId: patientSummary?.memberId,
      policyEffectiveEndEpoch: patientSummary?.policyEffectiveEndDate,
      policyEffectiveStartEpoch: patientSummary?.policyEffectiveStartDate,
      searchType: Constants.MEMBER_PARTY,
      sectionNumber: patientSummary?.sectionNumber,
      singleResult: true,
      subscriberId: subId?.substr(-12),
      subscriberPartyId: patientSummary?.subscriberPartyId
    };
    const request = {
      memberPartyId: setAccumsData.memberPartyId?.toString(),
      subpartyId: ''
    };
    this.requestBuilder.store(Constants.MEMBER_PARTY_FORM_KEY, request);
    this.requestBuilder.store(Constants.MEMBER_HISTORY_SEARCH_PARAMS, setAccumsData);
    sessionStorage.setItem('SELECTED_GROUPNUMBER', setAccumsData?.groupNumber);
    sessionStorage.setItem('ACCUMS_INFO_CLM_ID', clmId);
    this.requestBuilder.store('SELECTED_MEMBER_PARTY_ID', parseInt(setAccumsData?.memberPartyId, 10));
    this.requestBuilder.store('SELECTED_POLICY_EFFECTIVE_DATE', setAccumsData?.policyEffectiveStartEpoch);

  }

  getViewMemberAccumsLink(cbdRouterIndicator) {
    let viewAccumsUrl = '';
    switch (cbdRouterIndicator) {
      case '':
        viewAccumsUrl = "LegacyMessageBanner";
        break;
      case 'L':
        viewAccumsUrl = "LegacyMessageBanner";
        break;
      case 'N':
        viewAccumsUrl = this.env.viewMemberAccums;
        break;
      case 'K':
        viewAccumsUrl = window.location.origin + '/accums-ui/member/member-detail/accums-ui/summary';
        break;
    }
    return viewAccumsUrl;
  }

  getDeductibleData(): MeterData {
    const data: MeterData = {
      max: this.deductibleData?.accumLimit ? Number(this.deductibleData?.accumLimit) : this.defaultAmountLimit,
      value: this.deductibleData?.amountUsed ? Number(this.deductibleData?.amountUsed) : this.defaultAmountUsed
    };
    return data;
  }

  getOutOfPocketData(): MeterData {
    const data: MeterData = {
      max: this.outOfPocketData?.accumLimit ? Number(this.outOfPocketData?.accumLimit) : this.defaultAmountLimit,
      value: this.outOfPocketData?.amountUsed ? Number(this.outOfPocketData?.amountUsed) : this.defaultAmountUsed
    };
    return data;
  }

  mappingResponse() {
    this.cassError = (this.servicesAndPaymentDetails.claimsInformationResponse as any[]).find(val => val.cassError)?.cassError;

    if (this.cassError) {
      this.noDataFound = true;
    } else {
      this.copayData = this.getAmounts('COPAY');
      this.coinsuranceData = this.getAmounts('COINSURANCE');
      this.deductibleData = this.getAmounts('DEDUCTIBLE');
      this.outOfPocketData = this.getAmounts('OUT_OF_POCKET');
    }
  }

  getAmounts(accumType: string): ClaimsInformationResponse {
    let tempValue = (this.servicesAndPaymentDetails.claimsInformationResponse as any[]).find(
      val => val.familyorIndividualIndicator === 'INDIVIDUAL' &&
        val.accumType === accumType
    );
    return tempValue;
  }

  openServerErrorModal(error) {
    this.modal.openModal(ServerErrorModalComponent, {
      navigateTo: [],
      error: error,
      params: {
        relativeTo: this.route
      }
    }).onClose()
      .subscribe(() => this.goBack());
  }

  goBack() {
    if (window.history.length > 1) {
      window.history.back();
    } else {
      this.router.navigate(['..'], { relativeTo: this.route.parent });
    }
  }
}
