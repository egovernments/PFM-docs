# Modify Expenses

## **Link**

→ {base url}/mgramseva/home/searchExpense/result/updateExpense![](blob:https://digit-discuss.atlassian.net/dca6f43c-dcb2-4af6-a499-d1ec10370375#media-blob-url=true\&id=7c300e66-6b1c-4f70-93e8-464b5c325411\&collection=contentId-1927348594\&contextId=1927348594\&mimeType=image%2Fpng\&name=Screenshot%202021-09-20%20at%201.52.54%20AM.png\&size=40178\&width=328\&height=584\&alt=)

Enables employees to modify/edit the expenses based on the status of the payment.

![](<../../../../../.gitbook/assets/image (74).png>)

Update Expenses card is visible on the home screen for defined user roles that have EXPENSE PROCESSING permission.

Clicking on the Update Expenditure card in the expense search results screen navigates the user to the Edit Expense Bills screen.

Users can edit the previously populated expense details for the vendors.

Clicking on the Submit button navigates the users to the Modified Expenditure Success screen.

## **Logic Implemented for Paid or Unpaid Bills**

**Use Case1:** When the status is “Unpaid”

Allows modification of all the details except the Bill Id. Users can Mark the Bill as “Cancelled” by checking on the option.

**Use Case2:** When the status is “Paid”

Cannot modify any details. But the users can Mark the Bill as “Cancelled” by checking the option.

![](<../../../../../.gitbook/assets/image (81).png>)

## File Path

Primary Files -[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/ExpenseDetails.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/AddExpense/ExpenseDetails.dart) ,

## **Field Validations**

| **Fields**                  | **Validations**                                                                    |
| --------------------------- | ---------------------------------------------------------------------------------- |
| Vendor Name\*               | `[A-Za-z ]`                                                                        |
| Mobile Number\*             | `[0-9] & is mandatory only if a new vendor is added`                               |
| Type of Expense\*           | None                                                                               |
| Amount\*                    | `[0-9]`                                                                            |
| Bill Date\*                 |  Before Current Date and after party Bill Date.                                    |
| Party Bill Date             | `Should be before the Bill Date`                                                   |
| Bill Paid                   | None                                                                               |
| Paid Date                   | After Bill date and less than current Date.                                        |
| Attach Documents            | Option to upload a single document, Supported files - PDF, JPEG, PNG (maximun 5MB) |
| Mark this Bill as Cancelled | None                                                                               |

## **API Details**&#x20;

| **API**                         | **Params**                                                                                                                                                                               | **Description**                                                                             |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `/egov-mdms-service/v1/_search` | `[{"moduleName": "Expense", "masterDetails": [{"name": "ExpenseType"},]}, {"moduleName": "BillingService", "masterDetails": [{"name": "BusinessService"}, {"name": "TaxHeadMaster"},]}]` | To get the Expense Type for the Dropdown                                                    |
| `egov.org.in/vendor/v1/_search` | `tenantId: {}`                                                                                                                                                                           | To get the list of vendors in the selected tenant for the suggestion text box - Vendor Name |

### Stack

1 → Home Screen. + Search Expense Screen + Expense Results Screen + Edit Expense Bills Screen

Pop → Expense Results Screen

Widgets Utilised from Library

| **Widgets**                                                                                                                                                                                | **File Path**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Description**       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| `BuildTextField`                                                                                                                                                                           | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)                                                                                                                                                                                                                                                                                                                                    | Text Field            |
| `AutoCompleteView`                                                                                                                                                                         | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/auto\_complete.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/auto\_complete.dart)                                                                                                                                                                                                                                                                                                                                        | Suggestion Text Field |
| <ul><li><br><code>SelectFieldBuilder</code></li></ul><p><strong>(Primary File)</strong></p><ul><li><code>SearchSelectFieldBuilder</code></li></ul><p><strong>(Secondary File)</strong></p> | <p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p><p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SearchSelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SearchSelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p> | Searchable Drop down  |
| `DatePickerFieldBulder`                                                                                                                                                                    | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/DatePickerFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/DatePickerFieldBuilder.dart)                                                                                                                                                                                                                                                                                                                        | Date Picker           |
| `CommonSuccessPage`                                                                                                                                                                        | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/CommonSuccessPage.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/CommonSuccessPage.dart)                                                                                                                                                                                                                                                                                                                                  | Success Screen        |
| `BottomButtonBar`                                                                                                                                                                          | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BottonButtonBar.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/BottonButtonBar.dart)                                                                                                                                                                                                                                                                                                                                      | Button                |



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
