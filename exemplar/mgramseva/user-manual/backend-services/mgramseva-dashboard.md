---
description: mGramsev-DSS Documentation
---

# mGramSeva Dashboard

## **Overview**

DSS has two sides to it. One is, the process in which the Data is pooled to ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of Data Sets, there is a need for making this configurable. So that, tomorrow, given a new scenario is introduced, then it is just a configuration away from getting the newly introduced scenario involved in this process flow.&#x20;

This document explains the steps on how to define the configurations for the Analytics Side Of DSS for mGramSeva.

### **What is analytics?**

**Analytics :** Micro Service which is responsible for building, fetching, aggregating and computing the Data on ElasticSearch to a consumable Data Response. Which shall be later used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. we need to add the changes related to mGramseva in this dashboard-analytics.\
Here is the location: [https://github.com/misdwss/config-mgramseva/tree/QA/egov-dss-dashboards/dashboard-analytics](https://github.com/misdwss/config-mgramseva/tree/QA/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run mGramSeva successfully.

1. Chart API Configuration
2. Master Dashboard Configuration

## **Description**  <a href="#description" id="description"></a>

### **Chart API Configuration**&#x20;

Each Visualization has its own properties. Each Visualization comes from different data sources (Sometimes it is a combination of different data sources)&#x20;

In order to configure each visualization and its properties, we have a Chart API Configuration Document.

In this, Visualization Code, which happens to be the key, will be having its properties configured as a part of the configuration and are easily changeable.

Here is the sample ChartApiConfiguration.json data for the mGramSeva.

```
"revenueAndExpenditureTrendTwo": {
    "chartName": "DSS_MGRAMSEVA_COLLECTIONS_DATA_TWO",
    "queries": [
      {
        "module": "WS",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.Bill.billDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\"}",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}]}},\"aggs\":{\"Water_Service\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"dataObject.paymentDetails.bill.businessService.keyword\":[\"WS\"]}}]}},\"aggs\":{\"WaterService\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"month\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.amountPaid\"}}}}}},\"Expense_Service\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"dataObject.paymentDetails.bill.businessService.keyword\":[\"EXPENSE.SALARY\",\"EXPENSE.OM\",\"EXPENSE.ELECTRICITY_BILL\"]}}]}},\"aggs\":{\"ExpenseService\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"month\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.amountPaid\"}}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "WaterService",
      "ExpenseService"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {},
    "_comment": " "
  },
```

[Click here to check the complete configuration](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json).

### **Master Dashboard Configuration**

Master Dashboard Configuration is the main configuration that defines as to which are the Dashboards that are to be painted on the screen.&#x20;

It includes all the Visualizations, their groups, the charts which comes within them and even their dimensions as what should be their height and width.

```
{
      "name": "DSS_MGRAMSEVA_DASHBOARD",
      "id": "mgramseva-wc",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 431,
              "name": "DSS_MGRAMSEVA_WC",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "revenueAndExpenditureTrendOne",
                  "name": "DSS_MGRAMSEVA_COLLECTIONS_DATA_ONE",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName": "Graphical"
                },
                {
                  "id": "revenueAndExpenditureTrendTwo",
                  "name": "DSS_MGRAMSEVA_COLLECTIONS_DATA_TWO",
                  "code": "",
                  "chartType": "line",
                  "filter": "",
                  "headers": [],
                  "tabName": "Expenditure"
                }
              ]
            }
          ]
        }
      ]
    }
```

[Click here to check the complete configuration](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

### **Role Dashboard Mappings Configuration**

Master Dashboard Configuration which was explained earlier hold the list of Dashboards that are available.

Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration will act as Role - Dashboard Mapping Configuration&#x20;

In this, each Role is mapped against the Dashboard which they are authorized to see

This was used earlier when the Role Action Mapping of eGov was not integrated.

Later, when the Role Action Mapping started controlling the Dashboards to be seen on the client-side, this configuration was just used to enable the Dashboards for viewing.&#x20;

[Click Here to check the complete configuration.](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-analytics/RoleDashboardConfig.json)

* Transform collection schema for V2
  * This transform collection v1 configuration file is used to map with the incoming data. This mapped data will go inside the data object in the DSS collection v2 index.

![](../../../../.gitbook/assets/image-20201010-143543.png)

* [Click here for an example configuration](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-ingest/transform\_collection\_v1.json)
*   Here: **$i**, the variable value that gets incremented for the number of records of paymentDetails&#x20;

    **$j**, the variable value that gets incremented for the number of records of billDetails.
* This configuration defines and directs the Enrichment Process which the data goes through.
* For example, if the Data which is incoming is belonging to a Collection Module data, then the Collection Domain Config is picked. And based on the Business Type specified in the data, the right config is picked.&#x20;
* In order to enhance the data of Collection, the domain index specified in the configuration is queried with the right arguments and the response data is obtained, transformed and set.&#x20;

### Enrichment Domain Configuration

1. Domain Configuration
2. Topic Context Configuration
3. transform\_expense.electricity\_bill\_v1 Configuration
4. transform\_expense.om\_v1 Configuration
5. transform\_expense.salary\_v1 Configuration
6. transform\_ws\_v1 Configuration

Below are the list of configurations made changes or added newly for mGramseva

```
 {
            "id": "4",
            "domain": "WS",
            "indexName": "water-services",
            "documentType": "",
            "query": "{\"query\":{\"bool\":{\"must\":[{\"match_phrase\":{\"Data.connectionNo\":\"value\"}}]}}}",
            "targetReferences": [
                {
                    "fieldName": "connectionNo",
                    "argument": "Data.connectionNo",
                    "dataType": "String",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "connectionNo"
                }
            ],
            "sourceReferences": [
                {
                    "fieldName": "consumerCode",
                    "argument": "Data.connectionNo",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "connectionNo"
                }
            ]
        },
        {
            "id": "5",
            "domain": "EXPENSE.SALARY",
            "indexName": "echallan-services",
            "documentType": "",
            "query": "{\"query\":{\"bool\":{\"must\":[{\"match_phrase\":{\"Data.challanNo\":\"value\"}}]}}}",
            "targetReferences": [
                {
                    "fieldName": "challanNo",
                    "argument": "Data.challanNo",
                    "dataType": "String",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "challanNo"
                }
            ],
            "sourceReferences": [
                {
                    "fieldName": "consumerCode",
                    "argument": "Data.challanNo",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "challanNo"
                }
            ]
        },
        {
            "id": "6",
            "domain": "EXPENSE.ELECTRICITY_BILL",
            "indexName": "echallan-services",
            "documentType": "",
            "query": "{\"query\":{\"bool\":{\"must\":[{\"match_phrase\":{\"Data.challanNo\":\"value\"}}]}}}",
            "targetReferences": [
                {
                    "fieldName": "challanNo",
                    "argument": "Data.challanNo",
                    "dataType": "String",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "challanNo"
                }
            ],
            "sourceReferences": [
                {
                    "fieldName": "consumerCode",
                    "argument": "Data.challanNo",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "challanNo"
                }
            ]
        },
        {
            "id": "7",
            "domain": "EXPENSE.OM",
            "indexName": "echallan-services",
            "documentType": "",
            "query": "{\"query\":{\"bool\":{\"must\":[{\"match_phrase\":{\"Data.challanNo\":\"value\"}}]}}}",
            "targetReferences": [
                {
                    "fieldName": "challanNo",
                    "argument": "Data.challanNo",
                    "dataType": "String",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "challanNo"
                }
            ],
            "sourceReferences": [
                {
                    "fieldName": "consumerCode",
                    "argument": "Data.challanNo",
                    "value": "$value",
                    "seperator": " ",
                    "expression": "challanNo"
                }
            ]
        }
```

[Click here to see the complete configuration.](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-ingest/DomainConfig.json)

### Topic Context Configuration

* Topic Context Configuration is an outline to define which data is received on which Kafka Topic.&#x20;
* Indexer Service and many other services are sending out data on different Kafka Topics. If the Ingest Service is asked to receive those data and pass it through the pipeline, the context and the version of the data being received has to be set. This configuration is used to identify as in which Kafka topic consumed the data and what is the mapping for that.

```
 "topicContextConfigurations": [
    {
      "topic": "dss-collection-update",
      "dataContext": "collection",
      "dataContextVersion": "v2"
    },
    {
      "topic": "topicTwo",
      "dataContext": "billing",
      "dataContextVersion": "v1"
    }
  ]
```

[Click here to see the complete configuration.](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-ingest/TopicContextConfiguration.json)&#x20;

Based on expense and water-service business service we added transfororm configurations as per below.

transform\_expense.electricity\_bill\_v1 Configuration: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">config-mgramseva/transform\_expense.electricity\_bill\_v1.json at QA · misdwss/config-mgramseva](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-ingest/transform\_expense.electricity\_bill\_v1.json)

transform\_expense.om\_v1 Configuration : [<img src="https://github.com/fluidicon.png" alt="" data-size="line">config-mgramseva/transform\_expense.om\_v1.json at QA · misdwss/config-mgramseva](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-ingest/transform\_expense.om\_v1.json)

transform\_expense.salary\_v1 Configuration: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">config-mgramseva/transform\_expense.salary\_v1.json at QA · misdwss/config-mgramseva](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-ingest/transform\_expense.salary\_v1.json)

transform\_ws\_v1 Configuration: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">config-mgramseva/transform\_ws\_v1.json at QA · misdwss/config-mgramseva](https://github.com/misdwss/config-mgramseva/blob/QA/egov-dss-dashboards/dashboard-ingest/transform\_ws\_v1.json)\


**Note:** For Kafka connect to work, Ingest pipeline application properties or in environments direct push must be disabled.

* `es.push.direct=false`
* If DSS collection index data is indexing directly ( without Kafka connector) to ES through the ingest pipeline then, make the application properties or in environments, direct push must be enabled.\
  `es.push.direct=true`

### **Creating a Kafka sync connector to push the data to the Elasticsearch**

* Configure the Kafka topics in the environments or Ingest pipeline application properties as shown below.

Kafka connection and re-indexing is available in this documentation. Please check from here. [mGramseva- Services Re-Indexing](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2024735035)

## **Dashboard Service Changes**

**Main-Monthly Dashboard**\
For the main monthly dashboard, we are using the service API to fetch the data and to show it in the main monthly dashboard table.\
**Ws-services:**\
`/ws-services/wc/_revenueCollectionData` Should be added to get the main monthly dashboard details. It is used to show the table data based on the no of months for selected financial year.

**eChallan-Service:**

`/echallan-services/eChallan/v1/_chalanCollectionData` it is added to get the main monthly dashboard data for the expense.

**Dashboard-Metrix:**

To show the data in metrix format in specific month dashboard we are using service API which will fetch the data based on dash board type.

**Ws-services:**\
`/ws-services/wc/_revenueDashboard` Should be added to get the revenue dashboard metrix data. It will show the data of revenue collections information

**eChallan-Service:**

`/echallan-services/eChallan/v1/_expenseDashboard` Is added in echallan-service to show the data of expenses in metrix format.\
MDMS- changes for the dashboard:

### Actions & Role Action Mapping

### **Actions**

```
[
 {
      "id": {{PLACEHOLDER1}},
      "name": " feedback search",
      "url": "/ws-services/wc/_revenueDashboard",
      "parentModule": "",
      "displayName": "get Revenue Dashboard Data",
      "orderNumber": 2,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER2}},
      "name": " feedback search",
      "url": "/ws-services/wc/_revenueCollectionData",
      "parentModule": "",
      "displayName": "get Revenue Dashboard Data",
      "orderNumber": 2,
      "enabled": false,
      "serviceCode": "ws-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER3}},
      "name": "Expense Update",
      "url": "/echallan-services/eChallan/v1/_expenseDashboard",
      "parentModule": "",
      "displayName": "get Expense Dashboard",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "echallan-services",
      "code": "null",
      "path": ""
    },
 {
      "id": {{PLACEHOLDER4}},
      "name": "Expense Update",
      "url": "/echallan-services/eChallan/v1/_chalanCollectionData",
      "parentModule": "",
      "displayName": "get Expense Dashboard",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "echallan-services",
      "code": "null",
      "path": ""
    },
      {
      "id": {{PLACEHOLDER5}},
      "name": "DSS Dashboard Charts",
      "url": "/dashboard-analytics/dashboard/getChartV2",
      "parentModule": "",
      "displayName": "DSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "DSS",
      "code": "null",
      "path": ""
     },
]



```

### **Role Action Mapping**

```
[
 
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER1}},
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
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER3}},
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
    },
    {
      "rolecode": "DASHBOARD_VIEWER",
      "actionid": {{PLACEHOLDER5}},
      "actioncode": "",
      "tenantId": "pb"
    }
]



```

### **Available Roles**

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

### Postman-collection for these dashboard**s**

| echallan-services/eChallan/v1/\_chalanCollectionData | [https://www.getpostman.com/collections/9724c55db3365b72c3e8](https://www.getpostman.com/collections/9724c55db3365b72c3e8) |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| echallan-services/eChallan/v1/\_chalanCollectionData | [https://www.getpostman.com/collections/9724c55db3365b72c3e8](https://www.getpostman.com/collections/9724c55db3365b72c3e8) |
| /ws-services/wc/\_revenueDashboard                   | [https://www.getpostman.com/collections/d79438f50b433917269d](https://www.getpostman.com/collections/d79438f50b433917269d) |
| /ws-services/wc/\_revenueCollectionData              | [https://www.getpostman.com/collections/d79438f50b433917269d](https://www.getpostman.com/collections/d79438f50b433917269d) |
| /dashboard-analytics/dashboard/getChartV2            | [https://www.getpostman.com/collections/119ee90dd54c04617c3a](https://www.getpostman.com/collections/119ee90dd54c04617c3a) |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

\
