import { Component, Input, OnChanges, OnInit, SimpleChanges } from '@angular/core';
import { ActivatedRoute, Router } from '@angular/router';
import { Angulartics2LaunchByAdobe, RequestBuilder } from 'ui-commons';
import { ClientMemberIdModel, ClientMemberIdMapper, GroupModel, GroupMapper, Constants } from '../../../claims-ui-claims-inquiry-services-module/src/projects';
import { SearchRequest } from '../../../model/searchRequest';
import { ClaimSummaryService } from '../shared/services/claim-summary.service';

@Component({
  selector: 'tab-section-header',
  templateUrl: './tab-section-header.component.html',
  styleUrls: ['./tab-section-header.component.scss']
})

export class TabSectionHeaderComponent implements OnInit {

  @Input() headerContent;

  @Input() providerDetails;

  @Input() patientDetails;
  screenName;
  loadDropdownContent;
  claimDateFormat: any;
  today: any;
  data: any;
  viewAdditionalDetailsOptions = ['Find Patient Claims (via Member ID)', 'Find Patient Claims (via Member ID and Service Dates)', 'Find Additional Claims (via ID/Group ID)', 'Find Additional Claims (via ID/Group ID and Service Dates)'];
  claimCorporateEntityCodes: any = [];
  subIdCorporateEntityCodes: any = [];
  defaultCorporateEntityCodes: any = [];

  constructor(private route: ActivatedRoute,
    private adobeAnalytics: Angulartics2LaunchByAdobe,
    public requestBuilder: RequestBuilder,
    private component: ClaimSummaryService,
    private router: Router
  ) {
  }

  ngOnInit(): void {
    this.screenName = this.route.snapshot.routeConfig.path;
    this.loadDropdownContent = this.providerDetails;
  }

  onDropDownSubmit(event) {
    this.adobeAnalytics.eventTrack('cl_select_view_additional_claims');
    this.claimDateFormat = new Date(this.patientDetails?.claimFromDate);
    this.today = new Date();
    if (event.currentValue === this.viewAdditionalDetailsOptions[0]) {
      this.data = {
        corporateEntityCodes: this.claimCorporateEntityCodes.length > 0 ? this.claimCorporateEntityCodes : this.defaultCorporateEntityCodes,
        clientMemberId: this.patientDetails?.memberId,
        serviceFromDate: this.component.getServiceFromMinusYearDate(this.claimDateFormat),
        serviceToDate: { formatted: this.today, epoc: this.component.getEpochFromDate(this.today) },
        dispositionFromDate: '',
        dispositionToDate: ''
      };
      this.requestBuilder.mapRequest<ClientMemberIdModel, SearchRequest>(Constants.CLAIMS_SEARCH_REQUEST_KEY, this.data as ClientMemberIdModel, new ClientMemberIdMapper());
      this.requestBuilder.store(Constants.CLAIMS_CLIENT_MEMBER_ID_FORM_KEY, this.data);
      this.requestBuilder.store(Constants.CLAIMS_SEARCH_TYPE_KEY, Constants.ClaimsStorageValues.CLAIMSCLIENTMEMBERID);
      this.onSelectOfDropdownOpenInNewTab('claimsclientmemberid');
    } else if (event.currentValue === this.viewAdditionalDetailsOptions[1]) {
      this.data = {
        corporateEntityCodes: this.claimCorporateEntityCodes.length > 0 ? this.claimCorporateEntityCodes : this.defaultCorporateEntityCodes,
        clientMemberId: this.patientDetails?.memberId,
        serviceFromDate: this.component.getTodaysServiceFromDate(this.claimDateFormat),
        serviceToDate: this.component.getTodaysServiceFromDate(this.today),
        dispositionFromDate: '',
        dispositionToDate: ''
      };
      this.requestBuilder.mapRequest<ClientMemberIdModel, SearchRequest>(Constants.CLAIMS_SEARCH_REQUEST_KEY, this.data as ClientMemberIdModel, new ClientMemberIdMapper());
      this.requestBuilder.store(Constants.CLAIMS_CLIENT_MEMBER_ID_FORM_KEY, this.data);
      this.requestBuilder.store(Constants.CLAIMS_SEARCH_TYPE_KEY, Constants.ClaimsStorageValues.CLAIMSCLIENTMEMBERID);
      this.onSelectOfDropdownOpenInNewTab('claimsclientmemberid');
    } else if (event.currentValue === this.viewAdditionalDetailsOptions[2]) {
      this.data = {
        corporateEntityCodes: this.subIdCorporateEntityCodes.length > 0 ? this.subIdCorporateEntityCodes : this.defaultCorporateEntityCodes,
        subscriberId: this.patientDetails?.subscriberId,
        groupId: this.patientDetails?.groupId,
        serviceFromDate: this.component.getServiceFromMinusYearDate(this.claimDateFormat),
        serviceToDate: { formatted: this.today, epoc: this.component.getEpochFromDate(this.today) },
        dispositionFromDate: '',
        dispositionToDate: ''
      };
      this.requestBuilder.store(Constants.CLAIMS_GROUP_FORM_KEY, this.data);
      this.requestBuilder.store(Constants.CLAIMS_SEARCH_TYPE_KEY, Constants.ClaimsStorageValues.CLAIMSGROUP);
      this.requestBuilder.mapRequest<GroupModel, SearchRequest>(Constants.CLAIMS_SEARCH_REQUEST_KEY, this.data as GroupModel, new GroupMapper());
      this.onSelectOfDropdownOpenInNewTab('claimsgroup');
    } else if (event.currentValue === this.viewAdditionalDetailsOptions[3]) {
      this.data = {
        corporateEntityCodes: this.subIdCorporateEntityCodes.length > 0 ? this.subIdCorporateEntityCodes : this.defaultCorporateEntityCodes,
        subscriberId: this.patientDetails?.subscriberId,
        groupId: this.patientDetails?.groupId,
        serviceFromDate: this.component.getTodaysServiceFromDate(this.claimDateFormat),
        serviceToDate: this.component.getTodaysServiceFromDate(this.today),
        dispositionFromDate: '',
        dispositionToDate: ''
      };
      this.requestBuilder.store(Constants.CLAIMS_GROUP_FORM_KEY, this.data);
      this.requestBuilder.store(Constants.CLAIMS_SEARCH_TYPE_KEY, Constants.ClaimsStorageValues.CLAIMSGROUP);
      this.requestBuilder.mapRequest<GroupModel, SearchRequest>(Constants.CLAIMS_SEARCH_REQUEST_KEY, this.data as GroupModel, new GroupMapper());
      this.onSelectOfDropdownOpenInNewTab('claimsgroup');
    }
  }

  onSelectOfDropdownOpenInNewTab(searchData) {
    const url = this.router.serializeUrl(
      this.router.createUrlTree(
        [`../../results`], { relativeTo: this.route.parent, queryParams: { searchType: searchData } }
      ));
    window.open(url, '_blank');
  }

  openInNewTab() {
    window.open(window.location.href, '_blank');
  }
  
  openNewTab(url) {
    window.open(url, '_blank');
  }

  externalBadgeLinkClicked(badge) {
    if(badge.analyticsEvent) {
      this.adobeAnalytics.eventTrack(badge.analyticsEvent);
    }
    this.openNewTab(badge.url);
  }
}
