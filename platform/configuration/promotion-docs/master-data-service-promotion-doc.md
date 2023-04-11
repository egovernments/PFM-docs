# Master Data Service Promotion Doc

## Adapter Master Data Service v1.0 And iFIX Master Data Service v2.0 <a href="#adapter-master-data-service-v1.0-and-ifix-master-data-service-v2.0" id="adapter-master-data-service-v1.0-and-ifix-master-data-service-v2.0"></a>

This page provides step-wise details on how to migrate Department, Project and Expenditure from iFix Master Data Service to Adapter Master Data Service.

### Steps To Migrate To The Master Data Service

1. Yaml configurations
   * Update "_mongo-db-username_", "_mongo-db-password_" and "_mongo-db-authenticated-uri_" in secrets db config in respective environment secret yaml file ([<img src="https://github.com/fluidicon.png" alt="" data-size="line">iFix-DevOps/mgramseva-qa-secrets.yaml at mgramseva · misdwss/iFix-DevOps](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/mgramseva-qa-secrets.yaml) ).
   * Update "_mongo-db-name_", "_mongo-db-host_" and "_mongo-db-url_" in egov-config of configmaps in respective environment yaml file ([<img src="https://github.com/fluidicon.png" alt="" data-size="line">iFix-DevOps/mgramseva-qa.yaml at mgramseva · misdwss/iFix-DevOps](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/mgramseva-qa.yaml) ).
   * Update "_adapter-master-data-service_" and "_ifix-department-entity-service_" in egov-service-host in respective environment yaml file ([<img src="https://github.com/fluidicon.png" alt="" data-size="line">iFix-DevOps/mgramseva-qa.yaml at mgramseva · misdwss/iFix-DevOps](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/mgramseva-qa.yaml) ).
2. Create a new DB in the MongoDB instance for these new services.
3. Next, create the same master data again in the new (mgramseva) database using the adapter-master-data-service's /\_create APIs.
4.  After restoring DB collections, drop the unused collections from the iFIX MongoDB.

    &#x20; Follow the steps below to drop the unused collections.

    1.  Connect to ifix namespace playground pod&#x20;

        `kubectl exec -it <playground-pod> -n ifix -- /bin/bash`
    2. Connect to the particular mongo db\
       `mongo --host <hostname>:27017 -u <username> -p <password>`
    3.  Use db

        `use  <db_name>`
    4.  Check the above-mentioned collection name using the below commands

        `db.getCollectionNames();`
    5.  If collections are there then drop them off using the below commands

        _e.g._

        `db.department.drop();`

        `db.expenditure.drop();`

        `db.project.drop();`

### Steps To Use Adapter Master Data Service

Port-forward the Adapter master data service in localhost from a specific environment (like QA/UAT/Prod).

Below is the command to port-forward :

_e.g._

`kubectl port-forward <pod-name> 8030:8080 -n mgramseva`

### Steps To Use iFix Master Data Service

We need the access token from keycloak server and pass it as a bearer token while requesting the ifix-master-data-service create APIs.

### &#x20;Technical Docs

[Adapter Master Data Service v1.0](../../../exemplar/ifix-adapter/adapter-service-configuration/ifix-adapter-master-data-service.md)

[IFIX Core Master Data Service v2.0](../services/master-data-setup/domain-services/ifix-core-master-data-service.md)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
