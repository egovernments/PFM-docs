# mGramSeva- Services Re-Indexing

## Overview <a href="#overview" id="overview"></a>

We are using re-indexing to get all the data to the respective indexer. We have 2 steps for this. The first step is to run the connector from the playground, which is followed by legacyindexer service call from indexer service, which internally calls the respective plain search service to get the data and to send it to the respective indexer.

## **Prerequisites**

* Access to kubectl of the environment targetted
* Postman scripts
* Plain search apis in the respective services

We have mainly 3 indexes in mGramSeva for Re-indexing.

* Water-services
* Echallan-services
* dss-collection\_v2

### Steps to follow for re-indexing

*   **ws-services re-indexing**

    Kafka Connector Curl to be run from playground pod

```
curl --location --request POST 'http://kafka-connect.mgramseva:8083/connectors/' \
--header 'Cache-Control: no-cache' \
--header 'Content-Type: application/json' \
--header 'Postman-Token: 419e68ba-ffb9-4da9-86e1-7ad5a4c8d0b9' \
--data-raw '{
    "name": "water-services-enriched-es-sink",
    "config": {
        "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
        "type.name": "general",
        "tasks.max": "1",
        "max.retries": "15",
        "key.ignore": "false",
        "retry.backoff.ms": "5000",
        "max.buffered.records": "25",
        "value.converter": "org.apache.kafka.connect.json.JsonConverter",
        "errors.log.enable": "true",
        "key.converter": "org.apache.kafka.connect.storage.StringConverter",
        "read.timeout.ms": "100000",
        "topics": "water-services-enriched",
        "batch.size": "25",
        "max.in.flight.requests": "2",
        "schema.ignore": "true",
        "behavior.on.malformed.documents": "warn",
        "flush.timeout.ms": "3600000",
        "errors.deadletterqueue.topic.name": "water-services-enriched-failed",
        "errors.tolerance": "all",
        "value.converter.schemas.enable": "false",
        "name": "water-services-enriched-es-sink",
        "connection.url": "http://elasticsearch-data-v1.mgramseva:9200",
        "linger.ms": "1000",
        "transforms": "TopicNameRouter",
        "transforms.TopicNameRouter.type": "org.apache.kafka.connect.transforms.RegexRouter",
        "transforms.TopicNameRouter.regex": "water-services-enriched*",
        "transforms.TopicNameRouter.replacement": "water-services-enriched"
    }
}'

```

**Plain Search call**

```
curl --location --request POST 'http://localhost:8055/egov-indexer/index-operations/_legacyindex' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": null,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "authToken": "ca3256e3-5318-47b1-8a68-ffcf2228fe35",
        "correlationId": "e721639b-c095-40b3-86e2-acecb2cb6efb",
        "userInfo": {
            "id": 23299,
            "uuid": "e721639b-c095-40b3-86e2-acecb2cb6efb",
            "userName": "9337682030",
            "name": "Abhilash Seth",
            "type": "CITIZEN",
            "mobileNumber": "9337682030",
            "emailId": "abhilash.seth@gmail.com",
            "roles": [
                {
                    "id": 281,
                    "name": "Citizen"
                }
            ]
        }
    },
    "apiDetails": {
        "uri": "http://ws-services.mgramseva:8080/ws-services/wc/_plainsearch",
        "tenantIdForOpenSearch": "pb",
        "paginationDetails": {
            "offsetKey": "offset",
            "sizeKey": "limit",
            "maxPageSize": 25,
            "limit":25
        },
        "responseJsonPath": "$.WaterConnection"
    },
    "legacyIndexTopic": "ws-connection-legacyIndex",
    "tenantId": "pb"
}'

```

**EChallan -Reindexing**\
Kafka Connector Call to be run from Playground pod

```
curl --location --request POST 'http://kafka-connect.mgramseva:8083/connectors/' \
--header 'Cache-Control: no-cache' \
--header 'Content-Type: application/json' \
--header 'Postman-Token: 419e68ba-ffb9-4da9-86e1-7ad5a4c8d0b9' \
--data-raw '{
    "name": "echallan-services-enriched-es-sink",
    "config": {
        "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
        "type.name": "general",
        "tasks.max": "1",
        "max.retries": "15",
        "key.ignore": "true",
        "retry.backoff.ms": "5000",
        "max.buffered.records": "25",
        "value.converter": "org.apache.kafka.connect.json.JsonConverter",
        "errors.log.enable": "true",
        "key.converter": "org.apache.kafka.connect.storage.StringConverter",
        "read.timeout.ms": "100000",
        "topics": "echallan-services-enriched",
        "batch.size": "25",
        "max.in.flight.requests": "2",
        "schema.ignore": "true",
        "behavior.on.malformed.documents": "warn",
        "flush.timeout.ms": "3600000",
        "errors.deadletterqueue.topic.name": "echallan-services-enriched-failed",
        "errors.tolerance": "all",
        "value.converter.schemas.enable": "false",
        "name": "echallan-services-enriched-es-sink",
        "connection.url": "http://elasticsearch-data-v1.mgramseva:9200/",
        "linger.ms": "1000",
        "transforms": "TopicNameRouter",
        "transforms.TopicNameRouter.type": "org.apache.kafka.connect.transforms.RegexRouter",
        "transforms.TopicNameRouter.regex": "echallan-services-enriched*",
        "transforms.TopicNameRouter.replacement": "echallan-services-enriched"
    }
}'

```

Legacy Index call from postman

```
curl --location --request POST 'http://localhost:8055/egov-indexer/index-operations/_legacyindex' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": null,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "authToken": "ca3256e3-5318-47b1-8a68-ffcf2228fe35",
        "correlationId": "e721639b-c095-40b3-86e2-acecb2cb6efb",
        "userInfo": {
            "id": 23299,
            "uuid": "e721639b-c095-40b3-86e2-acecb2cb6efb",
            "userName": "9337682030",
            "name": "Abhilash Seth",
            "type": "CITIZEN",
            "mobileNumber": "9337682030",
            "emailId": "abhilash.seth@gmail.com",
            "roles": [
                {
                    "id": 281,
                    "name": "Citizen"
                }
            ]
        }
    },
    "apiDetails": {
        "uri": "http://echallan-services.mgramseva:8080/echallan-services/eChallan/v1/_plainsearch",
        "tenantIdForOpenSearch": "pb",
        "paginationDetails": {
            "offsetKey": "offset",
            "sizeKey": "limit",
            "maxPageSize": 25,
            "limit":25
        },
        "responseJsonPath": "$.challans"
    },
    "legacyIndexTopic": "echallan-legacyIndex",
    "tenantId": "pb"
}'

```

* **Dss collection v2 re-indexing**

Kafka Connector call to be run from playground pod

```
curl --location --request POST 'http://kafka-connect.mgramseva:8083/connectors/' \
--header 'Cache-Control: no-cache' \
--header 'Content-Type: application/json' \
--header 'Postman-Token: 419e68ba-ffb9-4da9-86e1-7ad5a4c8d0b9' \
--data-raw '{
  "name": "cms-case-es-sink9121",
  "config": {
    "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
        "connection.url": "http://elasticsearch-data-v1.mgramseva:9200",
    "type.name": "payments",
    "topics": "paymentsindex-v1-enriched",
    "key.ignore": "false",
    "schema.ignore": true,
    "value.converter.schemas.enable": false,
    "key.converter": "org.apache.kafka.connect.storage.StringConverter",
    "value.converter": "org.apache.kafka.connect.json.JsonConverter",
    "transforms": "TopicNameRouter",
    "transforms.TopicNameRouter.type": "org.apache.kafka.connect.transforms.RegexRouter",
    "transforms.TopicNameRouter.regex": ".*",
    "transforms.TopicNameRouter.replacement": "paymentsindex-v1",
    "batch.size": 10,
    "max.buffered.records": 500,
    "flush.timeout.ms": 600000,
    "retry.backoff.ms": 5000,
    "read.timout.ms": 10000,
    "linger.ms": 100,
    "max.in.flight.requests": 2,
    "errors.log.enable": true,
    "errors.deadletterqueue.topic.name": "paymentsindex-v1-es-failed",
    "tasks.max": 1
  }
}'

```

```
curl --location --request POST 'http://kafka-connect.mgramseva:8083/connectors/' \
--header 'Cache-Control: no-cache' \
--header 'Content-Type: application/json' \
--header 'Postman-Token: 419e68ba-ffb9-4da9-86e1-7ad5a4c8d0b9' \
--data-raw '{
    "name": "cms-case-es-sink9132",
    "config": {
        "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
        "connection.url": "http://elasticsearch-data-v1.mgramseva:9200",
        "type.name": "general",
        "topics": "egov-dss-ingest-enriched",
        "key.ignore": "false",
        "schema.ignore": true,
        "value.converter.schemas.enable": false,
        "key.converter": "org.apache.kafka.connect.storage.StringConverter",
        "value.converter": "org.apache.kafka.connect.json.JsonConverter",
        "transforms": "TopicNameRouter",
        "transforms.TopicNameRouter.type": "org.apache.kafka.connect.transforms.RegexRouter",
        "transforms.TopicNameRouter.regex": ".*",
        "transforms.TopicNameRouter.replacement": "dss-collection_v2",
        "batch.size": 10,
        "max.buffered.records": 500,
        "flush.timeout.ms": 600000,
        "retry.backoff.ms": 5000,
        "read.timout.ms": 10000,
        "linger.ms": 100,
        "max.in.flight.requests": 2,
        "errors.log.enable": true,
        "errors.deadletterqueue.topic.name": "dss-collection_v2-es-failed",
        "tasks.max": 1
    }
}'

```

payment re-indexing run from postman call

```
curl --location --request POST 'http://localhost:8055/egov-indexer/index-operations/_legacyindex' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": null,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "authToken": "b843ef27-1ac6-49b8-ab71-cd0c22f4e50e",
        "correlationId": "e721639b-c095-40b3-86e2-acecb2cb6efb",
        "userInfo": {
            "id": 23299,
            "uuid": "e721639b-c095-40b3-86e2-acecb2cb6efb",
            "userName": "9337682030",
            "name": "Abhilash Seth",
            "type": "EMPLOYEE",
            "mobileNumber": "9337682030",
            "emailId": "abhilash.seth@gmail.com",
            "roles": [
                {
                    "id": 281,
                    "name": "Employee"
                }
            ]
        }
    },
    "apiDetails": {
        "uri": "http://collection-services:8080/collection-services/payments/_plainsearch",
          "tenantIdForOpenSearch": "pb",
        "paginationDetails": {
            "offsetKey": "offset",
            "sizeKey": "limit",
            "maxPageSize": 50,
            "startingOffset": 150
        },
        "responseJsonPath": "$.Payments"
    },
    "legacyIndexTopic": "egov-payment-legacy-index",
    "tenantId": "pb"
}'

```

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
