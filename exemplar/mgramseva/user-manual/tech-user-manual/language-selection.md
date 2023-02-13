# Language Selection

## **Link**

→ {base url}/mgramseva/selectLanguage

User will be Landed/ Navigated to Language Selection Screen

![](<../../../../.gitbook/assets/image (86).png>)

APP → Initial Screen

### **User Interaction on Screen**

* Users can switch to different languages which the application supports
* Click on [Continue](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1922269219) to navigate to the next screen

### **File Path**

Primary Files[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/languageSelection.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/SelectLanguage/languageSelection.dart)

Secondary Files[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/DesktopView.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/SelectLanguage/DesktopView.dart)[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/MobileView.dart at develop · egovernments/punjab-mgramseva](https://github.com/egovernments/punjab-mgramseva/blob/develop/frontend/mgramseva/lib/screeens/SelectLanguage/MobileView.dart)

### **Data Storage**&#x20;

LocalStorage

| **SL No** | **Key**                     | **Stored Data**                         |
| --------- | --------------------------- | --------------------------------------- |
| 1         | `states_key`                | State Information for From MDMS Service |
| 2.        | ex :`pn_IN`,`en_IN`,`hi_IN` | Localisation codes                      |

## **API Details**

| **API EndPoint**                                                     | **Input Params (Modules)**                                   | **Description**                                                                                                                           |
| -------------------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `egov-mdms-service/v1/_search`                                       | <p><code>common-masters</code></p><p><code>tenant</code></p> | <p>To Fetch the Details</p><p><strong>State Info</strong></p><ul><li>Logo</li><li> background Image</li><li>Languages Supported</li></ul> |
| `localization/messages/v1/_search?module`={}`locale`={}`tenantId`={} | ALL the necessary Modules, with locale key and tenant Id     | To Load the Localised data                                                                                                                |

### **Stack**

0 → Langage Selection Screen

Pop → Application closes

Widgets Utilised from Library

| **SL No** | **Widgets Library** |
| --------- | ------------------- |
| 1         | Button Bar          |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
