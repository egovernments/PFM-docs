# iFIX Core Fiscal Event Post-Processor

## Overview <a href="#overview" id="overview"></a>

Fiscal Event Post Processor is a streaming pipeline for validated fiscal event data. Apache Kafka has been used to stream the validated fiscal event data, process it for dereferencing, unbundle, flatten, and finally push these details to the Druid data store.

### Version  <a href="#version" id="version"></a>

Current version : 2.0.0

## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met:

1. Java 8
2. Apache Kafka and Kafka-Connect server should be up and running
3. Druid DB should be up and running
4. Below dependent services are required:\
   iFix Master data service\
   iFix Fiscal Event service

## Features <a href="#features" id="features"></a>

Fiscal Event post-processor consumes the fiscal event validated data from Kafka topic named “fiscal-event-request-validated” and processes it by following the below steps:

1. Fiscal event validated data gets dereferenced. For dereferencing, service ids like COA id, Tenant id etc. are passed to corresponding services - master service and fetch the corresponding object(s). Once the fiscal event data is dereferenced, push/send the same data to the dereferenced Topic.
2. Unbundle consumers pick up the dereferenced fiscal event data from the dereferencing topic. Dereference fiscal event data gets unbundled and then flattened. Once the flattening is complete, push/send the same data to the Druid Sink topic.
3. Flattened fiscal event data is pushed to Druid DB from a topic named: fiscal-event-druid-sink.

## Kafka to Data Store Sink <a href="#kafka-to-data-store-sink" id="kafka-to-data-store-sink"></a>

### MongoDB Sink <a href="#mongodb-sink" id="mongodb-sink"></a>

The Kafka-connect is used to push the data from a Kafka topic to MongoDB. Follow the steps below to start the connector.

1. Connect (port-forward) with the Kafka-connect server.
2. Create a new connector with a POST API call to localhost:8083/connectors.
3. The request body for that API call is written in the file [fiscal-event-mongodb-sink](https://github.com/misdwss/iFix-Dev/blob/master/domain-services/fiscal-event-post-processor/fiscal-event-mongodb-sink.json).
4. Within that file, wherever ${---} replace it with the actual value based on the environment. Get ${mongo-db-authenticated-uri} from the configured secrets of the environment.\
   (Optional) Verify and make changes to the topic names.
5. The connector is ready. You can check it using API call GET localhost:8083/connectors.

### Druid Sink <a href="#druid-sink" id="druid-sink"></a>

The Druid console is used to start ingesting data from a Kafka topic to the Druid data store. Follow the steps below to start the Druid Supervisor.

1. Open the Druid console
2. Go to the Load Data section
3. Select Other
4. Click on Submit Supervisor
5. Copy...Paste the JSON from the [druid-ingestion-config.json](https://github.com/misdwss/iFix-Dev/blob/master/domain-services/fiscal-event-post-processor/druid-ingestion-config.json) file in the available text box.
6. Verify the Kafka topic name and the Kafka bootstrap server address before submitting the config
7. Submit the config and the data ingestion should start into the fiscal-event data source

## Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

![](<../../../../../.gitbook/assets/Fiscal Event Processing Piepline-Post-Processor.drawio (1).png>)

## Environment

_**Note**: Kafka topic needs to be configured with respect to the environment_



| **Key**                                    | **Value**                           | **Description**                                               | **Remarks**                                                                             |
| ------------------------------------------ | ----------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `fiscal-event-kafka-push-topic`            | `fiscal-event-request-validated`    | Fiscal event post processor will consume data from this topic | Kafka topic should be same as configured in Fiscal event service.                       |
| `fiscal-event-kafka-dereferenced-topic`    | `fiscal-event-request-dereferenced` | Dereferenced fiscal event data will be pushed to this topic   | NA                                                                                      |
| `fiscal-event-kafka-flattened-topic`       | `fiscal-event-line-item-flattened`  | NA                                                            | NA                                                                                      |
| `fiscal-event-processor-kafka-druid-topic` | `fiscal-event-druid-sink`           | Flattened Fiscal Event data will be pushed to this topic.     | While druid ingest of fiscal event , make sure it has the same topic as mentioned here. |

## Configurations and Setup <a href="#configurations-and-setup" id="configurations-and-setup"></a>

Update the DB, Kafka producer & Consumer And URI configurations in the dev.yaml, qa.yaml, prod.yaml file.

## References and Notes <a href="#references-and-notes" id="references-and-notes"></a>

| **Title**    | **Link**                                                                                                                                                                                                                                                                                 |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Swagger Yaml | [<img src="https://github.com/fluidicon.png" alt="" data-size="line">iFix-Dev/fiscal-event-post-processor-2.0.0.yaml at develop · misdwss/iFix-Dev](https://github.com/misdwss/iFix-Dev/blob/develop/domain-services/fiscal-event-post-processor/fiscal-event-post-processor-2.0.0.yaml) |

&#x20;

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
