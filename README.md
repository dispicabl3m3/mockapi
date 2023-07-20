import { Component, Input, OnInit } from '@angular/core';
import { UniformBillingDetails } from '../../../shared/models/uniformBillingDetails';
import { ConditionCodes } from '../../../shared/models/conditionCodes';

@Component({
    selector: 'claim-details-uniform-billing-section',
    templateUrl: './uniform-billing.component.html',
    styleUrls: ['./uniform-billing.component.scss']
})
export class ClaimDetailsUniformBillingComponent implements OnInit {

    @Input() uniformBillingDetail: UniformBillingDetails;
    otherPayersDetails: string[] = [];
    conditionCodesDetails: Array<ConditionCodes> = [];

    constructor() { }

    ngOnInit(): void {
        if (this.uniformBillingDetail?.otherPayers) {
            this.otherPayersDetails = this.uniformBillingDetail?.otherPayers.slice(0, 3);
        }
        if (this.uniformBillingDetail?.conditionCodes) {
            this.conditionCodesDetails = this.uniformBillingDetail?.conditionCodes.slice(0, 11);
        }
    }

    checkDateValue(date: string): string {
        if (date && date !== '') {
            return (date.includes('9999') || date.includes('0001')) ? '' : date;
        } else { return ''; }
    }
}

----------------------

Here's an example of a test case for the Angular component described earlier:

```
it('should display other payer details and condition codes details', () => {
  const uniformBillingDetail: UniformBillingDetails = {
    otherPayers: ['Payer 1', 'Payer 2', 'Payer 3', 'Payer 4'],
    conditionCodes: [
      { code: '01', date: '2022-01-01' },
      { code: '02', date: '2022-02-02' },
      { code: '03', date: '2022-03-03' },
      { code: '04', date: '2022-04-04' },
      { code: '05', date: '2022-05-05' },
      { code: '06', date: '2022-06-06' },
      { code: '07', date: '2022-07-07' },
      { code: '08', date: '2022-08-08' },
      { code: '09', date: '2022-09-09' },
      { code: '10', date: '2022-10-10' },
      { code: '11', date: '2022-11-11' },
      { code: '12', date: '2022-12-12' }
    ]
  };
  component.uniformBillingDetail = uniformBillingDetail;
  fixture.detectChanges();
  const otherPayersDetails: string[] = ['Payer 1', 'Payer 2', 'Payer 3'];
  const conditionCodesDetails: ConditionCodes[] = [
    { code: '01', date: '2022-01-01' },
    { code: '02', date: '2022-02-02' },
    { code: '03', date: '2022-03-03' },
    { code: '04', date: '2022-04-04' },
    { code: '05', date: '2022-05-05' },
    { code: '06', date: '2022-06-06' },
    { code: '07', date: '2022-07-07' },
    { code: '08', date: '2022-08-08' },
    { code: '09', date: '2022-09-09' },
------------------
describe('checkDateValue', () => { it('should return an empty string if date is null

or empty', () => {

expect(checkDateValue(null)).toEqual("); expect(checkDateValue('')).toEqual('');

});

it('should return an empty string if date includes "9999" or "0001", () => {

expect(checkDateValue('12/31/9999')).toEqual ('');

expect(checkDateValue('01/01/0001')).toEqual

('');

expect(checkDateValue('12/31/1999')).toEqual ('12/31/1999');

});

it('should return the original date string if it is valid', () => {

expect(checkDateValue('12/31/1999')).toEqual ('12/31/1999');

expect(checkDateValue('01/01/2000')).toEqual ('01/01/2000');

});

});


Here's an example of a test case that tests the `checkDateValue` function:

```
describe('checkDateValue', () => {
  it('should return the correct date value', () => {
    const date1 = '9999-12-31T00:00:00';
    const date2 = '2023-07-15T07:51:00';
    const date3 = '0001-01-01T00:00:00';
    const date4 = '';
    const checkedDate1 = checkDateValue(date1);
    const checkedDate2 = checkDateValue(date2);
    const checkedDate3 = checkDateValue(date3);
    const checkedDate4 = checkDateValue(date4);
    expect(checkedDate1).toEqual('');
    expect(checkedDate2).toEqual('2023-07-15T07:51:00');
    expect(checkedDate3).toEqual('');
    expect(checkedDate4).toEqual('');
  });
});
```

This test case creates four `string` variables, one with a date that includes '9999', one with a valid date, one with a date that includes '0001', and one with an empty string. The test case then passes each of these variables to the `checkDateValue` function. The test case then checks that the result of the function is equal to the expected checked date.

-------------
Sure thing! Here's an example Karma test case that tests the behavior of the `ClaimDetailsUniformBillingComponent` component:

```
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { ClaimDetailsUniformBillingComponent } from './uniform-billing.component';
import { UniformBillingDetails } from '../../../shared/models/uniformBillingDetails';
import { ConditionCodes } from '../../../shared/models/conditionCodes';

describe('ClaimDetailsUniformBillingComponent', () => {
  let component: ClaimDetailsUniformBillingComponent;
  let fixture: ComponentFixture<ClaimDetailsUniformBillingComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ClaimDetailsUniformBillingComponent]
    })
      .compileComponents();
  });

  beforeEach(() => {
    fixture = TestBed.createComponent(ClaimDetailsUniformBillingComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });

  it('should set otherPayersDetails to the first three elements of otherPayers', () => {
    const uniformBillingDetail: UniformBillingDetails = {
      otherPayers: ['payer1', 'payer2', 'payer3', 'payer4', 'payer5']
    };
    component.uniformBillingDetail = uniformBillingDetail;
    component.ngOnInit();
    expect(component.otherPayersDetails).toEqual(['payer1', 'payer2', 'payer3']);
  });

  it('should set conditionCodesDetails to the first eleven elements of conditionCodes', () => {
    const uniformBillingDetail: UniformBillingDetails = {
      conditionCodes: [
        { code: 'code1', date: '2023-07-15' },
        { code: 'code2', date: '2023-07-14' },
        { code: 'code3', date: '2023-07-13' },
        { code: 'code4', date: '2023-07-12' },
        { code: 'code5', date: '2023-07-11' },
        { code: 'code6', date: '2023-07-10' },
        { code: 'code7', date: '2023-07-09' },
        { code: 'code8', date: '2023-07-08' },
        { code: 'code9', date: '2023-07-07' },
        { code: 'code10', date: '2023-07-06' },
        --------------------------------------------------------
        import { Component, OnInit, Input, ViewEncapsulation } from '@angular/core';
import { ServicesAndPaymentsSummary } from '../../../shared/models/servicesAndPaymentsSummary';
import { MeterData, ServerErrorModalComponent, ModalService, NotificationMessageModalComponent, RequestBuilder } from 'ui-commons';
import { ClaimsInformationResponse, ClaimsCassErrorData } from '../../../shared/models/claimsInformationResponse';
import { Constants} from '../../../../../claims-ui-claims-inquiry-services-module/src/projects';
import { PatientSummary } from '../../../shared/models/patientSummary';
import { takeUntil } from 'rxjs/operators';
import { ActivatedRoute } from '@angular/router';
import { Subject } from 'rxjs';

@Component({
    selector: 'claim-summary-service-payments-section',
    templateUrl: './service-summary.component.html',
    styleUrls: ['./service-summary.component.scss'],
    encapsulation: ViewEncapsulation.None
})
export class ClaimSummaryServicePaymentsComponent implements OnInit {
    @Input() servicesSummary: ServicesAndPaymentsSummary;
    @Input() patientSummary: PatientSummary;
    @Input() servicesVisible = false;
    @Input() accumsVisible = false;
    deductibleData: ClaimsInformationResponse;
    outOfPocketData: ClaimsInformationResponse;
    cassError: ClaimsCassErrorData;
    private unsubscribe$ = new Subject<void>();
    // temporary default values
    defaultAmountLimit = 0;
    defaultAmountUsed = 0;
    noDataFound = false;

    constructor(
        private route: ActivatedRoute,
        public modal: ModalService,
        public requestBuilder: RequestBuilder

    ) { }

    ngOnInit(): void {
        this.mappingResponse();
    }

    checkValueNotEmpty(value: string): string {
        return (value && value !== '') ? value : '-';
    }

    checkDateValue(date: string): string {
        if (date && date !== '') {
            return (date.includes('9999') || date.includes('0001')) ? '' : date;
        } else { return ''; }
    }

    getDeductibleData(): MeterData {
        const data: MeterData = {
            max: this.deductibleData?.accumLimit ? Number(this.deductibleData?.accumLimit) : this.defaultAmountLimit,
            value: this.deductibleData?.amountUsed ? + this.deductibleData?.amountUsed : this.defaultAmountUsed
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
        this.cassError = (this.servicesSummary.accumulators.claimsInformationResponse as any[]).find(
            val => val.cassError
        )?.cassError;

        if (this.cassError) {
            if (this.cassError.systemError) {
                this.openServerErrorModal();
            }
            this.noDataFound = true;
        } else {
            this.deductibleData = this.getAmounts('DEDUCTIBLE');
            this.outOfPocketData = this.getAmounts('OUT_OF_POCKET');
        }
    }

    getAmounts(accumType: string): ClaimsInformationResponse {
        let tempValue = (this.servicesSummary.accumulators.claimsInformationResponse as any[]).find(
            val => val.familyorIndividualIndicator === 'INDIVIDUAL' &&
                val.accumType === accumType
        );
        if (!tempValue) {
            tempValue = (this.servicesSummary.accumulators.claimsInformationResponse as any[]).find(
                val => val.familyorIndividualIndicator === 'FAMILY' &&
                    val.accumType === accumType
            );
        }
        return tempValue;
    }

    openServerErrorModal() {
        this.modal.openModal(ServerErrorModalComponent, {
            navigateTo: ['..', ],
            error: {
                message: this.cassError.systemErrorMessage,
                timestamp: this.cassError.timeStamp,
                sourceList: [{
                    parameter: 'Reference Number',
                    pointer: this.cassError.referenceNumber
                }]
            },
            params: {
                relativeTo: this.route
            }
        }).onClose()
            .pipe(takeUntil(this.unsubscribe$))
            .subscribe(() => { });
    }

    viewAccumsDetails() {
        if (this.servicesSummary.cbdRouterIndicator) {
            switch (this.servicesSummary.cbdRouterIndicator) {
                case 'L':
                case ' ':
                    this.modal.openModal(
                    NotificationMessageModalComponent,
                    {}
                    ).onClose().subscribe(() => { });
                    break;
                case 'N':
                    window.open('https://accumui.fyiblue.com/accumui/login.do', '_blank');
                    break;
                case 'K':
                    this.accumsSummaryDetails();
                    break;
            }
        }
    }

accumsSummaryDetails() {
    const subId = this.patientSummary.subscriberId;
    const grpId = this.patientSummary.groupId;
    const setAccumsData = {
        corporateEntityCode: this.patientSummary.corporateEntityCode.length === 3 ?
         this.patientSummary.corporateEntityCode : this.patientSummary.corporateEntityCode + '1',
        groupNumber: grpId.substr(-6),
        memberPartyId: this.patientSummary.memberId,
        policyEffectiveEndEpoch:  this.patientSummary.policyEffectiveEndDate,
        policyEffectiveStartEpoch:  this.patientSummary.policyEffectiveStartDate,
        searchType: Constants.MEMBER_PARTY,
        sectionNumber: this.patientSummary.sectionNumber,
        singleResult: true,
        subscriberId: subId.substr(-12),
        subscriberPartyId:  this.patientSummary.subscriberPartyId
    };
    const request = {
        memberPartyId: setAccumsData.memberPartyId.toString(),
        subpartyId: ''
    };
    this.requestBuilder.store(Constants.MEMBER_PARTY_FORM_KEY, request);
    this.requestBuilder.store(Constants.MEMBER_HISTORY_SEARCH_PARAMS, setAccumsData);
    this.requestBuilder.store('SELECTED_GROUPNUMBER', parseInt(setAccumsData?.groupNumber, 10));
    this.requestBuilder.store('SELECTED_MEMBER_PARTY_ID', parseInt(setAccumsData?.memberPartyId, 10));
    this.requestBuilder.store('SELECTED_POLICY_EFFECTIVE_DATE', setAccumsData?.policyEffectiveStartEpoch);

    const BASE_URL = window.location.origin;
    window.open(BASE_URL + '/accums-ui/member/member-detail/accums-ui/summary', '_blank');
}
}/////////////////////
import { ComponentFixture, TestBed } from '@angular/core/testing';

import { ClaimPatientAccumulationsComponent } from './accumulations.component';
import { NullEmptyToNaPipe, Angulartics2LaunchByAdobe, MeterComponent, NotificationMessageModalComponent, RequestBuilder } from 'ui-commons';
import { RouterTestingModule } from '@angular/router/testing';
import { HttpClientTestingModule } from '@angular/common/http/testing';
import { MatDivider } from '@angular/material/divider';
import { MemberRequest } from 'projects/claims-ui-app/src/app/model/memberRequest';
import { Router } from '@angular/router';
import { Constants } from 'projects/claims-ui-app/src/app/claims-ui-claims-inquiry-services-module/src/projects';

let adobeAnalytics: jasmine.SpyObj<Angulartics2LaunchByAdobe>;
const accumulationDetails = {
  claimsInformationResponse : [
    {
        accumLimit: '16300.00',
        accumType: 'DEDUCTIBLE',
        amountApplied: '1250.00',
        amountRemaining: '15050.00',
        amountUsed: '1250.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'IN_NETWORK',
        familyorIndividualIndicator: 'INDIVIDUAL',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    },
    {
        accumLimit: '16300.00',
        accumType: 'DEDUCTIBLE',
        amountApplied: '250.00',
        amountRemaining: '16050.00',
        amountUsed: '250.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'OUT_OF_NETWORK',
        familyorIndividualIndicator: 'INDIVIDUAL',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    },
    {
        accumLimit: '16300.00',
        accumType: 'DEDUCTIBLE',
        amountApplied: '750.00',
        amountRemaining: '15550.00',
        amountUsed: '750.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'IN_NETWORK',
        familyorIndividualIndicator: 'FAMILY',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    },
    {
        accumLimit: '16300.00',
        accumType: 'DEDUCTIBLE',
        amountApplied: '800.00',
        amountRemaining: '15500.00',
        amountUsed: '800.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'OUT_OF_NETWORK',
        familyorIndividualIndicator: 'FAMILY',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    },
    {
        accumLimit: '12300.00',
        accumType: 'OUT_OF_POCKET',
        amountApplied: '250.00',
        amountRemaining: '12050.00',
        amountUsed: '250.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'IN_NETWORK',
        familyorIndividualIndicator: 'INDIVIDUAL',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    },
    {
        accumLimit: '12300.00',
        accumType: 'OUT_OF_POCKET',
        amountApplied: '200.00',
        amountRemaining: '12100.00',
        amountUsed: '200.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'OUT_OF_NETWORK',
        familyorIndividualIndicator: 'INDIVIDUAL',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    },
    {
        accumLimit: '12300.00',
        accumType: 'OUT_OF_POCKET',
        amountApplied: '250.00',
        amountRemaining: '12050.00',
        amountUsed: '250.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'IN_NETWORK',
        familyorIndividualIndicator: 'FAMILY',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    },
    {
        accumLimit: '10000.00',
        accumType: 'OUT_OF_POCKET',
        amountApplied: '2000.00',
        amountRemaining: '8000.00',
        amountUsed: '2000.00',
        appliedToSubscript: '00',
        benefitPeriodBeginningDate: '2021-01-01T06:00:00.000+0000',
        benefitPeriodEndingDate: '2021-12-31T06:00:00.000+0000',
        carryOverCreditIndicator: '0',
        costContainmentIndicator: 'OUT_OF_NETWORK',
        familyorIndividualIndicator: 'FAMILY',
        icdNo: 'NONE',
        internalDescriptor: 'OUTPOCKET',
        percentageLevel: '0.50',
        placeOfTreatment: '',
        treatmentGroup: '0R',
        valueQualifier: 'DOLLARS'
    }
  ]
};

describe('ClaimPatientAccumulationsComponent', () => {
  let component: ClaimPatientAccumulationsComponent;
  let fixture: ComponentFixture<ClaimPatientAccumulationsComponent>;

  beforeEach(async () => {
    adobeAnalytics = jasmine.createSpyObj('Angulartics2LaunchByAdobe', ['eventTrack', 'isAuthorized']);
    await TestBed.configureTestingModule({
      declarations: [ ClaimPatientAccumulationsComponent, NullEmptyToNaPipe, MatDivider, MeterComponent ],
      imports: [RouterTestingModule, HttpClientTestingModule],
      providers: [{ provide: Angulartics2LaunchByAdobe, useValue: adobeAnalytics}]
    })
    .compileComponents();
  });

  beforeEach(() => {
    fixture = TestBed.createComponent(ClaimPatientAccumulationsComponent);
    component = fixture.componentInstance;
    component.accumulationDetails = accumulationDetails;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });

  /////////////////////////

  it('should map data correctly when there is no cassError', () => {
    const component = new ClaimPatientAccumulationsComponent(null, null, null, null, null);
    component.accumulationDetails = {
        claimsInformationResponse: [
            {
                familyorIndividualIndicator: 'INDIVIDUAL',
                accumType: 'DEDUCTIBLE',
                costContainmentIndicator: 'IN_NETWORK',
                accumLimit: 100,
                amountUsed: 50
            },
            {
                familyorIndividualIndicator: 'INDIVIDUAL',
                accumType: 'DEDUCTIBLE',
                costContainmentIndicator: 'NON_PARTICIPATING',
                accumLimit: 200,
                amountUsed: 100
            }
        ]
    };
    component.mappingResponse();
    expect(component.noDataFound).toBeFalsy();
});

it('test_behaviour_K', () => {
  spyOn(component, 'goToAccumsSummary');
  component.accumulationDetails.cbdRouterIndicator = 'K';
  component.viewAccumsDetails();
  expect(component.goToAccumsSummary).toHaveBeenCalled();
});

it('test_behaviour_N', () => {
  spyOn(window, 'open');
  component.accumulationDetails.cbdRouterIndicator = 'N';
  component.viewAccumsDetails();
  expect(window.open).toHaveBeenCalledWith('https://accumui.fyiblue.com/accumui/login.do', '_blank');
});

//
it('test_behaviour_L', () => {
  spyOn(component.modal, 'openModal').and.returnValue({ onClose: () => { } });
  component.accumulationDetails.cbdRouterIndicator = 'L';
  component.viewAccumsDetails();
  expect(component.modal.openModal).toHaveBeenCalledWith(NotificationMessageModalComponent, {});
});
//

it('test_edge_case_undefined', () => {
  spyOn(component.modal, 'openModal');
  component.accumulationDetails.cbdRouterIndicator = undefined;
  component.viewAccumsDetails();
  expect(component.modal.openModal).not.toHaveBeenCalled();
});



});
/////////////////////////////////

import { Component, OnInit, Input } from '@angular/core';
import { ClaimsInformationResponse, ClaimsCassErrorData } from '../../../shared/models/claimsInformationResponse';
import { MeterData, ServerErrorModalComponent, ModalService, RequestBuilder, NotificationMessageModalComponent, Angulartics2LaunchByAdobe } from 'ui-commons';
import { Constants, PartyModel, PartyMapper, SearchRequest } from '../../../../../claims-ui-claims-inquiry-services-module/src/projects';
import { ActivatedRoute, Router } from '@angular/router';
import { takeUntil } from 'rxjs/operators';
import { Subject } from 'rxjs';

@Component({
    selector: 'claim-patient-accumulations-section',
    templateUrl: './accumulations.component.html',
    styleUrls: ['./accumulations.component.scss']
})
export class ClaimPatientAccumulationsComponent implements OnInit {

    @Input() accumulationDetails: any = null;
    @Input() memberRequest: any = null; // same as MemberHistorySearchParams type in 'claims-keystone-accums-ui-services-client-module'
    cassError: ClaimsCassErrorData;
    private unsubscribe$ = new Subject<void>();

    idiData: ClaimsInformationResponse; // Individual - Deductible - In Network
    idoData: ClaimsInformationResponse; // Individual - Deductible - Out of Network
    fdiData: ClaimsInformationResponse; // Family - Deductible - In Network
    fdoData: ClaimsInformationResponse; // Family - Deductible - Out of Network
    ioiData: ClaimsInformationResponse; // Individual - Out of Pocket - In Network
    iooData: ClaimsInformationResponse; // Individual - Out of Pocket - Out of Network
    foiData: ClaimsInformationResponse; // Family - Out of Pocket - In Network
    fooData: ClaimsInformationResponse; // Family - Out of Pocket - Out of Network

    idiMeterData: MeterData; // Individual - Deductible - In Network
    idoMeterData: MeterData; // Individual - Deductible - Out of Network
    fdiMeterData: MeterData; // Family - Deductible - In Network
    fdoMeterData: MeterData; // Family - Deductible - Out of Network
    ioiMeterData: MeterData; // Individual - Out of Pocket - In Network
    iooMeterData: MeterData; // Individual - Out of Pocket - Out of Network
    foiMeterData: MeterData; // Family - Out of Pocket - In Network
    fooMeterData: MeterData; // Family - Out of Pocket - Out of Network

    noDataFound = false;

    constructor(
        private router: Router,
        private route: ActivatedRoute,
        public modal: ModalService,
        public requestBuilder: RequestBuilder,
        private adobeAnalytics: Angulartics2LaunchByAdobe
    ) { }

    ngOnInit(): void {
        this.mappingResponse();
    }

    mappingResponse() {
        this.cassError = (this.accumulationDetails.claimsInformationResponse as any[]).find(
            val => val.cassError
        )?.cassError;

        if (this.cassError) {
            if (this.cassError.systemError) {
                this.openServerErrorModal();
            }
            this.noDataFound = true;
        } else {
            // get data for each section
            this.idiData = this.getData('INDIVIDUAL', 'DEDUCTIBLE', 'IN_NETWORK');
            this.idiMeterData = this.getMeterData(this.idiData);
            this.idoData = this.getData('INDIVIDUAL', 'DEDUCTIBLE', 'NON_PARTICIPATING');
            this.idoMeterData = this.getMeterData(this.idoData);
            this.fdiData = this.getData('FAMILY', 'DEDUCTIBLE', 'IN_NETWORK');
            this.fdiMeterData = this.getMeterData(this.fdiData);
            this.fdoData = this.getData('FAMILY', 'DEDUCTIBLE', 'NON_PARTICIPATING');
            this.fdoMeterData = this.getMeterData(this.fdoData);
            this.ioiData = this.getData('INDIVIDUAL', 'OUT_OF_POCKET', 'IN_NETWORK');
            this.ioiMeterData = this.getMeterData(this.ioiData);
            this.iooData = this.getData('INDIVIDUAL', 'OUT_OF_POCKET', 'NON_PARTICIPATING');
            this.iooMeterData = this.getMeterData(this.iooData);
            this.foiData = this.getData('FAMILY', 'OUT_OF_POCKET', 'IN_NETWORK');
            this.foiMeterData = this.getMeterData(this.foiData);
            this.fooData = this.getData('FAMILY', 'OUT_OF_POCKET', 'NON_PARTICIPATING');
            this.fooMeterData = this.getMeterData(this.fooData);
        }
    }

    getData(familyorIndividualIndicator: string, accumType: string, costContainmentIndicator: string): ClaimsInformationResponse {
        return (this.accumulationDetails.claimsInformationResponse as any[]).find(
            val => val.familyorIndividualIndicator === familyorIndividualIndicator &&
                val.accumType === accumType &&
                val.costContainmentIndicator === costContainmentIndicator
        );
    }

    getMeterData(data) {
        return { max: +data?.accumLimit || 0, value: +data?.amountUsed || 0};
    }

    openServerErrorModal() {
        this.modal.openModal(ServerErrorModalComponent, {
            navigateTo: [],
            error: {
                message: this.cassError.systemErrorMessage,
                timestamp: this.cassError.timeStamp,
                sourceList: [{
                    parameter: 'Reference Number',
                    pointer: this.cassError.referenceNumber
                }]
            },
            params: {
                relativeTo: this.route
            }
        }).onClose()
            .pipe(takeUntil(this.unsubscribe$))
            .subscribe(() => {});
    }

    viewAccumsDetails() {
        this.adobeAnalytics.eventTrack('cl_click_view_accums_details');
        if (this.accumulationDetails.cbdRouterIndicator || this.accumulationDetails.cbdRouterIndicator === '') {
            switch (this.accumulationDetails.cbdRouterIndicator) {
                case 'K':
                    this.goToAccumsSummary();
                    break;
                case 'N':
                    window.open('https://accumui.fyiblue.com/accumui/login.do', '_blank');
                    break;
                case 'L':
                case '':
                    this.modal.openModal(
                        NotificationMessageModalComponent,
                        {}
                    ).onClose().subscribe(() => { });
                    break;
            }
        }
    }

    goToAccumsSummary() {
        const requestParams: PartyModel = {
            memberPartyId: this.memberRequest.memberPartyId,
            subpartyId: ''
        };
        this.requestBuilder.mapRequest<PartyModel, SearchRequest>(Constants.MEMBER_SEARCH_REQUEST_KEY,
            requestParams, new PartyMapper()
        );
        this.requestBuilder.store(Constants.MEMBER_PARTY_FORM_KEY, requestParams );
        this.requestBuilder.store(Constants.MEMBER_HISTORY_SEARCH_PARAMS, this.memberRequest);
        sessionStorage.setItem(Constants.SELECTED_GROUPNUMBER, this.memberRequest.groupNumber);
        this.requestBuilder.store(Constants.SELECTED_MEMBER_PARTY_ID, parseInt(this.memberRequest.memberPartyId, 10));
        this.requestBuilder.store(Constants.SELECTED_POLICY_EFFECTIVE_DATE, this.memberRequest.policyEffectiveStartEpoch);
        this.router.navigate(['accums-ui', 'member', 'member-detail', 'accums-ui', 'summary']);
    }

}
//////////////
// Import necessary dependencies and the function to test
import { goToAccumsSummary } from '../path/to/your-file';
import { PartyModel } from '../path/to/PartyModel';
import { SearchRequest } from '../path/to/SearchRequest';

describe('goToAccumsSummary', () => {
  let mockRequestBuilder: any; // Mock for RequestBuilder
  let mockRouter: any; // Mock for Router
  let mockMemberRequest: any; // Mock for memberRequest

  beforeEach(() => {
    // Initialize mock objects before each test
    mockRequestBuilder = {
      mapRequest: jasmine.createSpy('mapRequest'),
      store: jasmine.createSpy('store'),
    };
    mockRouter = {
      navigate: jasmine.createSpy('navigate'),
    };
    // Create a mock memberRequest object with the required properties
    mockMemberRequest = {
      memberPartyId: '123',
      groupNumber: '456',
      policyEffectiveStartEpoch: '2023-07-20',
    };
  });

  it('should correctly call mapRequest and store methods', () => {
    const expectedPartyModel: PartyModel = {
      memberPartyId: '123',
      subpartyId: '',
    };

    // Call the function with the mock objects
    goToAccumsSummary.call(
      {
        memberRequest: mockMemberRequest,
        requestBuilder: mockRequestBuilder,
        router: mockRouter,
      }
    );

    // Assertions to check if the mapRequest and store methods are called with the expected parameters
    expect(mockRequestBuilder.mapRequest).toHaveBeenCalledWith(
      jasmine.any(String),
      expectedPartyModel,
      jasmine.any(Object) // Replace this with the appropriate PartyMapper mock
    );

    expect(mockRequestBuilder.store).toHaveBeenCalledWith(
      jasmine.any(String),
      expectedPartyModel
    );

    expect(mockRequestBuilder.store).toHaveBeenCalledWith(
      jasmine.any(String),
      mockMemberRequest
    );

    expect(mockRequestBuilder.store).toHaveBeenCalledWith(
      jasmine.any(String),
      parseInt(mockMemberRequest.memberPartyId, 10)
    );

    expect(mockRequestBuilder.store).toHaveBeenCalledWith(
      jasmine.any(String),
      mockMemberRequest.policyEffectiveStartEpoch
    );
  });

  // Add more test cases as needed
});