# mGramSeva - Billing Service

## **Overview**

The main objective of the billing module is to serve the Bill for all revenue Business services. To serve the Bill, Billing-Service requires demand. Demands will be prepared by Revenue modules and stored by billing based on which it will generate the Bill.

## **Pre-requisites**

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* Prior Knowledge of KAFKA
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc.
* Prior knowledge of the demand-based systems.
* Following services should be up and running:
  * user
  * MDMS
  * Id-Gen
  * URL-Shortening
  * notification-sms

## **Key Functionalities**

* **eGov** billing service creates and maintains demands.
* Generates bills based on demands.
* push created and updated bill/demand to Kafka on specified topics
* Updates the demands from payment when the collection service takes a payment.

## **Deployment Details**

* Deploy the latest image of the billing service available.

## **Configuration Details**

In the MDMS data configuration, the following master data is needed for the functionality of the billing

### **MDMS**

Business Service JSON

```
{
  "tenantId": "pb",
  "moduleName": "BillingService",
  "BusinessService": [
    {
      "businessService": "EXPENSE.ELECTRICITY_BILL",
      "code": "EXPENSE.ELECTRICITY_BILL",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true,
      "type": "Adhoc"
    },
     {
      "businessService": "EXPENSE.SALARY",
      "code": "EXPENSE.SALARY",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true,
      "type": "Adhoc"
    },
    {
      "businessService": "EXPENSE.OM",
      "code": "EXPENSE.OM",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true,
      "type": "Adhoc"
    },
    {
      "businessService": "EXPENSE.MISC",
      "code": "EXPENSE.MISC",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true,
      "type": "Adhoc"
    },
    {
      "businessService": "ws-services-calculation",
      "code": "WS",
      "collectionModesNotAllowed": [
        "DD",
        "CHEQUE",
        "CARD",
        "OFFLINE_NEFT",
        "OFFLINE_RTGS",
        "POSTAL_ORDER",
        "ONLINE"
      ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": false,
      "demandUpdateTime": 86400000,
      "isVoucherCreationEnabled": false,
      "billGineiURL" : "egov-searcher/bill-genie/waterbills/_get",
      "isBillAmendmentEnabled":true
    }
  ]
}

```

TAX-Head JSON

```
{
  "tenantId": "pb",
  "moduleName": "BillingService",
  "TaxHeadMaster": [
    {
      "category": "CHARGES",
      "service": "EXPENSE.ADVANCE",
      "name": "EXPENSE.ADVANCE_TAX",
      "code": "EXPENSE.ADVANCE_TAX",
      "isDebit": true,
      "isActualDemand": false,
      "order": "1",
      "isRequired": true
    },
    {
      "category": "CHARGES",
      "service": "EXPENSE.ELECTRICITY_BILL",
      "name": "EXPENSE.ELECTRICITY_BILL_TAX",
      "code": "20101",
      "isDebit": true,
      "isActualDemand": false,
      "order": "1",
      "isRequired": true
    },
    {
      "category": "CHARGES",
      "service": "EXPENSE.SALARY",
      "name": "Salary",
      "code": "20201",
      "isDebit": true,
      "isActualDemand": false,
      "order": "1",
      "isRequired": true
    },
    {
      "category": "CHARGES",
      "service": "EXPENSE.OM",
      "name": "O&M",
      "code": "20301",
      "isDebit": true,
      "isActualDemand": false,
      "order": "1",
      "isRequired": true
    },
    {
      "category": "CHARGES",
      "service": "EXPENSE.MISC",
      "name": "MISC",
      "code": "20401",
      "isDebit": true,
      "isActualDemand": false,
      "order": "1",
      "isRequired": true
    },
    {
      "category": "CHARGES",
      "service": "WS",
      "name": "Water Charges",
      "code": "10101",
      "isDebit": true,
      "isActualDemand": false,
      "order": "0",
      "isRequired": false,
      "IsBillamend": true
    },
    {
      "category": "CHARGES",
      "service": "WS",
      "name": "Water Charges - Arrears",
      "code": "10102",
      "isDebit": true,
      "isActualDemand": false,
      "order": "0",
      "isRequired": false,
      "IsBillamend": true
    },
    {
      "category": "TAX",
      "service": "WS",
      "name": "Rebate",
      "code": "WS_TIME_REBATE",
      "isDebit": true,
      "isActualDemand": false,
      "order": "0",
      "isRequired": false,
      "IsBillamend": false
    },
    {
      "category": "TAX",
      "service": "WS",
      "name": "Interest",
      "code": "WS_TIME_INTEREST",
      "isDebit": false,
      "isActualDemand": true,
      "order": "1",
      "isRequired": false,
      "IsBillamend": true
    },
    {
      "category": "TAX",
      "service": "WS",
      "name": "Water Cess",
      "code": "WS_WATER_CESS",
      "isDebit": false,
      "isActualDemand": true,
      "order": "2",
      "isRequired": false,
      "IsBillamend": true
    },
    {
      "category": "PENALTY",
      "service": "WS",
      "name": "Penalty",
      "code": "10201",
      "isDebit": false,
      "isActualDemand": true,
      "order": "3",
      "isRequired": false,
      "IsBillamend": true
    },
    {
      "category": "TAX",
      "service": "WS",
      "name": "Round Off",
      "code": "WS_Round_Off",
      "isDebit": false,
      "isActualDemand": true,
      "order": "4",
      "isRequired": false,
      "IsBillamend": false
    },
    {
      "category": "TAX",
      "service": "WS",
      "name": "Water adhoc rebate",
      "code": "WS_TIME_ADHOC_REBATE",
      "isDebit": false,
      "isActualDemand": true,
      "order": "5",
      "isRequired": false,
      "IsBillamend": false
    },
    {
      "category": "TAX",
      "service": "WS",
      "name": "Water adhoc penalty",
      "code": "WS_TIME_ADHOC_PENALTY",
      "isDebit": false,
      "isActualDemand": true,
      "order": "6",
      "isRequired": false,
      "IsBillamend": false
    },
    {
      "category": "ADVANCE_COLLECTION",
      "service": "WS",
      "name": "Ws advance carry forward",
      "code": "WS_ADVANCE_CARRYFORWARD",
      "isDebit": true,
      "isActualDemand": false,
      "order": "0",
      "isRequired": false,
      "IsBillamend": false
    },
    {
      "category": "CHARGES",
      "service": "WS",
      "name": "Water Amendment Charges",
      "code": "WS_AMENDMENT_CHARGES",
      "isDebit": true,
      "isActualDemand": false,
      "order": "3",
      "isRequired": false,
      "IsBillamend": true
    }
  ]
}

```

Tax-Period JSON

```
{
  "tenantId": "pb",
  "moduleName": "BillingService",
  "TaxPeriod": [
    {
      "fromDate": 1554076799000,
      "toDate": 1585679399000,
      "periodCycle": "ANNUAL",
      "service": "PT",
      "code": "PTAN2019",
      "financialYear": "2019-20"
    },
    {
      "fromDate": 1522540800000,
      "toDate": 1554076799000,
      "periodCycle": "ANNUAL",
      "service": "PT",
      "code": "PTAN2018",
      "financialYear": "2018-19"
    },
    {
      "fromDate": 1491004800000,
      "toDate": 1522540798000,
      "periodCycle": "ANNUAL",
      "service": "PT",
      "code": "PTAN2017",
      "financialYear": "2017-18"
    },
    {
      "fromDate": 1459468800000,
      "toDate": 1491004799000,
      "periodCycle": "ANNUAL",
      "service": "PT",
      "code": "PTAN2016",
      "financialYear": "2016-17"
    },
    {
      "fromDate": 1522540800000,
      "toDate": 1554076799000,
      "periodCycle": "ANNUAL",
      "service": "TL",
      "code": "TLAN2018",
      "financialYear": "2018-19"
    }
  ]
}
```

|                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                                                                                                                  |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bs.businesscode.demand.updateurl           | <p>{</p><p>"WS":"<a href="http://pt-calculator-v2:8080/pt-calculator-v2/propertytax/_updatedemand%22,%22TL%22:%22%22%7D">http://ws-calculator:8080/ws-calculator/waterCalculator/_updatedemand",</a></p><p><a href="http://pt-calculator-v2:8080/pt-calculator-v2/propertytax/_updatedemand%22,%22TL%22:%22%22%7D">"TL":""</a></p><p><a href="http://pt-calculator-v2:8080/pt-calculator-v2/propertytax/_updatedemand%22,%22TL%22:%22%22%7D">}</a></p> | Each module’s application calculator should provide its own update URL. if not present then new bill will be generated without making any changes to the demand. |
| bs.bill.billnumber.format                  | BILLNO-{module}-\[SEQ\_egbs\_billnumber{tenantid}]                                                                                                                                                                                                                                                                                                                                                                                                     | IdGen format for bill number                                                                                                                                     |
| `bs.amendment.idbs.bill.billnumber.format` | `BILLNO-{module}-[SEQ_egbs_billnumber{tenantid}]`                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                                                                                                                  |
| `is.amendment.workflow.enabled`            | `true/false`                                                                                                                                                                                                                                                                                                                                                                                                                                           | enable disable workflow of bill amendment                                                                                                                        |
| `kafka.mgramseva.create.demand`            | `mgramseva-create-demand`                                                                                                                                                                                                                                                                                                                                                                                                                              | topic name to push demand created, to be consumed by mgramseva adaptor                                                                                           |
| `kafka.mgramseva.update.demand`            | `mgramseva-update-demand`                                                                                                                                                                                                                                                                                                                                                                                                                              | topic name to push demand updated, to be consumed mgram sevaadaptor                                                                                              |
| `kafka.mgramseva.create.bill`              | `mgramseva-create-bill`                                                                                                                                                                                                                                                                                                                                                                                                                                | topic name to push bill created, to be consumed mgram seva                                                                                                       |
| `kafka.mgramseva.update.bill`              | `mgramseva-update-bill`                                                                                                                                                                                                                                                                                                                                                                                                                                | topic name to push bill updated, to be consumed mgram seva                                                                                                       |

## Integration

### Integration Scope

Billing service can be integrated with any organization or system that wants a demand-based payment system.

### Integration Benefits

* Easy to create and simple process of generating bills from demands
* The amalgamation of bills period-wise for a single entity like Water connection.
* Amendment of bills in case of legal requirements.

### Steps to Integration

1. Customers can create a demand using the `/demand/_create`
2. Organizations or Systems can search the demand using `/demand/_search`endpoint
3. Once the demand is raised the system can call `/demand/_update` endpoint to update the demand as per need.
4. Bills can be generated using, which is a self-managing API that generates a new bill only when the old one expires `/bill/_fetchbill.`
5. Bills can be searched using `/bill/_search.`
6. Amendment facility can be used in case of a legal issue to add values to existing demands using `/amendment/_create` and `/amendment/_update` can be used to cancel the created ones or update workflow if configured.

## Interaction Diagram

**Interaction Diagram V1.1**

![](<../../../../.gitbook/assets/image (63).png>)

## **Reference Docs**

### **Doc Links**

| **Title**       | **Link** |
| --------------- | -------- |
|  Id-Gen service |          |
| url-shortening  |          |
|  MDMS           |          |

### **API List**

| **Title**                             | **Link**                                                                                                                   |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
|  /demand/\_create, \_update, \_search | [https://www.getpostman.com/collections/900d99a85d083fb2d377](https://www.getpostman.com/collections/900d99a85d083fb2d377) |
|  /bill/\_fetchbill, \_search          | [https://www.getpostman.com/collections/900d99a85d083fb2d377](https://www.getpostman.com/collections/900d99a85d083fb2d377) |
| /amendment/\_create, \_update         | [https://www.getpostman.com/collections/b195d3b1d354c767b6bd](https://www.getpostman.com/collections/b195d3b1d354c767b6bd) |

## **Apportioning**

### What is apportioning?

Adjusting the receivable amount with the individual tax head.

### Types of apportioning V1.1:

Default order based apportioning(Based on apportioning order adjust the received amount with each tax head).V1.1

### Types of apportioning V1.2: (TBD)

* Proportionate based apportioning (Adjust total receivable with all the tax head equally)
* Order & Percentage based apportioning(Adjust total receivable based on order and the percentage which is defined for each tax head).

### Principle of Apportioning

&#x20;The basic principle of apportioning is, if the full amount is paid for any bill then each individual tax head should get nullify with their corresponding adjusted amount.

**Example**:\
**Case 1:** When there are no arrears all tax heads belong to their current purpose:\
&#x20;

| **TaxHead**                | **Amount** | **Order** | **Full Payment(2000)** | **Partial Payment1(1500)** | **Partial payment2(750)** | **Partial payment2 with rebate(500)** |
| -------------------------- | ---------- | --------- | ---------------------- | -------------------------- | ------------------------- | ------------------------------------- |
|                            |            |           |                        |                            |                           |                                       |
| WS\_CHARGE                 | 1000       | 6         | 1000                   | 1000                       | 750                       | 750                                   |
| AdjustedAmt                |            |           | 1000                   | -250                       | -750                      | -750                                  |
| RemainingAMTfromPayableAMT |            |           | 0                      | 0                          | 0                         | 0                                     |
|                            |            |           |                        |                            |                           |                                       |
| Penality                   | 500        | 5         | 500                    | 500                        |                           |                                       |
| AdjustedAmt                |            |           | 500                    | -500                       |                           |                                       |
| RemainingAMTfromPayableAMT |            |           | 1000                   | 250                        |                           |                                       |
|                            |            |           |                        |                            |                           |                                       |
|                            |            |           |                        |                            |                           |                                       |
| Interest                   | 500        | 4         | 500                    | 500                        |                           |                                       |
| AdjustedAmt                |            |           | 500                    | -500                       |                           |                                       |
| RemainingAMTfromPayableAMT |            |           | 1500                   | 750                        |                           |                                       |
|                            |            |           |                        |                            |                           |                                       |
| Cess                       | 500        | 3         | 500                    | 500                        |                           |                                       |
| AdjustedAmt                |            |           | 500                    | -500                       |                           |                                       |
| RemainingAMTfromPayableAMT |            |           | 2000                   | 1250                       |                           |                                       |
|                            |            |           |                        |                            |                           |                                       |
| Exm                        | -250       | 1         | -250                   | -250                       |                           |                                       |
| AdjustedAmt                |            |           | -250                   | 250                        |                           |                                       |
| RemainingAMTfromPayableAMT |            |           | 2250                   | 1750                       |                           |                                       |
|                            |            |           |                        |                            |                           |                                       |
| Rebate                     | -250       | 2         | -250                   |                            |                           | -250                                  |
| AdjustedAmt                |            |           | -250                   |                            |                           | 250                                   |
| RemainingAMTfromPayableAMT |            |           | 2500                   |                            |                           | 750                                   |

&#x20;\
**Case 2:** Apportioning with two years of arrear:\
If the current financial year is 2014-15. Below are the demands &#x20;

| **TaxHead** | **Amount** | **TaxPeriodFrom** | **TaxPeriodTo** | **Order** | **Purpose** |
| ----------- | ---------- | ----------------- | --------------- | --------- | ----------- |
|             |            |                   |                 |           |             |
| WS\_CHARGE  | 1000       | 2014              | 2015            | 6         | Current     |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Penality    | 500        | 2014              | 2015            | 5         | Current     |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Interest    | 500        | 2014              | 2015            | 4         | Current     |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Cess        | 500        | 2014              | 2015            | 3         | Current     |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Exm         | -250       | 2014              | 2015            | 1         | Current     |
| AdjustedAmt | 0          |                   |                 |           |             |

if any payment is not done, and we generating demand in 2015-16 then the demand structure will as follows:

| **TaxHead** | **Amount** | **TaxPeriodFrom** | **TaxPeriodTo** | **Order** | **Purpose** |
| ----------- | ---------- | ----------------- | --------------- | --------- | ----------- |
|             |            |                   |                 |           |             |
| WS\_CHARGE  | 1000       | 2014              | 2015            | 6         | Arrear      |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| WS\_CHARGE  | 1500       | 2015              | 2016            | 6         |  Current    |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Penality    | 600        | 2014              | 2015            | 5         | Arrear      |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Penalty     | 500        | 2015              | 2016            | 5         | Current     |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Interest    | 500        | 2014              |                 | 4         | Arrear      |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Cess        | 500        | 2014              |                 | 3         | Arrear      |
| AdjustedAmt | 0          |                   |                 |           |             |
|             |            |                   |                 |           |             |
| Exm         | -250       | 2014              |                 | 1         | Arrear      |
| AdjustedAmt | 0          |                   |                 |           |             |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
