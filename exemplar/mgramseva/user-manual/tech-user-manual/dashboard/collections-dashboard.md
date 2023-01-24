# Collections Dashboard

## **Link**

&#x20;→ {base url}/mgramseva/home/dashboard?tab=0.

![](<../../../../../.gitbook/assets/image (60).png>)

Users are redirected to this screen if they select the GPWSC Dashboard option on the home screen.

## **User Interaction on Screen**

* Users can select the year from the drop-down which contains the list of financial years.
* From the text field, users can search connections by using connection ID.
* Users can see the connections data based on the property type for each respective tab (Ex: All, Residential, Commercial).
* Initially, only 10 connections are loaded for the selected tab. The pagination dropdown and right arrow click enable users to view more connections.
* By selecting any connection ID users are navigated to the [Connection update screen](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1926791195).

## **Files Path**

Primary Files:&#x20;

[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Dashboard.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/Dashboard.dart)

[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/search\_expense.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/search\_expense.dart)

## **API Details**

| **End Point**             | **Request Method** | **Request Info**                                                                                                                                                                                                                                                                                      |
| ------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| /`ws-services/wc/_search` | POST               | <p>tenantId : {}<br>offset ; {}<br>limit : {}<br>fromDate : {}<br>toDate : {}<br><code>iscollectionAmount</code>: {}<br><code>isPropertyCount</code>: {}<br><code>propertyType</code>: {}<br><code>connectionNumber</code>: {}<br><code>freeSearch</code>: {}</p><p>sortOrder ; {}<br>sortBy : {}</p> |

### **Stack**

1 → Home Screen. + Dashboard collection screen + update connection screen

Pop → Dashboard collection screen → Home Screen

2 → Home Screen. + Dashboard collection screen + update connection screen + Update Success

Pop → Home Screen

Widgets Utilised from Library

| **Widgets**      | **File Path**                                                                                                                                                                                                                                                                | **Description** |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| `Pagination`     | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/pagination.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/pagination.dart)              | Pagination      |
| `BuildTextField` | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)  | Text Field      |
| `BillsTable`     | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BillsTable.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/BillsTable.dart) | Table           |
| `LabelText`      | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/LabelText.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/LabelText.dart)                | Subtitle        |

## **Role Access Mapping**

```
case Routes.DASHBOARD:
  return ['SUPERUSER', 'DASHBOARD_VIEWER'];
```

## **Files Path**

Model →[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/water\_connections.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/connection/water\_connections.dart)

View →[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Dashboard.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/Dashboard.dart) ,[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/search\_expense.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/search\_expense.dart)

Controller →[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/dashboard\_provider.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/providers/dashboard\_provider.dart) ,[<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/search\_connection\_repo.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/repository/search\_connection\_repo.dart)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
