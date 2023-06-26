# View Consumer

## Overview

1. Users are redirected to the View Consumer screen from the home screen via
   1. Collect payments → Search Screen → Consumer Details Screen
   2. Download bills & receipts → Search screen → consumer details Screen
   3. Dashboard → Collections → Click on Consumer ID
   4. Household register → Click on Consumer ID
2. This screen contains all information related to HH

Static HH card which displays the following details

1. New Connection ID (also displayed as a heading)
2. Consumer name
3. Father's name
4. Phone number
5. Old connection ID
6. Address - Door Number, Street number, Ward (attached)
7. Property type
8. Service type
   1. for metered connections meter number is also displayed

## **For Non-Metered Connection**

* When Bill is not generated (Post rollout until the first month)
  * Only Data Card is shown - No action required  &#x20;
  * After the first demand is generated - A new consumer bill/Card gets generated with the following data points and actions
    * &#x20;Billing Cycle – the latest billing cycle
      * Amount -&#x20;
        * Current Amount - fixed charges applicable to the billing cycle
        * Arrears - Arrears from the first month. From next month onwards this field will display any unpaid dues.
        * Total Amount - Sum of current amount and arrears
      * Action Items
        * Download, Share Bill
          * Clicking on download bill prompts to download bill (Bill details is given in a separate user story)
          * Share bill (WhatsApp icon) opens sharing options to phone OS and the user is able to share bills via WhatsApp
          * Message to go in WhatsApp “Please find Bill for water charges with Connection ID WS-83121-8312 generated on dd/mm/yyyy” along with bill PDF.
          * Name of the PDF - “Bill ID”
        * Collect Payment
          * Collect payment button takes the revenue collector to the payment collection screen
* After the First payment collection is done
  * A receipt history block is visible only after the first payment transaction is completed through mGramSeva.
    * A list of all the receipts is shown under this section as cards, with different data points as actions. Order of receipts is newest → oldest from top to bottom
    * Each receipt card contains
      * Receipt ID
      * Amount Paid
      * Paid Date
    * Actions
      * Download Receipt - download receipt in Revenue collectors phone as a PDF
        * Name of PDF - “Receipt ID”
      * Share (WhatsApp)
        * Message to go in WhatsApp “Please find the receipt for water charges with Connection ID WS-83121-8312 paid on dd/mm/yyyy” along with receipt PDF



![New Connection Before First Bill Generation](<../../../.gitbook/assets/image (49).png>)

![First bill is generated   Payment Collection is pending](<../../../.gitbook/assets/image (43).png>)

![2 payments are already made](<../../../.gitbook/assets/image (40).png>)

## **For Metered Connection**

1. &#x20;When Bill is not generated (Post rollout until the first month)
   1. Data Card is shown
   2. Below the data card - the Card to generate a new bill is also shown.
   3. This card contains
      1. Last bill generation date - For the first time this will be picked up from data entry. Next time onwards systems latest bill generation date will be captured.
      2. Days from last bill generation Date - this is to indicate revenue collector how many days have passed by since last time bill is generated
      3. Previous Meter reading - Units of the meter that is the last read will be displayed here.
      4. Pending Amount
         1. Before the first bill is generated this will just be arrears that are captured during data entry
         2. After the first bill is generated, this pending amount includes the whole pending amount by the user
      5. Generate a new bill
         1. Clicking on Generate a New Bill initiates bill generation flow for metered connection
      6. Note
         1. Users have to generate a bill to start collecting payments, Without the first generation of bills, collection cant happen even for arrears entered in data entry.
   4. After the first bill is generated
      1. A new consumer bill/Card gets generated with the following data points and actions
         1. Last bill generation date - Date of bill generation
            1. Amount -
               1. Current Amount - Volumetric charges between 2 latest meter readings according to rate master
               2. Arrears - All previously unpaid dues.
            2. Total Amount - Sum of current amount and arrears
         2. Action Items
            1. Download, Share Bill
               1. Clicking on download bill will prompt to download bill for the respective amount (Bill details is given in separate user story)
               2. Share bill (WhatsApp icon) will open sharing options of phone OS and the user should be able to share bill via WhatsApp
               3. Message to go in WhatsApp “ Please find Bill for water charges with Connection ID WS-83121-8312 generated on dd/mm/yyyy” along with bill PDF.
               4. Name of the PDF - “Bill ID”
            2. Collect Payment
               1. Collect payment should take revenue collector to the payment collection screen
   5. After the first payment collection is done
      1. A receipt history block is visible only after the first payment happens through mgramseva.
      2. A list of all the receipts is shown under this section as cards, with different data points as actions. Order of receipts is newest → oldest from top to bottom
      3. Each receipt card contains
         1. Receipt ID
         2. Amount Paid
         3. Paid Date
      4. Actions
         1. Download Receipt - should download receipt in Revenue collectors phone as a PDF
            1. Name of PDF - “Receipt ID”
         2. Share(WhatsApp)
            1. Message to go in WhatsApp “ Please find receipt for water charges with Connection ID WS-83121-8312 paid on dd/mm/yyyy” along with receipt PDF.
   6. If a new bill is generated again by clicking on ‘Generate a new bill’ revenue collector goes through bill generation flow and a new single card appears between ‘Generate bill’ and ‘Consumer receipts block’

![](<../../../.gitbook/assets/image (5) (1).png>)

![](<../../../.gitbook/assets/image (36).png>)

![](<../../../.gitbook/assets/image (23).png>)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
