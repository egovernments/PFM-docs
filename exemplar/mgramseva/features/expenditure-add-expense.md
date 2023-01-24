# Expenditure - Add Expense

The expense entry for the O\&M on regular basis is captured on this screen.

![](<../../../.gitbook/assets/image (72).png>)

On selecting the option “Add Expense Record” from the list of tile/cards on the home page, the user is navigated to the expense entry screen. The screen displays the following fields.

| **Field Name**   | **Type**                         | **Mandatory Y/N** | **Description**                                                                                                                                     |
| ---------------- | -------------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Vendor Name      | Text (With Suggestions dropdown) | Y                 | Name of the Vendor. The suggestion list is shown as the user entry is done for every character. The new Name will also create a Vendor Register.    |
| Type of Expense  | Drop Down                        | Y                 | Type of expense list From Master                                                                                                                    |
| Amount           | Numeric                          | Y                 | Expense amount for the Bill                                                                                                                         |
| Bill Date        | Date                             | Y                 | Date on which the bill is to be recorded in the registers. Validation - Before Current Date and after party Bill Date.                              |
| Party Bill Date  | Date                             | N                 | Date on which the Party/vendor bill was issued. Validation - Before the Bill Date.                                                                  |
| Bill Paid        | Radio Buttons                    | N                 | With option Yes/No. To update status if it is paid. If yes, “Paid Date” is captured.                                                                |
| Paid Date        | Date                             | N                 | Date on which the bill is paid. Displayed if the Bill paid option is selected as “Yes”. Validation - After Bill date and less than current Date.    |
| Attach Documents | Doc Attachments                  | N                 | Option to upload documents (Max of 5). Supported files - PDF, JPEG, PNG. Should show required validation for other types of files.                  |
| Submit           | Button                           | -                 | On click, the consumer master gets created with the detail entered above. The new connection id also should get generated as per the configuration. |

On Submitting, the Expense entry gets created with a Bill number assigned. The Bill number generated would be based on logic defined as - “EB-\<FY>-<4 digit running seq No>”

On Successful creation of expense entry, an acknowledgement screen is shown “Expense Entry successful” along with the Bill Number.&#x20;

![](<../../../.gitbook/assets/image (43).png>)



| **Expenditure Entry** | **Expenditure entry Successful** |   |
| --------------------- | -------------------------------- | - |
|                       |                                  |   |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
