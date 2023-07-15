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
