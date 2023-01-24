# Billing - Metered Connection

Unlike Non-Metered connections which have a billing cycle for demand & bills generated automatically, a metered connection needs more inputs, which helps in volumetric billing.

A revenue collector can see a CTA to “Generate a new Bill” on the HH details screen.

1. Clicking on “Generate a new Bill” takes users to the bill generation screen where new meter reading details are entered
2. Field on bill generation screen for metered connections are displayed in the table below
3. Clicking on “Generate bill” takes the user to the bill generation successful screen
4. Logic for Bill ID number - “RB - dd/mm/yyyy-yy/running\_sequence\_number”
5. On the success screen there are 3 user actions
   1. Download bill - Download bill as PDF (name of PDF is always the Bill ID by default)
   2. Share bill on WhatsApp - Share bill as PDF on WhatsApp
   3. Collect Payment - navigates the revenue collector to the payment collection screen
6.  Share on WhatsApp opens the WhatsApp share popup with the option to choose contacts/groups. The bill is shared with the below text and attached PDF details -

    Text “ Dear \<ConsumerName>, Please find water bill for billing cycle \<Cycle> attached as PDF”

| **Input Metric**       | ****                                                                                              | Comments                                                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Previous Meter reading | Only for first-time bill generation                                                               |                                                                                                                        |
| New meter reading      | For the first time and all consecutive bill generations                                           | Previous meter reading units and previous meter reading dates will be taken from the last bill for new bill generation |
| Meter reading date     | The default is the current date. Revenue collectors can change it to a previous date if required. |                                                                                                                        |

For Demand Generation Logic refer to [Demand/Bill Generation for metered connection](demand-bill-generation-for-metered-connection.md)

![Bill Generation screen for Metered connections](<../../../.gitbook/assets/image (22).png>)



![ Bill Generation Successful](<../../../.gitbook/assets/image (87).png>)

1. All 5 Digits in the meter reading has to be entered. Show error message “ Old Meter Reading entered is Invalid”, “ New Meter Reading entered is invalid” respectively.
2. The New Meter reading should be greater than the Old Meter Reading.
3. The meter reading date is by default set to \<today's date> but give the option to change to the user.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
