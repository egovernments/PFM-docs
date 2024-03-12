# Mukta iFix Adapter

## Overview

The Mukta iFix Adapter is a service designed to facilitate communication between the Expense Service and the Program Service. It acts as a mediator, listening for payment creation events from the Expense Service, enriching the payment request data, and generating disbursement requests. These disbursement requests are then sent to the Program Service for further processing.

### Dependencies

* Expense Service
* Expense Calculator Service
* MDMS Service
* Bank Account Service
* Individual Service
* Organization Service
* User Service
* Program Service
* Encryption Service

## API Specifications

**Base path:** /mukta-ifix-adapter/

### API Contract Link

TBD

## Data Model

### DB Schema Diagram

<figure><img src="../../../.gitbook/assets/Mukta Adapter (1).png" alt=""><figcaption></figcaption></figure>

## Postman Collection

TBD

