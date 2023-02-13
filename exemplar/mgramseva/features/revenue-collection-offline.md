# Revenue Collection - Offline

![](<../../../.gitbook/assets/image (39).png>)

After the demand is generated for Metered and non-metered connections Revenue collectors come to this screen to collect payments.

1. Users can see the consumer billing information on the screen
2. Clicking on View Details expands the card and shows more details. Clicking on the Hide Details collapses the card to show only connection ID, Consumer Name & Total Due Amount.
3. Payment amount - can either pay
   1. The full amount, or
   2. Custom amount - Users can enter the custom amount in the input field - this cannot be zero or greater than the total due amount.
4. Payment methods
   1. Cash - select cash and proceed to payment takes the user to the successful collection screen
   2. Online - The online payment option displays a Q/R code on the user screen that can be scanned by another phone to pay the due.
   3. Post payment via any mode - payment success screen is shown
   4. Receipt ID format - RB-dd/mm/yyyy-yy/running\_sequence\_number
5. User Actions
   1. Download receipt - download PDF version of receipt with receipt ID as the name of PDF while downloading
   2. Share receipt via WhatsApp - opens the Phone OS sharing options
   3. back to home - takes the user back to the home screen
6. SMS to HH
   1. As soon as the amount is paid and the Revenue collector reaches the Payment success screen SMS is sent to HH.
      1. SMS 1 - Dear ‘Username’, Paid Rs.X for water charges for bill period \<Cycle>. Download receipt \<link>
      2. SMS 2 - Dear ‘Username’, Please leave a review on water supply at \<GP> at \<Link>
      3. HH is able to leave a review for water charges. Refer [Feedback - Post Payments](feedback-post-payment.md). &#x20;

Details on the card

| **Detail**       | **Comments**                                                                                                                                                                                                                                                    |                                                                                                                               |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Connection ID    | New Connection ID will be displayed here                                                                                                                                                                                                                        |                                                                                                                               |
| Consumer Name    | Consumer Name (Should take updated consumer name)                                                                                                                                                                                                               |                                                                                                                               |
| Bill ID number   | ID of the Bill                                                                                                                                                                                                                                                  |                                                                                                                               |
| Bill period      | <p>for non-metered connections</p><ol><li>This is the latest billing cycle for which demand is generated</li></ol><p>For metered connections</p><ol><li>This is the new bill generated from the meter reading between the 2 most recent billing dates</li></ol> | <p>Format</p><ol><li>Month &#x3C;space> Financial Year</li><li>Previous meter reading date - New meter reading date</li></ol> |
| Water charges    | Amount for the latest billing cycle                                                                                                                                                                                                                             | For metered, calculate charges as per rate master between the latest 2 billing dates                                          |
| Arrears          | All old arrears accumulated for HH                                                                                                                                                                                                                              | Expansion should breakup of arrears by individual billing cycles/bill generation dates                                        |
| Total Due amount | Net amount consumer has to pay                                                                                                                                                                                                                                  |                                                                                                                               |

![](<../../../.gitbook/assets/image (50).png>)

![](<../../../.gitbook/assets/image (20).png>)

1. When online is selected for payment method, the “Collect Payment” option is disabled. Since HH scans the QR, the Revenue collector does not have control over the online process.
2. A partial amount can’t be greater than the full amount.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
