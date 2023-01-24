# Edit Profile

## **Link**

→ {base url}/mgramseva/home/editProfile

![](<../../../../.gitbook/assets/image (82).png>)

Users are navigated to this screen if they click on the Edit Profile option on the Side Bar app Drawer.![](blob:https://digit-discuss.atlassian.net/6fab3b7c-764f-4cd5-ad69-248197e2873e#media-blob-url=true\&id=2cba3990-808e-45ec-8e26-0681e2361567\&collection=contentId-1925709827\&contextId=1925709827\&mimeType=image%2Fpng\&name=EditProfile.png\&size=28631\&width=377\&height=818\&alt=)

## **User Interaction on Screen**

* User can change their profile name, gender and email on this screen
* Click on the Save button triggers a Details Saved Successfully message on the screen and saves the changes to the profile.

## **File Path**

Primary Files:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/EditProfile.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/Profile/EditProfile.dart)

## **Field Validations**

| **SL** | **Fileds** | **Validations**                                                                                                                                                      |
| ------ | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Name       | `r'^[a-zA-Z ]+$'`                                                                                                                                                    |
| 2      | Email ID   | `r'^$\|^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)\|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])\|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$'` |

## **API Details**

| **SL** | **End Point**           | **Request Method** | **Request Info**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------ | ----------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | `/user/profile/_update` | `POST`             | <p>"user": {<br>"id": {},<br>"userName": {},<br>"salutation": null,<br>"name": {},<br>"gender": {},<br>"mobileNumber": "9191919146",<br>"emailId": {},<br>"altContactNumber": null,<br>"pan": null,<br>"aadhaarNumber": null,<br>"permanentAddress": null,<br>"permanentCity": null,<br>"permanentPinCode": null,<br>"correspondenceAddress": null,<br>"correspondenceCity": null,<br>"correspondencePinCode": null,<br>"active": true,<br>"locale": null,<br>"type": "EMPLOYEE",<br>"accountLocked": false,<br>"accountLockedDate": 0,<br>"fatherOrHusbandName": null,<br>"relationship": null,<br>"signature": null,<br>"bloodGroup": null,<br>"photo": null,<br>"identificationMark": null,<br>"createdBy": {},<br>"lastModifiedBy": {},<br>"tenantId": {},<br>"roles": [ {} ],<br>}</p> |

### **Stack**

1 → Home Screen. + Edit Profile Screen

Pop → Home Screen

Widgets Utilised from Library

| **SL No** | **Widgets**        | **File Path**                                                                                                                                                                                                                                                                             | **Description**           |
| --------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| 1         | `BuildTextField`   | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart)               | Text Field                |
| 2         | `BottomButtonBar`  | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/BottonButtonBar.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/BottonButtonBar.dart)                 | Button                    |
| 3         | `RadioButtonField` | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/RadioButtonFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/RadioButtonFieldBuilder.dart) | Radio Buttons for options |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
