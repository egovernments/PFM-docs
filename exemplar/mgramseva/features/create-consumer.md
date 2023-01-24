# Create Consumer

## Overview

The household masters need to be created in the system to initiate the demand generation and collection process. These are consumers also referred to as the household that will be issued the water connection and supplied on regular basis.

![Non Metered Connection](<../../../.gitbook/assets/image (6).png>)

On selecting the option Create consumer from the list of tile/cards on the home page, the user is navigated to the Create Consumer page.&#x20;

Data elements for the consumer listed in the table below -

| **Field Name**              | **Type**        | **Mandatory Y/N** | **Description**                                                                                                                                                                                                                          |
| --------------------------- | --------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Consumer’s Name             | Text            | Y                 | Name of the household or connection owner.                                                                                                                                                                                               |
| Gender                      | Radio           | Y                 | Male, Female, Transgender                                                                                                                                                                                                                |
| Father's Name               | Text            | Y                 | Name of the father of the owner                                                                                                                                                                                                          |
| Mobile Number               | Numeric         | Y                 | Mobile number for the consumer                                                                                                                                                                                                           |
| Old Connection id           | Alpha Numeric   | Y                 | Old connection id or ref number for reference                                                                                                                                                                                            |
| Door Number                 | Alpha Numeric   | N                 | Address details with door number for the connection                                                                                                                                                                                      |
| Street No/Street Name       | Alpha Numeric   | N                 | Street number or name of the house for the connection                                                                                                                                                                                    |
| Ward                        | Drop Down       | Y                 | <ul><li>For a tenant which has a single ward, the ward field is not shown</li><li>For a tenant which has multiple wards, the ward field is shown as a single select dropdown</li></ul>                                                   |
| Gram Panchayat              | Display         | -                 | For info. the GP or tenant in which the connection master is created.                                                                                                                                                                    |
| Property Type               | Drop Down       | Y                 | Dropdown with the list of property types from Master ( Ex - Residential, Commercial, Mixed, etc)                                                                                                                                         |
| Service Type                | Drop Down       | Y                 | Dropdown with the list of service types from Master (Ex - Metered, Non-metered)                                                                                                                                                          |
| Meter Number                | Alpha - Numeric | Y                 | **Only for Metered connections -** Meter number will be attached to consumer respectively                                                                                                                                                |
| Previous meter reading date | Date selection  | Y                 | **Only for Metered connections -** This field is used to tag arrears to a demand. Less than current Date.                                                                                                                                |
| Previous meter reading      | Numeric         | Y                 | **Only for Metered connections -** This field is used to attach arrears to a demand.                                                                                                                                                     |
| Last Billing Cycle Billed   | Drop Down       | Y                 | **Only for Non-metered connections -** Dropdown with the list of Billing Cycles prior to the current cycle. This field is used to specify the arrears or total outstanding as of the billing cycle.                                      |
| Arrears as of Last Bill     | Numeric         | Y                 | <p>Arrears as of date - This will be considered for the first Demand/Bill generation as total outstanding or arrears as of the billing period mentioned.</p><p>If no arrears are present to a HH, '0' has to be entered by the user.</p> |
| Submit                      | Button          | -                 | On click of Submit button, the consumer master is created with the detail entered above. The new connection id is also generated as per the configuration.                                                                               |

{% hint style="info" %}
* Multiple connections (HH records) can be created with the same phone number.
  * Phone numbers can be the same, but the old connection ID should be different to create a new HH record.
* A single HH record, can't be registered in the system more than once. Trying to register on the system again displays the error message “this connection already exists”.
{% endhint %}

## Additional Notes and Validation

* On Submit, the consumer master is created and the new consumer id is assigned to the master. The consumer id generated is based on logic defined as - “WS-\<GP id>-<4 digit running seq No>”
* If the connection id already exists,  an error message is shown accordingly.
* On first time/new load, all data entry fields and dropdowns are empty (since there are no records prefilled except for the default fields).
* SMS is not sent to any user upon consumer (HH) creation.
* Submit is disabled until all mandatory fields are entered. Once all inputs are made, the button is enabled.
* Arrears demand :
  * Metered - The arrear demand for the period is created, where the From date is counted as the start of the Financial year and the To date as the period mentioned in the screen.
  * Non metered - The arrear demand is created for the selected billing cycle.

## **Successful Actions**

1. On the successful creation of consumer records, a toast message “ Registration successful” is shown.
2. Closing this toast message, using the close icon, refreshes the page and the user sees an empty consumer creation screen.

| **Consumer creation - non metered** | **Consumer creation - metered** |
| ----------------------------------- | ------------------------------- |
|                                     |                                 |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
