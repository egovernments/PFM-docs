# Search Connection

## **Link**&#x20;

→ {base url}/mgramseva/home/householdSearch?Mode=collect

&#x20;→ {base url}/mgramseva/home/consumersearchupdate?Mode=update

&#x20;→ {base url}/mgramseva/home/householdReceiptsSearch?Mode=receipts

![](<../../../../.gitbook/assets/image (84).png>)

Users are redirected to this screen once they click on the Collect Payment Card or the Update Consumer Details Card or Download Bills and Receipts Card on Home Screen.![](blob:https://digit-discuss.atlassian.net/23527a1c-0ba9-4b83-9c8f-ae1824f6554a#media-blob-url=true\&id=22a4929f-89bc-480a-a918-c5a4e85188ab\&collection=contentId-1925316787\&contextId=1925316787\&mimeType=image%2Fpng\&name=Search%20Connection.png\&size=43384\&width=380\&height=814\&alt=)

## **User Interaction on Screen**

* Users can search the consumer/connection with their Mobile Number / Name / Old Connection ID / New Connection ID ( `Search with any one of these`)
* Click on Search to get the household details of the Consumer/Connection

## **Files Path**

Primary Files:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/SearchConnection.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/ConnectionResults/SearchConnection.dart)

## **Field Validations**

| **SL** | **Fileds**           | **Validations**            |
| ------ | -------------------- | -------------------------- |
| 1      | Owner Mobile Number  | `r'^(?:[+0]9)?[0-9]{10}$'` |
| 2      | Name of the Consumer | `r'^[A-Za-z ]'`            |
| 3      | Old Connection ID    | `No Validation`            |
| 4      | New Connection ID    | `No Validation`            |

## **API Details**

| **SL** | **End Point**             | **Request Method** | **Request Info**                                                                                                   |
| ------ | ------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------ |
| 1      | `/ws-services/wc/_search` | `POST`             | <p>tenantId: {}</p><p>oldConnectionNumber: {}</p><p>name: {}</p><p>connectionNumber: {}</p><p>mobileNumber: {}</p> |

### Stack

1 → Home Screen. + Search Connection Screen

Pop → Home Screen

Widgets Utilised from Library

| **SL No** | **Widgets**       | **File Path**                                                                                                                                                                                                                                                               | **Description** |
| --------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| 1         | `BuildTextField`  | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart) | Text Field      |
| 2         | `BottomButtonBar` | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BottonButtonBar.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/BottonButtonBar.dart)   | Button          |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
