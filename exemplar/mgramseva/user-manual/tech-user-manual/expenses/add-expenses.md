# Add Expenses

## **Link**

→ {base url}/mgramseva/home/addExpense

![](<../../../../../.gitbook/assets/image (2).png>)

Enables employees to add expenses - the process of onboarding the end-users.

Add Expenses card is available on the home screen for defined user roles having the EXPENSE PROCESSING permission.

Clicking the Add Expense Record tile/card on the home screen navigates the user to Add Expenses screen.

The user enters the required details to add the expenses for the vendors.

If a user logs in for the first time then a walkthrough is populated following the same logic as in the home screen.

Clicking on the Submit button navigates the user to the Expenditure Added Successful acknowledgement screen.

![](<../../../../../.gitbook/assets/image (66).png>)

## **Logic Implemented for Date Validation and File Attachments**

### **File Attachments**

This feature allows the user to take a picture or choose a single file. The [Image Picker](https://pub.dev/packages/image\_picker) plugin is used to implement this.

Whenever this application is used on mobile, it prompts the user with two options - Camera and File Picker. If the application is opened on desktop or laptop browsers, the camera option is not available. The user has to select an image from the folder.

The maximum supported file size is 5 MB.

### &#x20;**Date Validation**

For validating the form we use the Form widget. Once the user selects a bill date the Bill Pay option is enabled. Else, the auto validation process is enabled.

Based on the bill date, the party selection date is enabled. If the user selects the party selection date first, the bill date can be selected only after entering the party date.

Whenever the bill paid option is true, the paid date field is enabled and mandatory. The date selection range allows date input only after the bill date and before the current date.

## **File Path**

Primary Files -

[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/ExpenseDetails.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/AddExpense/ExpenseDetails.dart)

&#x20;[<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/WalkThroughContainer.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/AddExpense/AddExpenseWalkThrough/WalkThroughContainer.dart)&#x20;

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/expenseWalkThrough.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/AddExpense/AddExpenseWalkThrough/expenseWalkThrough.dart)

| **Fields**        | **Validations**                                                                    |
| ----------------- | ---------------------------------------------------------------------------------- |
| Vendor Name\*     | `[A-Za-z ]`                                                                        |
| Mobile Number\*   | `[0-9] & is mandatory only if a new vendor is added`                               |
| Type of Expense\* | None                                                                               |
| Amount\*          | `[0-9]`                                                                            |
| Bill Date\*       |  Before Current Date and after party Bill Date.                                    |
| Party Bill Date   | `Should be before the Bill Date`                                                   |
| Bill Paid         | None                                                                               |
| Paid Date         |  After Bill date and less than current Date.                                       |
| Attach Documents  | Option to upload a single document, Supported files - PDF, JPEG, PNG (maximum 5MB) |

{% hint style="info" %}
**Note:** All fields are validated on Submit apart from the Mobile number which gets validated on change.
{% endhint %}

## **API Details**

| **API**                         | **Params**                                                                                                                                                                               | **Description**                                                                             |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `/egov-mdms-service/v1/_search` | `[{"moduleName": "Expense", "masterDetails": [{"name": "ExpenseType"},]}, {"moduleName": "BillingService", "masterDetails": [{"name": "BusinessService"}, {"name": "TaxHeadMaster"},]}]` | To get the Expense Type for the Dropdown                                                    |
| `egov.org.in/vendor/v1/_search` | `tenantId: {}`                                                                                                                                                                           | To get the list of vendors in the selected tenant for the suggestion text box - Vendor Name |

### Stack

1 → Home Screen. + Add Expense Screen

Pop → Home Screen

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
