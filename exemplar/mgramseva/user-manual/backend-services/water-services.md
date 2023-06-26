# mGramSeva - Water Services

## Overview

Water service is a DIGIT application that helps and gives flexibility to municipalities and citizens to manage water service requirements like apply for a water connection or search for water connections. The application goes through various steps as defined by the states. The application is passed through different users who verify and inspect the application details before moving it to the next stage. Based on the state, citizens get notifications (SMS and in-app ). Citizens can also pay for application fees or employees can collect the fee for the application.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has a water service persister config path added to it
* PSQL server is running and a database is created to store water connection/application data
* knowledge of eGov-mdms service, eGov-persister, eGov-idgen, eGov-sms, eGov-email,eGov-user, eGov-localization, eGov-workflow-service will be helpful.

## Key Functionalities

* Add old water connection to the system with/without arrears
* Create a new Water Connection
* Searching for water connections
* Notification based on the application state

| **Environment Variables**                                | **Description**                                                                                                               |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `egov.waterservice.createwaterconnection`                | This variable contains the kafka topic name which is used to create new water connection application in the system.           |
| `egov.waterservice.updatewaterconnection`                | This variable contains the kafka topic name which is used to update the existing water connection application in the system.  |
| `egov.waterservice.updatewaterconnection.workflow.topic` | This variable contains the kafka topic name which is used to update the process instance of the water connection application. |
| `egov.idgen.wcapid.name`                                 | This variable contains the idgen format name for water application                                                            |
| `egov.idgen.wcapid.format`                               | <p>This variable contains the idgen format for water application<br>ex:- WS/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]</p>    |
| `egov.idgen.wcid.name`                                   | This variable contains the idgen format name for water connection                                                             |
| `egov.idgen.wcid.format`                                 | <p>This variable contains the idgen format for water connection<br>ex:- WS_AP/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]</p>  |

## Interaction Diagram

![](../../../../.gitbook/assets/w-and-s-service-add-new-connection-20210914-131404.png)

**Table UML Diagram**

![](../../../../.gitbook/assets/screenshot-from-2020-07-15-12-50-16-1-.png)

### Configuration Details <a href="#configuration-details" id="configuration-details"></a>

_Mdms configuration_

[mdms-mgramseva/data at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/mdms-mgramseva)

master-config.json for water service

```
"ws-services-masters": {
    "connectionCategory": {
      "masterName": "connectionCategory",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "connectionType": {
      "masterName": "connectionType",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "waterSource": {
      "masterName": "waterSource",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "billingPeriod": {
      "masterName": "billingPeriod",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.billingCycle"
      ]
    },
    "waterSourceWithSubSource": {
      "masterName": "waterSourceWithSubSource",
      "isStateLevel": true,
      "uniqueKeys": []
    }
  },
  "ws-services-calculation": {
    "WaterCess": {
      "masterName": "WaterCess",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "Interest": {
      "masterName": "Interest",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.fromFY"
      ]
    },
    "Rebate": {
      "masterName": "Rebate",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.fromFY"
      ]
    },
    "Penalty": {
      "masterName": "Penalty",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.fromFY"
      ]
    },
    "WCBillingSlab": {
      "masterName": "WCBillingSlab",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "WS_CHARGE": {
      "masterName": "WS_CHARGE",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "WS_TIME_PENALTY": {
      "masterName": "WS_TIME_PENALTY",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "WS_WATER_CESS": {
      "masterName": "WS_WATER_CESS",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "MeterStatus": {
      "masterName": "MeterStatus",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "WS_Round_Off": {
      "masterName": "WS_Round_Off",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "PlotSizeSlab": {
      "masterName": "PlotSizeSlab",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "PropertyUsageType": {
      "masterName": "PropertyUsageType",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "FeeSlab": {
      "masterName": "FeeSlab",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "RoadType": {
      "masterName": "RoadType",
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

**ConnectionType**

Two connection types supported Metered and Non metered.

```
{
  "tenantId": "pb",
  "moduleName": "ws-services-masters",
  "connectionType": [
    {
      "name": "Metered",
      "code": "Metered",
      "active": true
    },
    {
      "name": "Non Metered",
      "code": "Non_Metered",
      "active": true
    }
  ]
}
```

**CheckList**

CheckList is used to define the Q & A for the feedback form and its validation.

```
{
	"tenantId": "pb",
	"moduleName": "ws-services-masters",
	"CheckList": [{
			"code": "HAPPY_WATER_SUPPLY",
			"name":"Are you happy with water supply?",
			"active": true,
			"required": true,
			"type": "SINGLE_SELECT",
			"options": [
				"1",
				"2",
				"3",
				"4",
				"5"
			]
		},
		{
			"code": "WATER_SUPPLY_REGULAR",
			"name": "Is the water supply regular?",
			"active": true,
			"type": "SINGLE_SELECT",
			"required": true,
			"options": [
				"1",
				"2",
				"3",
				"4",
				"5"
			]
		},
		{
			"code": "WATER_QUALITY_GOOD",
			"name":"Is the water quality good?",
			"active": true,
			"type": "SINGLE_SELECT",
			"required": true,
			"options": [
				"1",
				"2",
				"3",
				"4",
				"5"
			]
		}
	]
}
```

**Category**

Predefined list of categories allowed.

```
{
  "tenantId": "pb",
  "moduleName": "ws-services-masters",
  "Category": [
    {
      "code": "APL",
      "name": "APL"
    },
    {
      "code": "BPL",
      "name": "BPL"
    }
  ]
}
```

**SubCategory**

Predefined list of subcategories allowed

```
{
  "tenantId": "pb",
  "moduleName": "ws-services-masters",
  "SubCategory": [
    {
      "code": "SC",
      "name": "SC"
    },
     {
      "code": "ST",
      "name": "ST"
    },
    {
      "code": "GENERAL",
      "name": "General"
    }
  ]
}
```

Property creation through WNS module\
[mdms-mgramseva/PTWorkflow.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/mdms-mgramseva/blob/DEV/data/pb/PropertyTax/PTWorkflow.json)

_Persister configuration_

[config-mgramseva/water-persist.yml at DEV · egovernments/configs](https://github.com/egovernments/config-mgramseva/blob/DEV/egov-persister/water-persist.yml)\
[<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/water-meter.yml at master · egovernments/configs](https://github.com/egovernments/configs/blob/master/egov-persister/water-meter.yml)

### Actions & Role Action Mapping

_Actions_

```
[
  {
      "id": {{PLACEHOLDER1}},
      "name": "Create Water Connection",
      "url": "/ws-services/wc/_create",
      "displayName": "Create Water COnnection",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER2}},
      "name": "Search Water Connection",
      "url": "/ws-services/wc/_search",
      "displayName": "Search Water COnnection",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER3}},
      "name": "Update Water Connection",
      "url": "/ws-services/wc/_update",
      "displayName": "Update Water COnnection",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
   {
      "id": {{PLACEHOLDER4}},
      "name": " feedback create",
      "url": "/ws-services/wc/_submitfeedback",
      "parentModule": "",
      "displayName": "create feedback",
      "orderNumber": 2,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
	{
      "id": {{PLACEHOLDER5}},
      "name": " feedback search",
      "url": "/ws-services/wc/_getfeedback",
      "parentModule": "",
      "displayName": "get feedback",
      "orderNumber": 2,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    }
]


```

_Role Action Mapping_

```
[
 
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SUPERUSER",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SUPERUSER",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "COLLECTION_OPERATOR",
      "actionid": {{PLACEHOLDER2}},
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
      "rolecode": "EXPENSE_PROCESSING",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DASHBOARD_VIEWER",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    }, 
    {
      "rolecode": "EMPLOYEE",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "COLLECTION_OPERATOR",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EMPLOYEE",
      "actionid": {{PLACEHOLDER3}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER3}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SUPERUSER",
      "actionid": {{PLACEHOLDER3}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER3}},
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

_Roles available_

```

		{
      "code": "GP_ADMIN",
      "name": "GP Admin",
      "description": "Who has a access to ws-services"
    },
		{
      "code": "COLLECTION_OPERATOR",
      "name": "Collection Operator",
      "description": "Who has a access to ws-services,demand, bill and payment"
    },
		{
      "code": "BULK_DEMAND_PROCESSING",
      "name": "Bulk Demand Processing",
      "description": "Who has a access to bulk demand generation,raise bill, downloa bill and receipts"
    },
		{
      "code": "EXPENSE_PROCESSING",
      "name": "Expense Processing",
      "description": "Who has a access to create and update expenses"
    },
		{
      "code": "DASHBOARD_VIEWER",
      "name": "Dashbaord Viewer",
      "description": "Who has a access to dashboard of revenue and expenditure"
    }
```

_Workflow business service config:_

Create businessService (workflow configuration) using the  `/businessservice/_create`. Following is the product configuration for water service

```
{
  "RequestInfo": {
    "apiId": "Rainmaker",
    "action": "",
    "did": 1,
    "key": "",
    "msgId": "20170310130900|en_IN",
    "requesterId": "",
    "ts": 1513579888683,
    "ver": ".01",
    "authToken": "{{Auth_Token}}"
  },
  "BusinessServices": [
    {
      "tenantId": "pb",
      "businessService": "NewWS1",
      "business": "WS",
      "businessServiceSla": 0,
      "states": [
        {
          "tenantId": "pb",
          "sla": null,
          "state": null,
          "applicationStatus": "DRAFT",
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "tenantId": "pb",
              "action": "SUBMIT",
              "nextState": "APPROVE",
              "roles": [
                "GP_ADMIN"
              ],
              "active": true
            }
          ]
        },
        {
          "tenantId": "pb",
          "sla": null,
          "state": "APPROVED",
          "applicationStatus": "ACTIVE",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true,
          "isStateUpdatable": true,
          "actions": null
        }
      ]
    }
  ]
}
```

_Indexer config for water_ _service_:

* The indexer provides the facility for indexing the data to elastic search.[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">config-mgramseva/water-service.yml at DEV · egovernments/config-mgramseva](https://github.com/egovernments/config-mgramseva/blob/DEV/egov-indexer/water-service.yml)

#### **Setup**

1. Write the configuration for water service.[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">config-mgramseva/water-service.yml at DEV · egovernments/config-mgramseva](https://github.com/egovernments/config-mgramseva/blob/DEV/egov-indexer/water-service.yml)
2. Provide the absolute path of the checked-in file to DevOps, to add it to the file-read path of egov-indexer. The file will be added to the egov-indexer's environment manifest file for it to be read at the start-up of the application.
3. Put indexer config file to the config repo under egov-indexer folder.([<img src="https://github.com/fluidicon.png" alt="" data-size="line">GitHub - egovernments/configs at master](https://github.com/egovernments/configs/tree/master) )
4. Run the egov-indexer app, Since it is a consumer, it starts listening to the configured topics and indexes the data.

#### **Notification**

Notification will be sent to the property owners and connection holders based on different application states.

#### **Capturing Connection Holders**

We can add connection holders to the water connection which will be the owner of the connection. We can fill in the connection holders' details or we can just make the property owner to the connection holder.

The connection holder will get a notification based on a different state of the application. We are pushing the data of the connection holders in the user service too.

#### **Multiple Road Type Support**

We can add road cutting details of multiple roads to the water connection. For each road that goes undercutting process, we have to fill their road type details and road cutting area.\
Based on this information, the application one-time fee estimate is calculated.

## Deployment Details

1. Add mdms configs required for water connection registration and restart mdms service.
2. Deploy the latest version of ws-services service.
3. Add water-service and water-services-meter persister yaml path in persister configuration and restart persister service.
4. Add Role-Action mapping for API’s.
5. Create businessService (workflow configuration) according to trade water connection, modify water connection
6. Add ws-service indexer yaml path in indexer service configuration and restart indexer service.

## Integration&#x20;

### Integration Scope

This ws-service module is used to manage water service connections against a property in the system.

### Integration Benefits

* Provide backend support for the different water connection registration processes.
* Mseva and SMS notifications on application status changes.
* The elastic search index for creating visualizations and Dashboards.
* Supports workflow which is configurable

### Steps to Integration

1. To integrate, the host of ws-service module should be overwritten in helm chart.
2. &#x20;`/ws-services/wc/_create` should be added as the create endpoint for creating water application/connection in the system.
3. &#x20;`/ws-services/wc/_search` should be added as the search endpoint . This method handles all requests to search existing records depending on different search criteria.
4. &#x20;`/ws-services/wc/_update` should be added as the update endpoint. This method is used to update fields in existing records or to update the status of the application based on workflow.

## Reference Docs

### Doc Links

| **Title**                 | **Link**                                                                                                                                                              |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/docs/water-sewerage-services.yaml#!/) |
| Water Calculator Service  | [Water-Service Calculator](water-service-calculator.md)                                                                                                               |

### API List

|                                         | **Link**                                                                                                                                           |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
|  _/ws-services/wc/\_create_             | [https://www.getpostman.com/collections/b7f8f02e80eec21f926d](https://www.getpostman.com/collections/b7f8f02e80eec21f926d)                         |
| _/ws-services/wc/\_update_              | [https://www.getpostman.com/collections/b7f8f02e80eec21f926d](https://www.getpostman.com/collections/b7f8f02e80eec21f926d)                         |
| _/ws-services/wc/\_search_              | [https://www.getpostman.com/collections/b7f8f02e80eec21f926d](https://www.getpostman.com/collections/b7f8f02e80eec21f926d)                         |
| /ws-services/wc/\_submitfeedback        | <p><a href="https://www.getpostman.com/collections/b7f8f02e80eec21f926d">	<br>https://www.getpostman.com/collections/b7f8f02e80eec21f926d</a></p> |
| /ws-services/wc/\_getfeedback           | [https://www.getpostman.com/collections/b7f8f02e80eec21f926d](https://www.getpostman.com/collections/b7f8f02e80eec21f926d)                         |
| /ws-services/wc/\_revenueDashboard      | [https://www.getpostman.com/collections/d79438f50b433917269d](https://www.getpostman.com/collections/d79438f50b433917269d)                         |
| /ws-services/wc/\_revenueCollectionData | [https://www.getpostman.com/collections/d79438f50b433917269d](https://www.getpostman.com/collections/d79438f50b433917269d)                         |

_(Note: All the API’s are in the same postman collection therefore the same link is added in each row)_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

