# Migration Steps - Adapter

1. Deploy `ifix-migration-toolkit-db:develop-2557812-9` to `mgramseva` environment.&#x20;
2. Port forward to the ifix-migration-toolkit pod

#### Instruction

The following common request body is used to hit the ifix-migration-toolkit endpoints:

```
{
    "requestHeader": {}
    "tenantId": "<tenant-id>"
}
```

## Migrate ifix-department-entity-service

1. First, deploy the latest image of the ifix-department-entity-service
   1. (So that the tables get created in PostgreSQL.)
2.  Deploy plain search docker image of ifix-department-entity-service:

    ```
    egovio/ifix-department-entity-service-db:mongodb-plainsearch-b12bf24-4
    ```
3. Ensure [department-entity-persister.yml](https://github.com/egovernments/config-mgramseva/blob/QA/egov-persister/department-entity-persister.yml) is configured in the egov-persister.
4. (Ensure [department-entity-migration-progress](https://github.com/egovernments/config-mgramseva/blob/QA/egov-persister/department-entity-migration-progress.yml) is configured in egov-persister to record the progress of the migration. In case of any failures during migration, with this, it will resume the migration from where it left off. )
5.  Hit the Department Hierarchy migrate endpoint of the migration-toolkit&#x20;

    ```
    /ifix-migration-toolkit/department_hierarchy/v1/_migrate
    ```
6.  Hit the Department Entity migrate endpoint of the migration-toolkit&#x20;

    ```
    /ifix-migration-toolkit/department_entity/v1/_migrate
    ```

## Migrate adapter-master-data-service

1. First, deploy the latest image of the ifix-department-entity-service
   1. (So that the tables get created in PostgreSQL.)
2.  Deploy plain search docker image of ifix-department-entity-service:

    ```
    egovio/adapter-master-data-service-db:mongodb-plainsearch-b12bf24-5
    ```
3. Ensure [adapter-master-data-service.yml](https://github.com/egovernments/config-mgramseva/blob/QA/egov-persister/adapter-master-data-service.yml) is configured in egov-persister.
4.  Hit the Department migrate endpoint of the migration-toolkit&#x20;

    ```
    /ifix-migration-toolkit/department/v1/_migrate
    ```
5.  Hit the Expenditure migrate endpoint of the migration-toolkit&#x20;

    ```
    /ifix-migration-toolkit/expenditure/v1/_migrate
    ```
6.  Hit the Project migrate endpoint of the migration-toolkit&#x20;

    ```
    /ifix-migration-toolkit/project/v1/_migrate
    ```
