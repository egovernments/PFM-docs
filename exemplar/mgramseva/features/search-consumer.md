# Search Consumer

## Overview

The search screen is used to filter the list of consumers based on selected criteria. This is the common search screen for all the transactions such as

1. Collect Payments
2. Download bills and receipts
3. Update consumer information

![Search Consumer](<../../../.gitbook/assets/image (52).png>)

## Search Parameters

The consumer can be searched on the following parameters -

1. **Owner Mobile Number** - Allows search of consumer records that match the entered mobile number.
   1. OLD Mobile Number
   2. NEW Mobile Number
   3. The user is able to search only when he/she enters the full mobile number. A partial mobile number search is not allowed.
2. **Name of Consumer** - Allows search of consumer records that match consumer names with the input text.
   1. OLD Name
   2. New Name
   3. Name search can be done with a partial name also.
3. **Old Connection id** - Allows search of consumer records that matches the old Connection id entered in the search bar.
4. **New Connection id** - Allows search of consumer records that matches the New Connection id entered in the search bar.

![Search Consumer Expanded](<../../../.gitbook/assets/image (11).png>)

{% hint style="info" %}
* As the user starts entering one field, other fields are made non-editable. When the user removes text/numbers entered in the field, other fields are made accessible.
* Show more, Show less expands and contracts the view.
* When the user search matches with only one record, show HH detail screen directly. No need to show the intermediary search details screen.
{% endhint %}

## **Search Result**

![](<../../../.gitbook/assets/image (26).png>)

The search result set contains below information -

1. **Sub-Heading** - Subheading text changes dynamically with the type of search carried out.
   1. Following consumers match search criteria with
      1. Phone Number as +91 - 7731045306
      2. Name as ABCxyZ
2. **New Connection ID**
3. **Old Connection ID**
4. **Consumer’s Name**
5. **Phone Number**
6. **Address** - Combination of Door Number, street number, Ward (if applicable)
7. Click on the **View Consumer Details** button redirects the user to the HH Details screen.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
