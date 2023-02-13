---
description: iFix specification details
---

# Specification

## Overview

iFix is a fiscal data exchange platform that enables the exchange of standardized fiscal data between various agencies. iFix is designed to enable the exchange of fiscal data between various agencies and ensure the visibility of fiscal data. iFix makes it possible to chain the fiscal data with each other and establish a chain of custody for the entire lifecycle from budgeting to accounting.

From the iFIX perspective, there are two types of agencies&#x20;

1. Fiscal Data Provider - posts the fiscal data into iFix using well-defined formats.
2. Fiscal Data Consumer - can query the fiscal data.&#x20;

Both these roles are interchangeable.

## **Registration**

Providers and consumers need to register on iFix before they can post or query fiscal data. To register the concerned person from the agency must be provided with the following information on the iFix portal - Name of the Agency, Contact Person, Name, Contact Person’s Phone Number, and Contact Person’s Official Email Address. The OTP sent to the email address for the person should be used to register.

### **System Registration & Access Key Generation**

Registered users -

* logs in to the iFix portal using the official email address&#x20;
* registers one or more systems as a provider or consumer or both&#x20;
* provides the name of the system
* a unique ID is generated for each system (example: mgramseva@punjab.ifix.org)
* a secret API key is also generated for each system - use this key to post or query fiscal data&#x20;
* The API key can be regenerated if required - only one API key is active at a given point in time

The portal provides the ability to generate new keys for each system.

## **Posting**&#x20;

Fiscal data providers post the fiscal data in two ways.&#x20;

* A fiscal message - is directed to a specific consumer and is delivered to intended consumers. These messages are available for query by intended consumers only.&#x20;
* A fiscal event - iFix stores the events for consumers to query

_Fiscal Event_ consists of&#x20;

* Header&#x20;
  1. From&#x20;
  2. To&#x20;
  3. Date of Posting&#x20;
* Body&#x20;
  1. Fiscal Event Type e.g. Revenue, Expenditure, Debt&#x20;
  2. Fiscal Event Subtype&#x20;
     * Revenue - Estimate, Plan, Demand, Receipt, Credit&#x20;
     * Expenditure - Estimate, Plan, Bill, Payment, Debit&#x20;
     * Debt - in progress - will be provided later.&#x20;
  3. Array of fiscal line items&#x20;
     * Amount&#x20;
     * CoA&#x20;
     * Location Code - from Location Registry&#x20;
     * Program Code - from Program Registry&#x20;
     * Project Code - from Project Registry&#x20;
     * Administrative Hierarchy Code from Administrative Hierarchy Registry&#x20;
     * Start Date of Period&#x20;
     * End Date of Period&#x20;
     * ….&#x20;
     * ….&#x20;
  4. Attachment - Attachments consist of additional attributes like key-value pairs e.g. Account Number, Correlation ID or Documents&#x20;
  5. Signature - Fiscal messages can be signed by multiple agencies and add the signature to the Signature Array that contains the below-mentioned values -
     * Array of Signature&#x20;
       1. System&#x20;
       2. eSign - Signed Value of the Fiscal Event/Message Body using the System Key&#x20;
       3. Purpose - Acknowledgement or Approval or Rejection&#x20;
       4. Comments&#x20;
       5. Date of Signing

## **Reversal**

Data providers can reverse a previous fiscal message or event. The data provider reverses the data by posting the same event with a negative amount in the line item(s). The data consumers should handle reversals appropriately.

## **Querying**

Data consumers can query fiscal data. They can query Messages - the unread messages that have been delivered to them. When consumers read the unread messages, these messages are marked as read. Events - Consumers can also query fiscal events posted by other data providers.

### **Reference Data Management**

1. Location&#x20;
2. Administrative&#x20;
3. Chart of Account …. … …



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
