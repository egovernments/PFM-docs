# Collect Payment

## **Link**

&#x20;→ {base url}/mgramseva/household/details/collectPayment![](blob:https://digit-discuss.atlassian.net/7b871954-91b9-47a8-8250-33a09a1908c8#media-blob-url=true\&id=91260146-5080-4158-83af-bae678dca7f3\&collection=contentId-1928200243\&contextId=1928200243\&mimeType=image%2Fpng\&name=Collect%20Payment%20Areears.png\&size=46493\&width=373\&height=812\&alt=)

![](<../../../../.gitbook/assets/image (96).png>)

After the demand is generated for Metered and non-metered connections or if any arrears are present, the Revenue collector uses this screen to collect payments. &#x20;

Collect Payment card is available on the home screen to the user role having `COLLECTION_OPERATOR` permission.

## **User Interaction on Screen**

* Users can pay the total due amount by selecting the Full Amount option below Payment Amount.
* Or, Users can also pay a partial amount by selecting Partial Amount from the Payment Amount options. If Partial Amount is selected, users have to provide the amount that he wants to pay.
* Clicking on Collect Payment navigates the user to the Payment Success screen. The user can download the receipt or share the receipt for the collected amount.
* Users can also print mini receipts with the help of Bluetooth thermal printers by selecting the [Print mini receipt](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2053210133) option.

## **Logic Implemented for Arrears Breakup**![](blob:https://digit-discuss.atlassian.net/5555ede1-7e6c-4048-9b53-12270099c765#media-blob-url=true\&id=be8bc96e-4523-4574-b3cc-b4d8473e642e\&collection=contentId-1928200243\&contextId=1928200243\&mimeType=image%2Fpng\&name=Payment%20Success.png\&size=40449\&width=374\&height=636\&alt=)

The Arrears is broken into 'BL\_(TaxHeadCode)' which we get from Bill details-->Bill Account details ---> Tax Head Code and the amount of particular arrears is similar to the Bill details--> amount from the Fetch Bill API.

![](<../../../../.gitbook/assets/image (70).png>)

(`Eg. if there are two bills with tax head codes is 10101 and 10102, then Arrears break up is represented as BL_10101(Water Charges) with the corresponding amount and BL_10102(Water Charges-Arrears) with the corresponding amount`)

## **Files Path**

Primary Files:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/collect\_payment.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/common/collect\_payment.dart)

## **Field Validations**

| **Fields**                                       | **Validations**                                          |
| ------------------------------------------------ | -------------------------------------------------------- |
| Payment Amount : Full Amount or Partial Amount   | None                                                     |
| Partial Amount (`If Partial Amount is selected`) | `r'^[0-9]+$' , Can not be 0 or greater than Full Amount` |
| Payment Method                                   | None                                                     |

## **API Details**

| **API EndPoint**                     | **Input Params (Modules)**                                                                                     | **Description**                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `egov-mdms-service/v1/_search`       |  `[{"moduleName":"BillingService","masterDetails":[{"name":"BusinessService","filter":"[?(@.code=='WS')]"}]}]` | To get the billGeneiURL, Calculation of Water services and collectionModesNotAllowed |
| `billing-service/bill/v2/_fetchbill` | <p><code>consumerCode : {}</code></p><p><code>businessService : WS</code></p><p><code>tenantId : {}</code></p> | To fetch the bills of the connection/Consumer                                        |

### Stack

1 → Home Screen. + Search Connection Screen + Household Results + Household Details Screen + Collect Payment Screen

Pop → Household Details Screen

Widgets Utilised from Library

| **Widgets**        | **File Path**                                                                                                                                                                                                                                                                             | **Description**           |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `BuildTextField`   | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)               | Text Field                |
| `BottomButtonBar`  | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BottonButtonBar.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/BottonButtonBar.dart)                 | Button                    |
| `RadioButtonField` | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/RadioButtonFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/RadioButtonFieldBuilder.dart) | Radio Buttons for options |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
