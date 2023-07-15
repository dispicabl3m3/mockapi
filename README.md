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