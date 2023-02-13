# iFix Department Entity Service

## Overview

Department Entity service manages the department and its hierarchies metadata. It deals with department entity and department hierarchy only. Department Hierarchy store only hierarchies definition like metadata for department level and department entity stores actual department data with its ancestry information.

### Version History

Current Version: 2.0.0

## Prerequisites

Before you proceed with the configuration, make sure the following pre-requisites are met.

1. Java 8
2. MongoDB instance
3. Required Service Dependencies - Adapter-Master-Data-Service

## Features

### Department Hierarchy

It defines the hierarchy definition for the department.

* department id: It is the ID of the department from the department master
* level: It defines the depth of hierarchy of department-level
* parent: It provides details about department hierarchy parent (UUID)

### **Level Value Evaluation**

1. Root level department hierarchy should not contain any parent value and the level value will be zero
2. When parent ID is having any value then we search parent in the department hierarchy record for hierarchy level evaluation.
3. Get level value from the parent department hierarchy and increment the current department hierarchy level value by one.

### Department Entity

It contains department entity information along with its hierarchy level and also attaches master department information (department id - UUID). It keeps all child level information lists at every department node (department record). Leaf level department does not have any children info.\
Child list contains department entity ID list, which makes the current department entity parent of all children list (department ID list). This is how it maintains the department entity level.

### Hierarchy Level Approach

Define the hierarchy level using the top to bottom because it has the parent's references. For department entity, create using the bottom-to-top approach. The leaf department entity does not have any child reference. When the department entity goes higher (parent) only then does it defines child reference in its child list.

### Department Hierarchy Request Action

1. **Create Department Hierarchy:**\
   We pass the current hierarchy level and its parent details along with master department and tenant information. It stores data as meta-information about hierarchy level for department entity data processing, it works as a reference meta index which will tell about hierarchy level information.
2. **Search Department Hierarchy:**\
   It just provides a preview of department hierarchies by providing request parameters - tenant ID, hierarchy level or department hierarchy ID.

### **API List**

| **Title**                                      | **Link**                                                                                                                   |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
|  `/departmentEntity/hierarchyLevel/v1/_create` | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |
|  `/departmentEntity/hierarchyLevel/v1/_search` | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650) |

### Department Entity Request Action

1. **Create Department Entity:**\
   It passes tenant Id, master department id, hierarchy level, its children list with department entity name and code. Tenant, hierarchy level and the master department is root info about the department entity. If the department entity does not contain any child, that means it is a leaf department entity it can only seek for its parent.
2. **Search Department Entity:**\
   It can make search requests based on any department entity attribute but can't skip tenant information, it returns the whole department entity details along with its child information. It finds all ancestry information of the current department entity.

### **API List**

| **Title**                       | **Link**                                                                                                                                           |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
|  `/departmentEntity/v1/_create` | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650)                         |
|  `/departmentEntity/v1/_search` | <p><a href="https://www.getpostman.com/collections/9891831cac4dad92a650">	<br>https://www.getpostman.com/collections/9891831cac4dad92a650</a></p> |

## Interaction Diagram

![](<../../../.gitbook/assets/Adapter Department Entity service - seq diag.png>)

## Environment

There will not be any environment variables required specific to the environment (migration).

## Configurations and Setup

1. Update the DB and URI configurations in the dev.yaml, qa.yaml, prod.yaml file.

## References and Notes

| **Title**          | **Link**                                                                                                                                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Swagger Yaml       | [ReDoc Interactive Demo](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/egovernments/iFix-Dev/develop/domain-services/ifix-department-entity-service/ifix-department-entity-service-1.0.0.yaml) |
| Postman collection | [https://www.getpostman.com/collections/9891831cac4dad92a650](https://www.getpostman.com/collections/9891831cac4dad92a650)                                                                                              |

## Department Hierarchy API With Example <a href="#department-hierarchy-api-with-example" id="department-hierarchy-api-with-example"></a>

Department Hierarchy defines the definition(Meta- Data) for actual department entity creation.

![](<../../../.gitbook/assets/1 (1).png>)

In the above image, the second row contains the actual Department Entities. Department Entity Create API - follows **Bottom to Up** approach.

In the above example data, the very first Department Entity will be created for  “BARUWAL” with code “7278”. Below are the Steps to create Department Entity :

* [x] The first Department Entity will be created for “BARUWAL” (Since the  Department Hierarchy has been defined from “Department” to “GPWSC”. Please refer [Department-Hierarchy-API-With-Example](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2072936577/Department+Entity+Service+v2.0#Department-Hierarchy-API-With-Example).)
* [x] The details that need to be passed in Department Entity Create API is -
  * tenantId: This will be from **Ifix Master Data Service**
  * departmentId: This will be from **Adapter Master Data Service**
  * code: For the first Department Entity, as per the above data image, it is “7278”
  * name: For the first Department Entity, as per the above data image, it is “BARUWAL”
  * hierarchyLevel:  For the first Department Entity, as per the above data image and defined    Department Hierarchy, It will be “6”.(Bottom to Up)
  * children:  For the first Department Entity, as per the above data image, it will be an empty set
* [x] For the next Department Entity Creation - repeat step 2 by making sure the subsequent request has - next Department Entity - Code, name, hierarchyLevel (this will decrement by one for every next Department entity), children (this will contain all or at least one previously created Department Entity Id(s)).

For reference, the Bottom to Up request & response of Department Entity Create API will look like :

Request :\[For Department Entity at Bottom - “**BARUWAL**”]

```
 {
    "requestHeader": {
    "ts": 1627193067,
    "version": "V1",
    "msgId": "Unknown",
    "signature": "NON",
    "userInfo": {
        "uuid": "e4fd96e8-3b6b-4e36-9503-0f14a01af39d"
    }
  },      
  "departmentEntity": {
    "tenantId": "pb",
    "departmentId": "3d9ef18a-361a-40cf-b142-dd6f998e1ad2",
    "code": "7278",
    "name": "BARUWAL",
    "hierarchyLevel": 6,
    "children": []
  }
  }

```

Response:

```
{
    "responseHeader": {
        "ts": 1627193067,
        "correlationId": "4f3d17a1-9608-4471-8fb0-dda7d02e79e8",
        "msgId": "Unknown",
        "status": "successful",
        "signature": "NON",
        "version": "V1"
    },
    "departmentEntity": [
        {
            "id": "7bdf9514-e2e5-4563-bfea-f5aaa41b2137",
            "tenantId": "pb",
            "departmentId": "3d9ef18a-361a-40cf-b142-dd6f998e1ad2",
            "code": "7278",
            "name": "BARUWAL",
            "hierarchyLevel": 6,
            "auditDetails": {
                "createdBy": "4faa912d-d531-485b-ad9b-0a9878f792b0",
                "lastModifiedBy": "4faa912d-d531-485b-ad9b-0a9878f792b0",
                "createdTime": 1637563256539,
                "lastModifiedTime": 1637563256539
            },
            "children": []
        }
    ]
}

```

Subsequent Request: \[For Department Entity - “**Kiratpur Sahib**”]

```
 {
    "requestHeader": {
    "ts": 1627193067,
    "version": "V1",
    "msgId": "Unknown",
    "signature": "NON",
    "userInfo": {
        "uuid": "e4fd96e8-3b6b-4e36-9503-0f14a01af39d"
    }
  },      
  "departmentEntity": {
    "tenantId": "pb",
    "departmentId": "3d9ef18a-361a-40cf-b142-dd6f998e1ad2",
    "code": "S557",
    "name": "Kiratpur Sahib",
    "hierarchyLevel": 5,
    "children": [
      "7bdf9514-e2e5-4563-bfea-f5aaa41b2137"  //This will be the previously created Department Entity Id(“BARUWAL”).
    ]
  }
  }

```

Response:

```
{
    "responseHeader": {
        "ts": 1627193067,
        "correlationId": "aba27b23-e5ab-4b64-a634-942553393f2a",
        "msgId": "Unknown",
        "status": "successful",
        "signature": "NON",
        "version": "V1"
    },
    "departmentEntity": [
        {
            "id": "7ae82e0e-5575-4fac-9b39-d12eead75c65",
            "tenantId": "pb",
            "departmentId": "3d9ef18a-361a-40cf-b142-dd6f998e1ad2",
            "code": "S557",
            "name": "Kiratpur Sahib",
            "hierarchyLevel": 5,
            "auditDetails": {
                "createdBy": "ba28ebe8-ed9c-4cdb-9328-b8e227eb0342",
                "lastModifiedBy": "ba28ebe8-ed9c-4cdb-9328-b8e227eb0342",
                "createdTime": 1631122344993,
                "lastModifiedTime": 1631122344993
            },
            "children": [
                "7bdf9514-e2e5-4563-bfea-f5aaa41b2137"
            ]
        }
    ]
}

```

And so on for the next Department Entity(ies) ...

**Note:** Below is the observation from the above example :

1. **Tenant Id** and **Department Id** will be created before creating the Department Entity hence before Department Hierarchy Create. Tenant Id and Department Id will be the same in all hierarchy levels for a Single Department Hierarchy and corresponding Department Entity(ies).
2. In the **children** attribute, we can pass a set of previous Department Entity Ids (or at least one **or** empty in case of Bottom level Department Entity).

### Update Existing Children List  <a href="#update-existing-children-list" id="update-existing-children-list"></a>

When we have to update the existing children list of Department Entity then update the existing children list using mongodb command like below

* Find the parent department entity where the new children need to be added. We should know which is the parent Department Entity beforehand. For the same, Do search by name and hierarchy level and find the corresponding parent department entity’s id (UUID).

```
db.departmentEntity.find({"name" : "<parent_department_entity's_name>","hierarchyLevel": <parent_department_entity_hierarchy_level>});
```

*   Append the department entity id at the end of the parent department entity children's list that we got from step 1. And count the length of the parent department entity children’s list (it is 0 based indexing ) that we are calling as ‘n’ here (it could be any integer number as per the children’s list size ) and then set it as

    "children.n": "\<picked\_from\_step\_1\_query\_department\_entity\_id>"

    &#x20;    _e.g._&#x20;

```
 db.departmentEntity.update({"_id": "<new_child_department_entity_id>"},{$set:
      {"children.n": "<Resulted_department_entity_id_1>",
      "children.n+1": "<Resulted_department_entity_id_2>"}
      })

```

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
