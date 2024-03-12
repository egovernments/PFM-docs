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

### Key Functionality

* The creation of a disbursement request involves listening for payment creation events on a designated topic. When a payment is created, the adapter processes the event, extracts relevant information, and forwards the enriched disbursement request to the Program Service for further processing.
* In case of a failure in the payment topic, we also have the option to manually create a disbursement using the adapter by providing the payment number.
* We have the ability to search for the created disbursements.
* After forwarding the disbursement to the program service, it undergoes sanction enrichment. Subsequently, it is forwarded to the Digit Exchange service, establishing a connection between two servers. Once a response is received from the IFMS system, the disbursement undergoes further enrichment and is sent back to the Mukta Adapter. The adapter then updates the payment status based on the statuses received in the disbursement.

### Code



### Deployment

[Helm Chart](https://github.com/egovernments/DIGIT-DevOps/tree/unified-env/deploy-as-code/helm/charts/digit-works/utilities/mukta-ifix-adapter)

### Master Data

| Master Name                                                                        | Sample Data                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Description                                                                                  |
| ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| <pre><code>HeadOfAccounts
</code></pre>                                            | <p></p><pre class="language-json"><code class="lang-json">"HeadOfAccounts": [
    {
      "id": "1",
      "code": "221705800358641045908",
      "name": "General Head",
      "sequence": 1,
      "schemeCode": 13145,
      "active": true,
      "effectiveFrom": 1682164954037,
      "effectiveTo": null
    },
    ]
</code></pre>                                                                                                                      | Head of accounts to be used for the Mukta scheme at the state level - to be provided by HUDD |
| <p></p><pre class="language-json"><code class="lang-json">SSUDetails
</code></pre> | <p></p><pre class="language-json"><code class="lang-json">"SSUDetails": [
    {
      "id": "1",
      "ssuCode": "OLSHUD001",
      "ddoCode": "OLSHUD001",
      "granteeAgCode": "GOHUDULBMPL0036",
      "granteeName": "ANGUL MUNICIPALITY",
      "programCode": "PG/2023-24/000310",
      "ssuId": "1621",
      "ssuOffice": "angul_op",
      "effectiveFrom": 1682164954037,
      "effectiveTo": null,
      "active": true
    }
  ]
</code></pre> | Spending unit details specific to each ULB are to be provided by HUDD.                       |

### Integration

#### base path:&#x20;

/mukta-ifix-adapter/

#### API Spec

TBD

#### Postman Collection:

TBD

