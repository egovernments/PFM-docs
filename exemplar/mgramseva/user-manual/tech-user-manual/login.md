# Login

## **Link**

→ {base url}/mgramseva/selectLanguage/login

![](<../../../../.gitbook/assets/image (61).png>)

Users are redirected to this screen once they select the preferred language in the previous screen

## **User Interaction on Screen**

* Users enter the registered Phone Number and Password.
* Click on Continue.
* First-time login users navigate to Reset Password Page.

**Log in with the default password**

YES → [Reset Password/ Update Password Screen](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1922662535)

NO → [Home Screen](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1923416085)

## **Files Path**

Primary Files[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Login.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/Login/Login.dart)

## **Field Validations**

| **SL** | **Fileds**     | **Validations**                                            |
| ------ | -------------- | ---------------------------------------------------------- |
| 1      | Phone Number\* | `r'^[0-9]+$'`                                              |
| 2      | Password\*     | `r'^(?=.*?[A-Za-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{6,}$'` |

## API details

| **SL** | **End Point**       | **Request Method** | **Request Info**                                                                                                               |
| ------ | ------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| 1      | `/user/oauth/token` | `POST`             | <p>username: {}</p><p>password:{}</p><p>scope: read</p><p>grant_type: password</p><p>tenantId: {}</p><p>userType: EMPLOYEE</p> |

### **Stack**

1 → Language Selection Screen. + Login Screen.

Pop → Language Selection Screen.

Widgets Utilised from Library

| **SL No** | **Widgets**      | **File Path**                                                                                                                                                                                                                                                               | **Description** |
| --------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| 1         | `BuildTextField` | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/TextFieldBuilder.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/TextFieldBuilder.dart) | Text Field      |
| 2         | `Button`         | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/Button.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/widgets/Button.dart)                     | Button          |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
