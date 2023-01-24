# Monthly Dashboard

**Link**. → {base url}/mgramseva/home/dashboard

Users are redirected to this screen if they select the GPWSC Dashboard option on the home screen.

### **User Interaction on Screen**

![](../../../../../.gitbook/assets/Screenshot\_1640844876.png)

* Users can select the year from the drop-down which contains the list of the last 5 Financial years, on tap of any year respective months will be displayed.
* Users can see the user satisfaction average scores of the selected month.
* Users can see the Trend line graph plotted based on both Revenue and Expenditure.
* By selecting any Month from the table, users are navigated to the [Expenditure](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1926791281) and [Revenue](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1926824058) Dashboard screen.
* Users can see the WhatsApp Share button, by tapping on it users can share the Monthly dashboard as a screenshot via WhatsApp.

### **Files Path**

Primary Files: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Dashboard.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/Dashboard.dart) [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_charts.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_charts.dart) [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_dashboard.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_dashboard.dart)

Secondary Files: [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue.dart) , [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/nested\_date\_picker.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/nested\_date\_picker.dart) [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/DashboardCard.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/DashboardCard.dart)

### &#x20;**API Details**

| **End Point**                                         | **Request Method** | **Request Info**                                                                                                                                       |
| ----------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `dashboard-analytics/dashboard/getChartV2`            | POST               | <p><code>aggregationRequestDto</code> : {}</p><p><code>requestDate</code> : {}</p><p><code>headers</code> : {}</p><p><code>RequestInfo</code> : {}</p> |
| `ws-services/wc/_revenueCollectionData`               | POST               | <p>tenantId : {}<br>fromDate : {}<br>toDate : {}</p><p><code>RequestInfo</code> : {}</p>                                                               |
| `echallan-services/eChallan/v1/_chalanCollectionData` | POST               | <p>tenantId : {}<br>fromDate : {}<br>toDate : {}</p><p><code>RequestInfo</code> : {}</p>                                                               |
| `/filestore/v1/files`                                 | POST               | <p><code>tenantId</code> : {}</p><p><code>module</code> : {}</p>                                                                                       |
| `/egov-url-shortening/shortener`                      | POST               | `url` : {}                                                                                                                                             |

### **Stack**

1 → Home Screen + Monthly Dashboard + Revenue Dashboard + update connection screen

Pop → Revenue Dashboard screen → Home Screen

2 → Home Screen + Monthly Dashboard + Expenditure Dashboard + update expenditure screen

Pop → Expenditure Dashboard Screen → Home Screen

3 → Home Screen + Monthly Dashboard + Revenue Dashboard + update connection screen + Update Success

Pop → Home Screen

4 → Home Screen + Monthly Dashboard + Expenditure Dashboard + update expenditure screen + Update Success

Pop → Home Screen

Widgets Utilised from Library

| **Widgets**        | **File Path**                                                                                                                                                                                                                                                                | **Description**    |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `Pagination`       | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/pagination.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/pagination.dart)              | Pagination         |
| `BuildTextField`   | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)  | Text Field         |
| `BillsTable`       | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BillsTable.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/BillsTable.dart) | Table              |
| `LabelText`        | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/LabelText.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/LabelText.dart)                | Subtitle           |
| `NestedDatePicker` | [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/nested\_date\_picker.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/components/Dashboard/nested\_date\_picker.dart)             | Nested Date Picker |

### &#x20;**Role Access Mapping**

```
case Routes.DASHBOARD:
  return ['SUPERUSER', 'DASHBOARD_VIEWER'];
```

### &#x20;**Files Path**

Model → [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/dashboard/revenue\_chart.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/dashboard/revenue\_chart.dart) [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/dashboard/revenue\_dashboard.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/dashboard/revenue\_dashboard.dart)

View → [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Dashboard.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/Dashboard.dart) , [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/Custom%20Label%20widget/custom\_tooltip\_label\_render.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/Custom%20Label%20widget/custom\_tooltip\_label\_render.dart) [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_charts.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_charts.dart) [https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_dashboard.dart](https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/dashboard/revenue\_dashboard/revenue\_dashboard.dart)

Controller → [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/dashboard\_provider.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/providers/dashboard\_provider.dart) , https://github.com/misdwss/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/providers/revenuedashboard\_provider.dart



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
