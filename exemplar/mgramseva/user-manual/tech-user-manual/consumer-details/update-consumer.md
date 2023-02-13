# Update Consumer

Enables employees to update consumer details.

![](<../../../../../.gitbook/assets/image (79).png>)

Users are redirected to this screen/page when they click on the Update Consumer Details card

![](<../../../../../.gitbook/assets/image (69).png>)

## **Link**&#x20;

→ {base url}/mgramseva/home/consumersearchupdate?Mode=update

&#x20;→ {base url}/mgramseva/home/consumersearchresult

It redirects to [Search Connection](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1925316787) Page in `update` mode where users enter specific consumer details to search for consumers. The search result screen has the Edit Consumer button. Clicking on this button navigates the users to the Update Consumer screen.

## **Field Validations**

| **Fields**             | **Validations** |
| ---------------------- | --------------- |
| consumer Name\*        | `[A-Za-z ]`     |
| Gender\*               | None            |
| Spouse/Parent’s Name\* | `[A-Za-z ]`     |
| Phone Number\*         | `[0-9]`         |
| Old Connection No      | None            |
| Door Number            | None            |
| Street Name/Number     | None            |
| Gram Panchayat Name\*  | None- Disabled  |
| Property Type\*        | None            |
| Service Type\*         | None            |
| Meter Id               | `[a-zA-Z0-9]`   |
| Meter Reading          | `[0-9]`         |
| Billing Cycle          | None            |
| Arrears                | `[0-9.]`        |

{% hint style="info" %}
**Note**: All fields are validated on Submit apart from the phone number which gets validated on change.
{% endhint %}

## **API Details**

| **API**                                         | **Params**                                                                                                                                                                                                                                                                                                                | **Description**                                                                     |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `/egov-mdms-service/v1/_search`                 | `[{"moduleName":"ws-services-masters","masterDetails":[{"name":"connectionType"}]},{"moduleName":"PropertyTax","masterDetails":[{"name":"PropertyType"}]},{"moduleName":"BillingService","masterDetails":[{"name":"TaxPeriod","filter":"[?(@.service=='WS' && @.fromDate <= 1631989800000 && @.toDate >= 1631989800000)]` | To get the Property Type and service Type and billing cycle values for the Dropdown |
| `egov-location/location/v11/boundarys/_search?` | `hierarchyTypeCode=REVENUE&boundaryType=Locality&tenantId={tenantID}`                                                                                                                                                                                                                                                     | To get the values for Locality DropDow                                              |
| `billing-service/demand/_search`                | `consumerCode`, `businessService`, `tenantId`                                                                                                                                                                                                                                                                             | To Fetch Demand Details                                                             |
| `property-services/property/_search`            | `propertyIds`, `tenantId`                                                                                                                                                                                                                                                                                                 | To Fetch Property Type                                                              |
| `ws-services/wc/_search`                        | `connectionNumber`, `tenantId`                                                                                                                                                                                                                                                                                            | On Demand this API is Made                                                          |

Components utilised from **Widgets Library**

| **Components**            | **File Path**                                                                                                                                                                                                                                                                               |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TextField Builder         | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)                 |
| RadioButtonField Builder  | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/RadioButtonFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/RadioButtonFieldBuilder.dart)   |
| SearchSelectField Builder | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SearchSelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SearchSelectFieldBuilder.dart) |
| DatePicker Builder        | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/DatePickerFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/DatePickerFieldBuilder.dart)     |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
