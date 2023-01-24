# iFix Adapter Integration Service

## **Objective**

The purpose of the mGramSeva IFIX adapter service is to push the demand, bill, and payment events to IFIX from the mGramSeva.

## Overview <a href="#overview" id="overview"></a>

mGramSeva IFIX adapter service is a wrapper for pushing data from the mGramSeva to IFIX. When demand or payment is generated in the mGramSeva system, mGramSeva IFIX adapter service listens to those topics and it calls the IFIX reference adapter service push API to publish the data to IFIX.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
* Kafka
* Spring boot

## Key Functionalities

* Pushing demand, bill and payment events to IFIX adapter

&#x20;The following topics interact with the mGramSeva IFIX adapter service - When we create demand for ws-services, then it sends an event as demand for IFIX. If it is expense demand, it sends the event as a bill for IFIX. If it is ws-services payment, then it sends the event as a receipt for IFIX. If it is an expense payment, it sends the payment as an event for IFIX.

* mgramseva-create-demand
* mgramseva-update-demand
* egov.collection.payment-create

## Deployment Details

Please deploy the following build.

* **ifix-adapter:v1.0.0-4e24064-14**

## Integration

### Integration Scope

mGramSeva IFIX adapter is integrated with the IFIX Reference adaptor service. mGramSeva IFIX adapter Application internally invokes the IFIX Reference adaptor service to push the data.

### Steps to Integration

mGramSeva IFIX adapter application to call IFIX-reference-adapter/events/v1/\_push to push the demand, bill, and payment events from mGramSeva to IFIX.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
