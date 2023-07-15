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