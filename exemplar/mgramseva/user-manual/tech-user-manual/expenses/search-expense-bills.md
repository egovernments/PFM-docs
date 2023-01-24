# Search Expense Bills

## **Link**

→ {base url}/mgramseva/home/searchExpense

![](<../../../../../.gitbook/assets/image (25).png>)

Users are redirected to this screen by selecting the Update Expense card on the home screen.![](blob:https://digit-discuss.atlassian.net/c8e3382f-6264-4770-989f-b8c80f5976f0#media-blob-url=true\&id=7e42a741-9da9-4bfc-879b-2bbafa70c5a7\&collection=contentId-1926791391\&contextId=1926791391\&mimeType=image%2Fpng\&name=Search%20EXpense.png\&size=42495\&width=373\&height=806\&alt=)

Update Expenses card is available on the home screen for defined roles that have EXPENSE PROCESSING permission.

## **User Interaction on Screen**

* Users can search the expense bills with the Vendor Name / Type of Expense / Bill ID ( `Search with any one of these criteria` )
* Click on Search navigates the user to the expense results screen which lists the expenditure bills matching the search criteria.

## **Files Path**

Primary Files:

[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/search\_expense.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/expense/search\_expense.dart)&#x20;

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/expense\_results.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/expense/expense\_results.dart)

![](<../../../../../.gitbook/assets/image (39).png>)

## **Field Validations**

| **Fileds**           | **Validations**            |
| -------------------- | -------------------------- |
| Owner Mobile Number  | `r'^(?:[+0]9)?[0-9]{10}$'` |
| Name of the Consumer | `r'^[A-Za-z ]'`            |
| Old Connection ID    | `No Validation`            |
| New Connection ID    | `No Validation`            |

## **API Details**

| **API**                         | **Params**                                                                                                                                                                               | **Description**                          |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `/egov-mdms-service/v1/_search` | `[{"moduleName": "Expense", "masterDetails": [{"name": "ExpenseType"},]}, {"moduleName": "BillingService", "masterDetails": [{"name": "BusinessService"}, {"name": "TaxHeadMaster"},]}]` | To get the Expense Type for the Dropdown |

### Stack

1 → Home Screen. + Search Expense Bills Screen

Pop → Home Screen

Widgets Utilised from Library

| **Widgets**                                                                                                                                                                                | **File Path**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Description**      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| `BuildTextField`                                                                                                                                                                           | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)                                                                                                                                                                                                                                                                                                                                    | Text Field           |
| <ul><li><br><code>SelectFieldBuilder</code></li></ul><p><strong>(Primary File)</strong></p><ul><li><code>SearchSelectFieldBuilder</code></li></ul><p><strong>(Secondary File)</strong></p> | <p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p><p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SearchSelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SearchSelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p> | Searchable Drop down |
| `BottomButtonBar`                                                                                                                                                                          | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BottonButtonBar.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/BottonButtonBar.dart)                                                                                                                                                                                                                                                                                                                                      | Button               |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
