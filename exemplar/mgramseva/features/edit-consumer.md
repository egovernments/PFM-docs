# Edit Consumer

## Overview

Consumer information can be edited under certain conditions -

1. Before the first demand is generated from the system
2. After the first demand is generated from the system

![](<../../../.gitbook/assets/image (35).png>)

## Edit Screen

1. Users with permissions to edit consumer records can click on the **Edit Consumer** info tile on the home screen. This navigates them to the consumer search screen.
2. Users can navigate from the search screen or the search results screen (Case when multiple search results are displayed) to the Consumer Edit Screen.
3. On the successful load of the consumer edit screen, all data parameters of the consumer are shown (with editable and non-editable fields).
4. By Default - New consumer ID is shown on the top of the screen and is non-editable.&#x20;

The table below lists the editable field details -

| **Data Field**              | **Before First Demand** | **After First Demand** | **Comments**                                                                                                                                                                                                                                                                  |
| --------------------------- | ----------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| New Consumer ID             | NO                      | NO                     | Consumer ID is generated while user creation and is not editable                                                                                                                                                                                                              |
| Consumer’s Name             | YES                     | YES                    | bills, receipts, bill generation screens etc starts displaying the newly entered consumer name                                                                                                                                                                                |
| Gender                      | YES                     | YES                    |                                                                                                                                                                                                                                                                               |
| Father’s Name               | YES                     | YES                    |                                                                                                                                                                                                                                                                               |
| Phone number                | YES                     | YES                    | <p>Use Cases</p><ol><li>After the phone number is changed, searching with the old/new phone number in the connection search screen leads to the same HH screen</li><li>SMS notifications are sent to the new mobile number of the user from the date of the change </li></ol> |
| Old Connection ID           | YES                     | NO                     | Validated for unique IDs in the system for the GPWSC                                                                                                                                                                                                                          |
| Door Number                 | YES                     | YES                    |                                                                                                                                                                                                                                                                               |
| Street Number / Name        | YES                     | YES                    |                                                                                                                                                                                                                                                                               |
| Ward Number / Name          | YES                     | YES                    |                                                                                                                                                                                                                                                                               |
| Gram Panchayat Name         | NO                      | NO                     |                                                                                                                                                                                                                                                                               |
| Property Type               | YES                     | YES                    | Charges applicable as per rate master. Effects take place from the next billing cycle                                                                                                                                                                                         |
| Service Type                | YES                     | YES                    | <ul><li>Effects take place from the next billing cycle</li><li>The last date of the current billing cycle is taken as the last meter reading date</li><li>Previous meter reading is captured while generating the demand</li></ul>                                            |
| Meter Number                | YES                     | YES                    |                                                                                                                                                                                                                                                                               |
| Previous meter reading Date | YES                     | NA                     | This field is not shown on screen after the first demand is generated                                                                                                                                                                                                         |
| Previous Meter Reading      | YES                     | NA                     | This field is not shown on the screen after the first demand is generated                                                                                                                                                                                                     |
| Last Billing Cycle Billed   | YES                     | NA                     | This field is not shown on the screen after the first demand is generated                                                                                                                                                                                                     |
| Arrears as of Last Bill     | YES                     | NA                     | This field is not shown on the screen after the first demand is generated. When changed the arrear demand is deleted and updated accordingly based on the selected service type.                                                                                              |
| Mark Connection as inactive | YES                     | YES                    | <p> If a connection is marked inactive, it is not considered for demand generation for future billing cycles.</p><p>An inactive connection can be reactivated later from this screen.</p>                                                                                     |

## Edit Options

1. In case there are arrears, demand is generated. If there are no arrears, demand is not generated.
2. Users can modify the arrear value. In such a case, demand is generated with the updated value.
3. Users can add arrear to the connection, for which arrear was zero at the time of creating the connection. In this case, the new demand is generated.

Clicking on the Submit button shows a nudge saying **Details Submitted Successfully**. Closing the nudge navigates the user back to the home screen.

The CTA is activated only when any field is changed or updated. Else, it is in an inactive state.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
