# Migration Steps - iFIX

1. Deploy `ifix-migration-toolkit-db:develop-b7a2050-13` to `ifix` environment
2. Port forward to the ifix-migration-toolkit pod

#### Instruction

The following common request body is used to hit the ifix-migration-toolkit endpoints:

```
{
    "requestHeader": {},
    "tenantId": "<tenant-id>"
}
```

## Migrate ifix-master-data-service

### Migrate Government

Government master data is moved to MDMS. Please manually copy the government(tenant) data to the `tenants` master of `tenant` module. Here is a link to a sample [tenants master](https://github.com/egovernments/mdms-mgramseva/blob/ifix-qa/data/pb/tenant/tenants.json).&#x20;

### Migrate Chart of Account

1. First, deploy the latest image of the ifix-master-data-service
   1. (So that the tables get created in PostgreSQL.)
2.  Deploy plain search docker image of ifix-master-data:&#x20;

    ```
    ifix-master-data-service-db:mongodb-plainsearch-b12bf24-7
    ```
3. Ensure [ifix-master-data-persister](https://github.com/egovernments/config-mgramseva/blob/ifix-qa/egov-persister/ifix-master-data-persister.yml) is configured in the egov-persister
4.  Hit the Chart of Account migrate endpoint of the migration-toolkit&#x20;

    ```
    /ifix-migration-toolkit/coa/v1/_migrate
    ```

## Migrate fiscal-event-service: Fiscal Events&#x20;

With this, we will be performing migration from MongoDB to both, PostgreSQL and ElasticSearch. Data will be read from MongoDB using fiscal-event-service's plain search api, and pushed to a kafka topic.&#x20;

1. From there, the data will reach PostgreSQL using egov-persister.&#x20;
2. From kafka-topic data will pass through ifix-es-pipeline. After that ifix-es-pipeline will post the processed data to the next kafka topic in the pipeline. From there, egov-indexer will read from the topic and index the data onto ElasticSearch.&#x20;

### Instructions:

1. First, deploy the latest image of the fiscal-event-service
   1. (So that the tables get created in PostgreSQL.)
2. Follow the instructions mentioned in the ifix-es-pipeline project's README to setup the ES mapping before performing the migration.&#x20;
3.  Deploy plain search docker image of fiscal-event-service:

    ```
    egovio/fiscal-event-service-db:mongodb-plainsearch-1bca621-7
    ```
4. Deploy the latest image of ifix-es-pipeline
5. Ensure [fiscal-events-persister](https://github.com/egovernments/config-mgramseva/blob/ifix-qa/egov-persister/fiscal-events-persister.yml) is configured in egov-persister
6. Ensure [ifix-fiscal-event-indexer](https://github.com/egovernments/config-mgramseva/blob/ifix-qa/egov-indexer/ifix-fiscal-event-indexer.yml) is configured in egov-indexer
7. (Ensure [ifix-migration-progress](https://github.com/egovernments/config-mgramseva/blob/ifix-qa/egov-persister/ifix-migration-progress.yml) is configured in egov-persister to record the progress of the migration. In case of any failures during migration, with this, it will resume the migration from where it left off. )
8.  Hit the Fiscal Event migrate endpoint of the migration-toolkit

    ```
    /ifix-migration-toolkit/fiscal_event/v1/_migrate
    ```
