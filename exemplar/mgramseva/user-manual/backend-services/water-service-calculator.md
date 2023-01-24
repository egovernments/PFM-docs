# mGramSeva - Water Service Calculator

## Overview

Water Calculator Service is used for creating meter reading, searching meter reading, updating existing meter reading, calculation of water charge, demand generation, SMS & email notification to ULB officials on-demand generation and estimation of water charge(one-time cost) which involves cost like road-cutting charge, form fee, scrutiny fee, etc.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has water service persister configs path added in it
* PSQL server is running and a database is created to store water connection/application data
* Following services should be up and running:
  * egov-perister
  * egov-mdms
  * ws-services
  * billing-service

## Key Functionalities

* Calculate water charges and taxes based on billing slab
* Calculate meter reading charge for water connection
* Generate demand
* Scheduler for generating the demand(for non metered connection)

| **Environment Variables**    | **Description**                                                       |
| ---------------------------- | --------------------------------------------------------------------- |
| `notification.sms.enabled`   | This variable is to check the SMS notifications are enabled or not.   |
| `notification.email.enabled` | This variable is to check the email notifications are enabled or not. |
| `download.bill.link.path`    | This variable is for download bill reciept path                       |
| `egov.demand.gp.user.link`   | This variable is to get the common link to the home page              |

## Deployment Details

1. Deploy the latest version of ws-service and ws-calculator
2. Add water-persist.yml & water-meter.yml file in config folder in git and add that path in persister. _(The file path is to be added in environment yaml file in param called_ `persist-yml-path` _)_

## Configuration Details

### MDMS Configuration

Master Config

```
"ws-services-calculation": {
    
    "WCBillingSlab": {
      "masterName": "WCBillingSlab",
      "isStateLevel": true,
      "uniqueKeys": []
    },
   
    "CalculationAttribute": {
      "masterName": "CalculationAttribute",
      "isStateLevel": true,
      "uniqueKeys": []
    }
  }
```

#### **Billing Slabs** <a href="#billing-slabs" id="billing-slabs"></a>

Criteria&#x20;

1. connection type
2. building type
3. calculation attribute
4. property usage type

The combination of the above can be used to define the billing slab. Billing Slab is defined in mdms under ws-services-calculation folder with the [WCBillingSlab](https://github.com/egovernments/mdms-mgramseva/blob/DEV/data/pb/ws-services-calculation/WCBillingSlab.json). The following is the sample slab.

```
{
      "id": "1",
      "buildingType": "RESIDENTIAL",
      "connectionType": "Metered",
      "calculationAttribute": "Water consumption",
      "minimumCharge": 100,
      "slabs": [
        {
          "from": 0,
          "to": 10,
          "charge": 2,
          "meterCharge": 50
        },
        {
          "from": 10,
          "to": 20,
          "charge": 2.5,
          "meterCharge": 50
        },
        {
          "from": 20,
          "to": 30,
          "charge": 8,
          "meterCharge": 150
        },
        {
          "from": 30,
          "to": 40,
          "charge": 12,
          "meterCharge": 150
        },
        {
          "from": 40,
          "to": 1000000000,
          "charge": 15,
          "meterCharge": 150
        }
      ]
    }

```

If all criteria will match for that water connection this slab will use for calculation.

### **Estimation**

#### Water Charge and Tax <a href="#water-charge-and-tax" id="water-charge-and-tax"></a>

Water charge is based on billing slab, for water application charge will be based on slab and tax based on master configuration.

```
{
  "tenantId": "pb.massewal",
  "moduleName": "ws-services-calculation",
  "WCBillingSlab": [
    {
      "id": "1",
      "buildingType": "RESIDENTIAL",
      "connectionType": "Metered",
      "calculationAttribute": "Water consumption",
      "minimumCharge": 100,
      
      "slabs": [
        {
          "from": 0,
          "to": 1000000,
          "charge": 2,
          "meterCharge": 50
        }
      ]
    },
    {
      "id": 2,
      "buildingType": "COMMERCIAL",
      "calculationAttribute": "Water consumption",
      "connectionType": "Metered",
      
      "minimumCharge": 200,
      "slabs": [
        {
          "from": 0,
          "to": 1000000,
          "charge": 13.31,
          "meterCharge": 532.4
          
        }
      ]
    },
    {
      "id": 3,
      "buildingType": "MIXED",
      "calculationAttribute": "Water consumption",
      "connectionType": "Metered",
      
      "minimumCharge": 200,
      "slabs": [
        {
          "from": 0,
          "to": 1000000,
          "charge": 13.31,
          "meterCharge": 532.4
          
        }
      ]
    },
    {
      "id": "4",
      "buildingType": "PUBLICSECTOR",
      "calculationAttribute": "Water consumption",
      "connectionType": "Metered",
      "minimumCharge": 150,
      
      "slabs": [
        {
          "from": 0,
          "to": 1000000,
          "charge": 8,
          "meterCharge": 250
        }
      ]
    },
    {
      "id": "5",
      "buildingType": "RESIDENTIAL",
      "calculationAttribute": "Flat",
      "connectionType": "Non_Metered",
      
      "minimumCharge": 150
    },
    {
      "id": "6",
      "buildingType": "COMMERCIAL",
      "calculationAttribute": "Flat",
      "connectionType": "Non_Metered",
      
      "minimumCharge": 150
    },
    {
      "id": "7",
      "buildingType": "MIXED",
      "calculationAttribute": "Flat",
      "connectionType": "Non_Metered",
      
      "minimumCharge": 150
    },
       {
      "id": "8",
      "buildingType": "PUBLICSECTOR",
      "calculationAttribute": "Flat",
      "connectionType": "Non_Metered",
      
      "minimumCharge": 150
    }
  ]
}

```

#### Actions & Role Action Mapping <a href="#actions-and-role-action-mapping" id="actions-and-role-action-mapping"></a>

**Actions**

```
[
  {
      "id": {{PLACEHOLDER1}},
      "name": "Bulk Demand Generation",
      "url": "/ws-calculator/waterCalculator/_bulkDemand",
      "parentModule": "",
      "displayName":"Bulk Demand Generation",
      "orderNumber": 1,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER2}},
      "name": "Demand Calculation",
      "url": "/ws-calculator/waterCalculator/_calculate",
      "parentModule": "",
      "displayName": "Demand Calculation",
      "orderNumber": 2,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER3}},
      "name": "Meter Demand Calculation",
      "url": "/ws-calculator/meterConnection/_create",
      "parentModule": "",
      "displayName": "Meter Demand Calculation",
      "orderNumber": 3,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER4}},
      "name": "Meter Demand search",
      "url": "/ws-calculator/meterConnection/_search",
      "parentModule": "",
      "displayName": "Meter Demand search",
      "orderNumber": 3,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER5}},
      "name": "Demand Estimate",
      "url": "/ws-calculator/waterCalculator/_estimate",
      "parentModule": "",
      "displayName": "Demand Estimate",
      "orderNumber": 2,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    }
]


```

**Role Action Mapping**

```
[
    {
      "rolecode": "BULK_DEMAND_PROCESSING",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BULK_DEMAND_PROCESSING",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BULK_DEMAND_PROCESSING",
      "actionid": {{PLACEHOLDER3}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BULK_DEMAND_PROCESSING",
      "actionid": {{PLACEHOLDER4}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "COLLECTION_OPERATOR",
      "actionid": {{PLACEHOLDER4}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER4}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER5}},
      "actioncode": "",
      "tenantId": "pb"
    }
]
```

### How to **A**dd New BillingSlab/RateMaster <a href="#how-to-add-new-billingslab-ratemaster" id="how-to-add-new-billingslab-ratemaster"></a>

Charge for the given connection for a given billing cycle will be defined/identified by the system with the help of the **CalculationAtrribute** MDMS and **WCBillngSlab** MDMS.

CalcualtionAttribute helps to identify the type of calculation for the given connectionType below mdms of

1. Metered Connection **water consumption** is the attribute used for the calculation of charge for billing cycle i.e Based no the units consumed for a given billing cycle for a given connection would identify the actual charge from the **WCBIllingSlab** mdms based on the **propertyType, calcautionAttribute** derived for a connection **and ConnectionType**
2. Non-Metered Connection **Flat** is the attribute used for calculation of the charge for a given billing cycle, i.e for NonMetered connection, there would be a flat charge for the given billing cycle. The amount can be derived from the **WCBillingSlab** mdms based on the **propertyType, calcautionAttribute** derived for a connection **and ConnectionType.**

### Demand Generation

Once water is sent to the calculator its tax estimates are calculated. Using these tax head estimates demand details are created. For every tax head, the estimated demand generates function will create a corresponding demand detail.

Whenever \_calculate API is called demand is first searched based on the connection no and the demand from and to period. If demand already exists the same demand is updated else new demand is generated with consumer code as connection no and demand from and to a period equal to financial year start and end period.

In the case of the update, if the tax head estimates change, the difference in amount for that tax head is added as new demand detail. For example, if the initial demand has one demand detail with WATER\_CHARGE equal to 120.

```
"demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "WATER_CHARGE",
                    "taxAmount": 120,
                    "collectionAmount": 120,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                }
            ],

```

After updating if the WATER\_CHARGE increases to 150 we add one more demand detail to account for the increased amount. The demand detail will be updated to:

```
"demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "WATER_CHARGE",
                    "taxAmount": 120,
                    "collectionAmount": 0,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                },
                {
                    "id": "0d83f4b0-6442-11ea-bc55-0242ac130003 ",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "WATER_CHARGE",
                    "taxAmount": 30,
                    "collectionAmount": 0,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                }
            ],

```

RoundOff is bill based i.e every time bill is generated round off is adjusted so that payable amount is the whole number. Individual WS\_ROUNDOFF in demand detail can be greater than 0.5 but the sum of all WS\_ROUNDOFF will always be less than 0.5.

### Scheduler For Generating the Demand (For non metered connection) <a href="#scheduler-for-generating-the-demand-for-non-metered-connection" id="scheduler-for-generating-the-demand-for-non-metered-connection"></a>

_**Description**_&#x20;

For generating the demand for non metered connections we have a feature for generating the demand in batch. The scheduler is responsible for generating the demand based on the tenant.

* The scheduler can be hit by scheduler API or we can schedule cron job or we can put config to kubectl which will hit scheduler based on config.
* After the scheduler has been hit we will search the list of the tenant (city) present in the database.
* After getting the tenants we will pick up tenants one by one and generate the demand for that tenant.
* We will load the consumer codes for the tenant and push the calculation criteria to Kafka. Calculation criteria contain minimal information (We are not pushing large data to Kafka), calculation criteria contain consumer code and one boolean variable.
* After pushing the data into Kafka we are consuming the records based on the batch configuration. Ex:-> if the batch configuration is 50 so we will consume the 50 calculation criteria at a time.
* After consuming the record(Calculation criteria) we will process the batch for generating the demand. If the batch is successful so will log the consumer codes which have been processed.
* If some records failed in batch so we will push the batch into dead letter batch topic. From the dead letter batch topic, we will process the batch one by one.
* If the record is successful we will log the consumer code, If the record is failed so we will push the data into a dead letter single topic.
* Dead letter single topic contains information about failure records in Kafka.

_**Use cases**_

_If the same job trigger multiple time what will happen?_

If the same job triggers multiple times we will process again as mentioned above but at the demand level we will check the demand based on consumer code and billing period, If demand already exists then we will update the demand otherwise we will create the demand.

_Are we maintaining success or failure status anywhere?_

Currently, we are maintaining the status of failed records in Kafka.

_**Configuration**_

We need to configure the batch size for Kafka consumers. This configuration is for how much data will be processed at a time.

```
ws.demand.based.batch.size=10
```

## Integration

### Integration Scope

ws-calculator will be integrated with ws-service. ws-services internally invoke the ws-calculator service to calculate and generate demand for the charges.

### Integration Benefits

WS calculator application is used to calculate the water application one-time Fees and meter reading charges based on the different billing slabs that's why the calculation and demand generation logic will be separated out from the WS service.\
So in future, if calculation logic needs to modify then changes can be carried out for each implementation without modifying the WS service.

### Steps to Integration

1. &#x20;Once the water connection is activated for metered connection, an employee can add meter reading details using this API - `/ws-calculator/meterConnection/_create`which in turn will generate the demand. For the Non-Metered connections, the scheduler APIs need to be called periodically to generate the demand.
2. For the Metered Connection service, to get the previous meter reading `/meterConnection/_search` API is used.
3. To generate the demand for metered or non-metered water connection `/waterCalculator/_calculate` API is used.
4. Users can pay partial/full/advance amount for the Metered or Non-Metered connection bill. In these cases, the Billing service would call back `/waterCalculator/_updateDemand`API to update the details of the demand generated.
5. `/waterCalculator/_jobscheduler` API is used to generate demand for Non-metered connections. This API can be called periodically.

## Reference Docs

### Doc Links

| **Title**              | **Link**                                                                                                                                                                                                         |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Contract   | [![](https://editor.swagger.io/dist/favicon-32x32.png)Swagger Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/docs/water-sewerage-services.yaml) |
| Water Service Document | [Water Service](water-services.md)                                                                                                                                                                               |

### API List

|                                          | **Link**                                                                                                                   |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `/ws-calculator/meterConnection/_create` | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |
| `/ws-calculator/meterConnection/_search` | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |
| `/waterCalculator/_estimate`             | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |
| `/waterCalculator/_calculate`            | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |
| `/waterCalculator/_updateDemand`         | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |
| `/waterCalculator/_jobscheduler`         | [https://www.getpostman.com/collections/b9a7bde133b0e1fa465f](https://www.getpostman.com/collections/b9a7bde133b0e1fa465f) |

_(Note: All the API’s are in the same postman collection therefore the same link is added in each row)_\


> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
