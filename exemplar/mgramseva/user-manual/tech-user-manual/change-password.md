# Change Password

## **Link**&#x20;

→ {base url}/mgramseva/home/changepassword.

![](<../../../../.gitbook/assets/image (60).png>)

Users are redirected to this screen if they click on the Change Password option in the Side Bar app Drawer.![](blob:https://digit-discuss.atlassian.net/ab0d2124-264f-4e7e-825a-6da61e034076#media-blob-url=true\&id=b1d71015-4630-47b9-a673-6bc5b8c40589\&collection=contentId-1925546002\&contextId=1925546002\&mimeType=image%2Fpng\&name=ChangePassword.png\&size=40193\&width=377\&height=813\&alt=)

## **User Interaction on Screen**

* Enter the Current Password
* Enter and Confirm a New Password to set the login credentials for next time login
* Click the Change Password Button. The user login password is set to the new password.

## **Password Hint Card**

* This feature helps match the user password to the requirements and checks if the password contains
  * Minimum 6 digits
  * At least one special character ( !#$%^&...)
  * At least one letter
  * Atleast one number

## **File Path**

Primary Files:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Changepassword.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/ChangePassword/Changepassword.dart)

## **Field Validations**

| **SL** | **Fileds**             | **Validations**                                            |
| ------ | ---------------------- | ---------------------------------------------------------- |
| 1      | Current Password\*     | No Validation                                              |
| 2      | Set a New Password\*   | `r'^(?=.*?[A-Za-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{6,}$'` |
| 3      | Confirm New Password\* | Match with New Password                                    |

## **API Details**

| **SL** | **End Point**           | **Request Method** | **Request Info**                                                                                         |
| ------ | ----------------------- | ------------------ | -------------------------------------------------------------------------------------------------------- |
| 1      | `user/password/_update` | `POST`             | <p>"userName": {},<br>"existingPassword": {},<br>"newPassword": {},<br>"tenantId": {},<br>"type": {}</p> |

### **Stack**

1 → Home Screen. + Change Password Screen

Pop → Home Screen

Widgets Utilised from Library

| **SL No** | **Widgets**      | **File Path**                                                                                                                                                                                                                                                               | **Description** |
| --------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| 1         | `BuildTextField` | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart) | Text Field      |
| 2         | `Button`         | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Button.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/Button.dart)                     | Button          |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
