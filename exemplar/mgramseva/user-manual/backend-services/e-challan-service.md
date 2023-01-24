# mGramSeva e-Challan Service

## Overview

eChallan system enables employees to generate the challans for Adhoc services so that the payment can be recorded into the system along with service-specific details.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has workflow persister config path added in it
* PSQL server is running and a database is created to store workflow configuration and data

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Allow employees to capture service details for miscellaneous services and mark as paid
* Allow employees to update/cancel challan.

| **Environment Variables**              | **Description**                                                                |
| -------------------------------------- | ------------------------------------------------------------------------------ |
| `egov.user.event.notification.enabled` | This variable is to check the event Notification enabled or not.               |
| `egov.challan.default.limit`           | This variable is to get the default limit value                                |
| `egov.challan.max.limit`               | This variable to check the max limit value.                                    |
| `create.ws.workflow.name`              | This variable will give the business service name while creating the workflow. |
| `notification.sms.enabled`             | This variable is to check the SMS notifications are enabled or not.            |
| `egov.localization.statelevel`         | This variable is used to check the localizations are state level or not.       |
| `egov.pending.collection.link`         | variable for collection list screen link for notifications                     |
| `egov.monthly.summary.link`            | variable for monthly summary screen link for notifications                     |
| `egov.new.Expenditure.link`            | variable for new expenditure screen link                                       |
| `egov.mark.paid.Expenditure.link`      | variable for paid expenditure screen link                                      |
| `egov.bilk.demand.failed.link`         | variable for mnaul bulk demand generation screen link                          |
| `egov.today.collection.link`           | variable for today’s collection screen link                                    |

## Interaction Diagram

![](../../../../.gitbook/assets/image-20210915-033153.png)

### Configuration Details <a href="#configuration-details" id="configuration-details"></a>

_**MDMS Configuration**_\
\
Actions & Role Action Mapping

**Actions**

```
[
   {
      "id": {{PLACEHOLDER1}},
      "name": "Expense Create",
      "url": "/echallan-services/eChallan/v1/_create",
      "parentModule": "",
      "displayName": "EChallan Create",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "echallan-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER2}},
      "name": "Expense Search",
      "url": "/echallan-services/eChallan/v1/_search",
      "parentModule": "",
      "displayName": "EChallan Create",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "echallan-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER3}},
      "name": "Expense Update",
      "url": "/echallan-services/eChallan/v1/_update",
      "parentModule": "",
      "displayName": "EChallan Create",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "echallan-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER4}},
      "name": "Vendor Create",
      "url": "/vedor/v1/_create",
      "parentModule": "",
      "displayName": "Vendor Create",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "vendor",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER5}},
      "name": "Vendor Search",
      "url": "/vendor/v1/_search",
      "parentModule": "",
      "displayName": "Vendor Create",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "vendor",
      "code": "null",
      "path": ""
    },
     {
      "id": 2007,
      "name": "Update Password",
      "url": "/user/password/_update",
      "parentModule": "",
      "displayName": "Password Update",
      "orderNumber": 4,
      "enabled": false,
      "serviceCode": "ADMIN",
      "code": "null",
      "path": ""
    },
]


```

**Role Action Mapping**

```
[
  {
      "rolecode": "EXPENSE_PROCESSING",
      "actionid": {{PLACEHOLDER1}},
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
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EXPENSE_PROCESSING",
      "actionid": {{PLACEHOLDER3}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SUPERUSER",
      "actionid": {{PLACEHOLDER4}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EXPENSE_PROCESSING",
      "actionid": {{PLACEHOLDER4}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EXPENSE_PROCESSING",
      "actionid": {{PLACEHOLDER5}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SUPERUSER",
      "actionid": {{PLACEHOLDER5}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SUPERUSER",
      "actionid": {{PLACEHOLDER6}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "GP_ADMIN",
      "actionid": {{PLACEHOLDER6}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "COLLECTION_OPERATOR",
      "actionid": {{PLACEHOLDER6}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BULK_DEMAND_PROCESSING",
      "actionid": {{PLACEHOLDER6}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EXPENSE_PROCESSING",
      "actionid": {{PLACEHOLDER6}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "DASHBOARD_VIEWER",
      "actionid": {{PLACEHOLDER6}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "PROFILE_UPDATE",
      "actionid": {{PLACEHOLDER6}},
      "actioncode": "",
      "tenantId": "pb"
    },
]


```

Roles available

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

## Deployment Details

1. Add mdms configs required for eChallan Service and calculator and restart mdms service.
2. Deploy the latest version of eChallan Service and calculator.
3. Add eChallan Service persister yaml path in persister configuration and restart persister service
4. Add Role-Action mapping for API’s.
5. Add pdf configuration file for challan and bill.

## Integration

### Integration Scope

The eChallan service is used to generate **e-challans / bills** for all miscellaneous / adhoc services .

### Integration Benefits

* Can perform service-specific business logic without impacting the other module.
* Provides the capability of capturing the unique identifier of the entity for which the challan is generated.
* In the future, if we want to expose the application to citizens then it can be done easily.
* The workflow or Service-specific workflow can be enabled at the challan service level at any time without changing the design.
* Allow employees to update/cancel challan

### Steps to Integration

1. To integrate, the host of echallan-services module should be overwritten in helm chart.
2. `echallan-services/eChallan/v1/_create` should be added as the create endpoint for creating eChallan in the system.
3. `echallan-services/eChallan/v1/_search` should be added as the search endpoint. This method handles all requests to search existing records depending on different search criteria.
4. `echallan-services/eChallan/v1/_update` should be added as the update endpoint. This method is used to update fields in existing records or to update the status of application based on workflow.
5. `/echallan-services/eChallan/v1/_expenseDashboard` Is added in echallan-service to show the data of expenses in metrix format.
6. `/echallan-services/eChallan/v1/_chalanCollectionData` it is added to get the main monthly dashboard data for the expense.

## Reference Docs

### Doc Links

| **Title**                 | **Link**                                                                                                                                                       |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/docs/e-Challan-v1.0.0.yaml#!/) |

### API List

|                                                      | **Link**                                                                                                                   |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
|  _echallan-services/eChallan/v1/\_create_            | [https://www.getpostman.com/collections/9724c55db3365b72c3e8](https://www.getpostman.com/collections/9724c55db3365b72c3e8) |
| _echallan-services/eChallan/v1/\_update_             | [https://www.getpostman.com/collections/9724c55db3365b72c3e8](https://www.getpostman.com/collections/9724c55db3365b72c3e8) |
| _echallan-services/eChallan/v1/\_search_             | [https://www.getpostman.com/collections/9724c55db3365b72c3e8](https://www.getpostman.com/collections/9724c55db3365b72c3e8) |
| echallan-services/eChallan/v1/\_chalanCollectionData | [https://www.getpostman.com/collections/9724c55db3365b72c3e8](https://www.getpostman.com/collections/9724c55db3365b72c3e8) |
| echallan-services/eChallan/v1/\_chalanCollectionData | [https://www.getpostman.com/collections/9724c55db3365b72c3e8](https://www.getpostman.com/collections/9724c55db3365b72c3e8) |

_(Note: All the API’s are in the same postman collection therefore the same link is added in each row)_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
