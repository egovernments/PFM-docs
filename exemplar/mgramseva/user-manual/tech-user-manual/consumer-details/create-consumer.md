# Create Consumer

Enables employees to create new Consumers or Connections - The process of onboarding the end-users.

## **Link**

→ {base url}/mgramseva/home/consumercreate

![](<../../../../../.gitbook/assets/image (72).png>)

The Create Consumer card is available on the home screen as per the defined user role.

Click on the Consumer Create card navigates the user to the consumer creation screen.

Users enter the required details for the creation of Consumer.

If a user logs in for the first time then a walkthrough is populated following the same logic as in the home screen.

## File Path

Primary Files -[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/WalkFlowContainer.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/ConsumerDetails/ConsumerDetailsWalkThrough/WalkFlowContainer.dart) ,[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/walkthrough.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/ConsumerDetails/ConsumerDetailsWalkThrough/walkthrough.dart)

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
| Propert Type\*         | None            |
| Service Type\*         | None            |
| Meter Id               | `[a-zA-Z0-9]`   |
| Meter Reading          | `[0-9]`         |
| Billing Cycle          | None            |
| Arrears                | `[0-9.]`        |

{% hint style="info" %}
**Note**: All fields are validated on Submit except the Phone number which gets validated on change.
{% endhint %}

## **API details**

| **API**                                         | **Params**                                                                                                                                                                                                                                                                                                                | **Description**                                                                     |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `/egov-mdms-service/v1/_search`                 | `[{"moduleName":"ws-services-masters","masterDetails":[{"name":"connectionType"}]},{"moduleName":"PropertyTax","masterDetails":[{"name":"PropertyType"}]},{"moduleName":"BillingService","masterDetails":[{"name":"TaxPeriod","filter":"[?(@.service=='WS' && @.fromDate <= 1631989800000 && @.toDate >= 1631989800000)]` | To get the Property Type and service Type and billing cycle values for the Dropdown |
| `egov-location/location/v11/boundarys/_search?` | `hierarchyTypeCode=REVENUE&boundaryType=Locality&tenantId={tenantID}`                                                                                                                                                                                                                                                     | To get the values for Locality DropDow                                              |

Consumer creation involves 2 sequential Process

1. Property Creation
2. Water connection Creation

After creating a property, the Property ID is linked to the WaterConnection Request JSON.

Water connection creation is of two types:

A metered connection that requires Meter ID and meter installation Date/ Last Meter Reading Date and an optional field to capture meter reading**.**

![](<../../../../../.gitbook/assets/image (80).png>)

Non-Metered Connection which requires the last billing cycle as mandatory params captured in the field as shown below.

![](<../../../../../.gitbook/assets/image (85).png>)

&#x20;Users can switch between connection types by selecting a desired value from the **Service Type** DropDown.

![](<../../../../../.gitbook/assets/image (62).png>)

| **API**                              | **Description**                                                                                                                                                                                                                                                                                                                        |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `property-services/property/_create` | <p>Property Creation Request JSON</p><p>defined in<a href="https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/connection/property.dart"> <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/property.dart at develop · egovernments/punjab-mgramseva</a></p> |
| `ws-services/wc/_create`             | Water Connection Request JSON defined in[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/water\_connection.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/connection/water\_connection.dart)        |

## &#x20;**Role Access Mapping**

```
    case Routes.CONSUMER_CREATE:
        return ['GP_ADMIN', 'SUPERUSER'];
```

Components utilised from **Widgets Library**

| **Components**            | **File Path**                                                                                                                                                                                                                                                                               |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TextField Builder         | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)                 |
| RadioButtonField Builder  | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/RadioButtonFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/RadioButtonFieldBuilder.dart)   |
| SearchSelectField Builder | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SearchSelectFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/SearchSelectFieldBuilder.dart) |
| DatePicker Builder        | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/DatePickerFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/DatePickerFieldBuilder.dart)     |

## **Files Path**

Model →[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/property.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/connection/property.dart) ,[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/water\_connection.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/model/connection/water\_connection.dart)

View →[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/ConsumerDetails.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/ConsumerDetails/ConsumerDetails.dart)

Controller →[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/consumer\_details\_repo.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/repository/consumer\_details\_repo.dart) ,[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/consumer\_details\_provider.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/providers/consumer\_details\_provider.dart)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
