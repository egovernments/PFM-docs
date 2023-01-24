# iFIX Adapter Master Data Service

## Overview <a href="#overview" id="overview"></a>

Adapter master data service maintains information on Department, Expenditure and Projects. We can create these details and search for the same details based on the given parameters/request data.

### Version <a href="#version" id="version"></a>

Current version : 1.0.0

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

Before we proceed with the configuration, make sure the following pre-requisites are met

1. Java 8
2. MongoDB instance
3. Required service dependency - Department entity service

## Features <a href="#features" id="features"></a>

It creates secure endpoints for the master data service. The access token is required to create any master data. The subsequent sections on this page discuss the service details maintained by the master data service.

### Department <a href="#department" id="department"></a>

Maintains the create and search department details. The following information is passed while creating the department - the Government ID, department code, department name, parent department if any. Searching the department details is on given parameters like IDs, Government ID, department code, department name.

### **API List**

| **Title**               | **Link**                                                                                                                   |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| /department/v1/\_create | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |
| /department/v1/\_search | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |

### Expenditure <a href="#expenditure" id="expenditure"></a>

Maintains the expenditure details And provide create and search functionality. For creating the expenditure, the following details are required - the Government ID, the department ID, code, name, type (can be "SCHEME", "NON\_SCHEME") details. While searching the expenditure details, pass the given parameters like IDs, Government IDs, names, code.

### **API List**

| **Title**                | **Link**                                                                                                                   |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| /expenditure/v1/\_create | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |
| /expenditure/v1/\_search | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |

### Project <a href="#project" id="project"></a>

Maintains the project details and provide create and search functionality. The following details are required to create the project - Government, name, code, expenditure ID, the department entity ID(s), location IDs. While searching, pass the IDs, Government ID, name, code, expenditure ID, location ID.

### **API List**

| **Title**            | **Link**                                                                                                                   |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| /project/v1/\_create | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |
| /project/v1/\_search | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |

## Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

![](<../../../.gitbook/assets/Adapter Master Data Service - seq diag.png>)

## Environment <a href="#environment" id="environment"></a>

No environment-specific variables are required for the environment (migration).

## Configurations and Setup <a href="#configurations-and-setup" id="configurations-and-setup"></a>

Update the DB and URI configurations in the dev.yaml, qa.yaml, prod.yaml file.

## References and Notes <a href="#references-and-notes" id="references-and-notes"></a>

| **Title**          | **Link**                                                                                                                                                                                                                                                         |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Swagger Yaml       | [ReDoc Interactive Demo](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/egovernments/iFix-Dev/develop/domain-services/ifix-master-data-service/ifix-master-data-service-1.0.0.yaml#tag/COA/paths/\~1chartOfAccount\~1v1\~1\_search/post) |
| Postman collection | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650)                                                                                                                                       |

## Master Project API With Example <a href="#master-project-api-with-example" id="master-project-api-with-example"></a>

Project Create API creates the project when the Master data details (COA, Government, Expenditure, Department) and Department Entity have been created. COA And Government have to be created in iFIX core Master data service.

Project Create API takes the below attributes in request :

1. tenantId: This is the Id that will be defined while creating the Ifix core Master Government Service.
2. expenditureId: This is the Id that will be generated while creating the Adapter Master Expenditure Service.
3. code: This is the project code that needs to be created.
4. name: This is the project name that needs to be created.
5. departmentEntityIds:  This is the Department Entity Ids. If we have to create a project at hierarchy level 1 then we need to pass the Department Entity Id of that corresponding level. It depends on the Department hierarchy level on which the project has to be created and hence the same level Department Entity [Id.](http://id.at/) You can pass a list of departmentEntityIds and can create the same project.

For reference, Below is a Dummy project create example:

Request :&#x20;

```
{
  "requestHeader": {
    "ts": 1627193067,
    "version": "2.0.0",
    "msgId": "Unknown",
    "signature": "NON",
    "userInfo": {
        "uuid": "e4fd96e8-3b6b-4e36-9503-0f14a01af39d"
    }
  },
  "project": {
    "tenantId": "pb",
    "code": "7330_S557_DIV23SD02",
    "name": "DOLOWAL UPPER",
    "expenditureId": "13ef1c53-702d-43b5-9f97-43fa03c145c5",
    "departmentEntityIds":  ["295180a0-4d60-4805-a77f-92143bd115b4","901f76a8-1911-4960-b389-57b62bd4dcdb"
    ]
  }
}


```

Response:

```
{
    "responseHeader": {
        "ts": 1627193067,
        "correlationId": null,
        "msgId": "Unknown",
        "status": "successful",
        "signature": "NON",
        "version": "2.0.0"
    },
    "project": [
        {
            "id": "1fb13f0a-588f-476d-b839-afddae7980ef",
            "tenantId": "pb",
            "code": "7330_S557_DIV23SD02",
            "name": "DOLOWAL UPPER",
            "expenditureId": "13ef1c53-702d-43b5-9f97-43fa03c145c5",
            "departmentEntityIds": [
                "295180a0-4d60-4805-a77f-92143bd115b4",
                "901f76a8-1911-4960-b389-57b62bd4dcdb"
            ],
            "locationIds": null,
            "auditDetails": {
                "createdBy": "e4fd96e8-3b6b-4e36-9503-0f14a01af39d",
                "lastModifiedBy": "e4fd96e8-3b6b-4e36-9503-0f14a01af39d",
                "createdTime": 1646726943845,
                "lastModifiedTime": 1646726943845
            }
        }
    ]
}
```

&#x20;

&#x20;

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
