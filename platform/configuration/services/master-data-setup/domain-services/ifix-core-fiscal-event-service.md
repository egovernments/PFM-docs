# iFIX Core Fiscal Event Service

## Overview <a href="#overview" id="overview"></a>

The Fiscal Event Service maintains the fiscal event flow activities of multiple projects. The root level entity is a tenant which is basically the State Government. The tenant has several projects that are tagged to multiple attributes like department, scheme, mission, department, hierarchy, etc.  All the entity information and COA (Chart of Account) are passed along with amount details which constitutes an array of fiscal event instances under the system.

### Version  <a href="#version" id="version"></a>

Current version : 2.0.0

## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met.

1. Java 8
2. MongoDB instance
3. Required Service Dependencies.
   1. iFIX-Master-Data-Service
   2. iFIX-Fiscal Event Post Processor
   3. Apache Kafka Server

## Features <a href="#features" id="features"></a>

This service provides two features - Push fiscal event data and search fiscal event data.

### Push fiscal event data <a href="#push-fiscal-event-data" id="push-fiscal-event-data"></a>

* It is a secure endpoint and user info details are required to access it.
* It receives fiscal detail along with mandatory tenant and project info under attributes detail in publish requests, which triggers the whole fiscal event process and forwards it to the post-process service.
* Before encompassing all entities, it checks for entities validation via iFix core Master Data Service.
* While we create any fiscal event instance in the system, we log ingestion time and event occurrence timestamp which makes event flow clear on timestamp activities.
* After processing all these activities, it passes fiscal event information to other fiscal event post-processor services for further processing by publishing fiscal data into the Kafka topic "fiscal-event-request-validated" and “fiscal-event-mongodb-sink“.
* It also responds to snapshots of enriched fiscal event data which can be used by the source system for reference or any further processing.

### Search fiscal Event Data <a href="#search-fiscal-event-data" id="search-fiscal-event-data"></a>

* It provides a search feature on the existing fiscal events which has been processed before by post-processor service and persisted into the MongoDB instance.
* We can mainly search on eventType, tenantId, referenceId and event time interval and in return we get enriched data (dereference with nested id details).

### API List <a href="#api-list" id="api-list"></a>

| <h4 id="title"><strong>Title</strong> </h4> | **Link**                                                                                                                   |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
|  `/events/v1/_push`                         | [https://www.getpostman.com/collections/1b2abbca3f6c290b57d9](https://www.getpostman.com/collections/1b2abbca3f6c290b57d9) |
|  `/events/v1/_search`                       | [https://www.getpostman.com/collections/1b2abbca3f6c290b57d9](https://www.getpostman.com/collections/1b2abbca3f6c290b57d9) |

## Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

![](../../../../../.gitbook/assets/Fiscal\_Event\_Sequence\_Diagram.PNG)

## Environment <a href="#environment" id="environment"></a>

_**Note:**_ _Kafka topic needs to be configured with respect to the environment_

| **Key**                          | **Value**                      | **Description**                                                                                                         |
| -------------------------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| fiscal-kafka-push-topic          | fiscal-event-request-validated | Once the fiscal event data will get validated and enriched , it will be published to this topic for further processing. |
| fiscal.event.kafka.mongodb.topic | fiscal-event-mongodb-sink      | Once the fiscal event data will get validated and enriched , push the details to mongo db sink                          |

## &#x20; Configurations and Setup

1. Update all the DB and URI configuration in the dev.yaml, qa.yaml, prod.yaml file.
2. Make sure the keycloak server is up and running And have been configured with the required client ID.

## References and Notes <a href="#references-and-notes" id="references-and-notes"></a>

| **Title**          | **Link**                                                                                                                                                                                              |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Swagger Yaml       | [ReDoc Interactive Demo](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/misdwss/iFix-Dev/ifix-2.0-alpha/domain-services/fiscal-event-service/fiscal-event-service-2.0.0.yaml) |
| Postman collection | [https://www.getpostman.com/collections/1b2abbca3f6c290b57d9](https://www.getpostman.com/collections/1b2abbca3f6c290b57d9)                                                                            |

&#x20;

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
