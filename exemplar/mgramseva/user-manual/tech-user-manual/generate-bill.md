# Generate Bill

## Manual Bulk Demand Generation

**Link**

→ {base url}/mgramseva/home/billmanualgenerate.

![](<../../../../.gitbook/assets/image (44).png>)

Users are redirected to this screen if they click on the Generate Demand card on the home screen.

* This will be used in cases when the scheduler is not run (due to technical errors) and GP wants to run manually.

### **Default Values Set**

* The service category displays water charges by default
* The service type displays non-metered connection by default

### **User Interaction on Screen**

* Set the billing year from the drop-down which contains the list of financial years.
* Set the Billing cycle which contains billing cycles for the selected financial year.
* On Click of Generate Demand Button, Bulk Demand is generated and the user is navigated to the success screen.

![](<../../../../.gitbook/assets/image (102).png>)

### **Logic Implemented for Billing Cycles**

* The Billing Cycle drop-down shows a list of months starting from the selected financial year **from Date** month till current date month.
* On selection of the desired month, the billing period value is set from the selected month’s first date to the selected month’s last date. (Eg. Selected Billing Cycle: June 2021, so Billing period: 01/07/2021 - 30/07/2021)

### **Files Path**

Primary Files:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/GenerateBill.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/GenerateBill/GenerateBill.dart)

### **Field Validations**

| **SL** | **Fileds**      | **Validations** |
| ------ | --------------- | --------------- |
| 1      | Billing Year\*  | `isMandatory`   |
| 2      | Billing Cycle\* | `isMandatory`   |

| **API EndPoint**               | **Input Params (Modules)**                                                                                | **Description**                                                                                                                                                                                                                                                                                   |
| ------------------------------ | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `egov-mdms-service/v1/_search` | <p><code>ws-services-masters</code></p><p><code>PropertyTax</code></p><p> <code>BillingService</code></p> | <p>To Fetch the Details of</p><ul><li><code>connectionType</code> from <code>ws-services-masters</code></li><li><code>TaxPeriod</code> from <code>BillingService</code> where <code>service=='WS' &#x26;&#x26; @.fromDate &#x3C;= $datestamp &#x26;&#x26; @.toDate >= $datestamp</code></li></ul> |

### **API Details**

| **SL** | **End Point**                                | **Request Method** | **Request Info**                              |
| ------ | -------------------------------------------- | ------------------ | --------------------------------------------- |
| 1      | `/ws-calculator/waterCalculator/_bulkDemand` | `POST`             | <p>"tenantId": {},<br>"billingPeriod": {}</p> |

#### **Stack**

1 → Home Screen. + Generate Bulk Demand Screen

Pop → Home Screen

Widgets Utilised from Library

| **SL No** | **Widgets**                                                                                                                                                                            | **File Path**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Description**     |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| 1         | <ul><li><code>SelectFieldBuilder</code></li></ul><p><strong>(Primary File)</strong></p><ul><li><code>SearchSelectFieldBuilder</code></li></ul><p><strong>(Secondary File)</strong></p> | <p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p><p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SearchSelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SearchSelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p> | Searchable Dropdown |
| 2         | `CommonSuccessPage`                                                                                                                                                                    | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/CommonSuccessPage.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/CommonSuccessPage.dart)                                                                                                                                                                                                                                                                                                                                  | Success Screen      |
| 3         | `BottomButtonBar`                                                                                                                                                                      | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BottonButtonBar.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/BottonButtonBar.dart)                                                                                                                                                                                                                                                                                                                                      | Button              |

## Bill Generation - Metered

### **Link**

→ {base url}/mgramseva/home/householddetails/billgenerate.

![](<../../../../.gitbook/assets/image (13).png>)

Users are redirected to the Generate New Bill screen if they click the Generate New Bill option in the household detail screen.

### **Default Values Set**

* The service category defaults to water charges
* The service type defaults to metered connection
* The property type defaults to the selected property type of the consumer

### **User Interaction on Screen**

* Previous Meter Reading: Takes input from the user only for first time Bill generation and if the Previous meter reading is null, else it's defaulted if the meter reading is present.
* New Meter Reading: Takes input from the user
* Meter Reading Date: Defaulted to today’s date, the User can change it to the desired date.

### **User Interaction on Bill Generation Success Screen**![](blob:https://digit-discuss.atlassian.net/e0b51049-9047-4cf5-aff1-355c808cead2#media-blob-url=true\&id=93f529e2-0f5b-45fc-a5cd-1b8e9cf857d8\&collection=contentId-1925480514\&contextId=1925480514\&mimeType=image%2Fpng\&name=Bill%20Success.png\&size=48696\&width=378\&height=815\&alt=)

* Users have the option of downloading the bill or sharing it via Whatsapp
* On click of the Collect Payment button, the user is navigated to the Payment Screen

### **Files Path**

Primary Files:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/GenerateBill.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/GenerateBill/GenerateBill.dart)

### **Field Validations**

| **SL** | **Fileds**               | **Validations**                                                                                                                                         |
| ------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Previous Meter Reading\* | <ul><li><code>r'^[0-9]+$'</code></li><li><code>5 - digit reading</code></li><li> <code>if Meter Reading &#x3C; 5 digit, prepend zeroes</code></li></ul> |
| 2      |  New Meter Reading\*     | <ul><li><code>r'^[0-9]+$'</code></li><li><code>5 - digit reading</code></li><li> <code>if Meter Reading &#x3C; 5 digit, prepend zeroes</code></li></ul> |
| 3      | Meter Reading Date\*     | <ul><li> <code>Shows dates till today's date</code></li></ul>                                                                                           |

| **API EndPoint**               | **Input Params (Modules)**                                                                                | **Description**                                                                                                                                                                                                                                                                        |
| ------------------------------ | --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `egov-mdms-service/v1/_search` | <p><code>ws-services-masters</code></p><p><code>PropertyTax</code></p><p> <code>BillingService</code></p> | <p>To Fetch the Details of</p><ul><li><code>connectionType</code> from <code>ws-services-masters</code></li><li><code>PropertyType</code> from <code>PropertyTax</code></li><li><code>TaxHeadMaster</code> from <code>BillingService</code> where <code>service=='WS'</code></li></ul> |

### **API Details**

| **SL** | **End Point**                            | **Request Method** | **Request Info**                                                                                                                                                                                                                                                 |
| ------ | ---------------------------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | `/ws-calculator/meterConnection/_create` | `POST`             | <p>"meterReadings": {<br>"currentReading": {},<br>"currentReadingDate": {},<br>"billingPeriod": {},<br>"meterStatus": "Working",<br>"connectionNo": {},<br>"lastReading": {},<br>"lastReadingDate": {},<br>"generateDemand": true,<br>"tenantId": {}</p><p>}</p> |

#### **Stack**

1 → Home Screen + Household Details Screen + Generate Bill Metered

Pop → Household Details Screen

Widgets Utilised from Library

| **SL No** | **Widgets**                                                                                                                                                                            | **File Path**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | **Description**                   |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| 1         | <ul><li><code>MeterReading</code></li></ul>                                                                                                                                            | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/MeterReading.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/GenerateBill/widgets/MeterReading.dart)                                                                                                                                                                                                                                                                                                                      | Meter Reading 5 digit boxes field |
| 2         | <ul><li><code>SelectFieldBuilder</code></li></ul><p><strong>(Primary File)</strong></p><ul><li><code>SearchSelectFieldBuilder</code></li></ul><p><strong>(Secondary File)</strong></p> | <p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p><p><a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SearchSelectFieldBuilder.dart"><img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SearchSelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva</a></p> | Searchable Drop down              |
| 3         | `DatePickerFieldBulder`                                                                                                                                                                | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/DatePickerFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/DatePickerFieldBuilder.dart)                                                                                                                                                                                                                                                                                                                        | Date Picker                       |
| 4         | `CommonSuccessPage`                                                                                                                                                                    | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/CommonSuccessPage.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/CommonSuccessPage.dart)                                                                                                                                                                                                                                                                                                                                  | Success Screen                    |
| 5         | `BottomButtonBar`                                                                                                                                                                      | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BottonButtonBar.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/BottonButtonBar.dart)                                                                                                                                                                                                                                                                                                                                      | Button                            |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
