# Department Entity Service Promotion

Department Entity service manages the department and its hierarchies metadata. It deals with department entities and department hierarchy only. Department Entity and Department Hierarchy were earlier in the iFIX core. Now, they have been moved to the mGramSeva iFIX adapter side. This page provides details on how to migrate that data from iFIX DB to mGramSeva iFIX adapter DB.

## Steps To Migrate

1. Create (if it's not available) DB schema (Mongo) in mgramseva namespace.
2. Create (if it's not available) DB schema (Mongo) in mgramseva namespace.
3. We can drop unused collections from iFix DB using the below steps :
   1.  &#x20;Connect to ifix namespace playground pod&#x20;

       &#x20;      `kubectl exec -it <playground-pod-name> -n ifix -- /bin/bash`
   2.  Connect to the particular mongo db

       &#x20;       `mongo --host <hostname>:27017 -u <username> -p <password>`
   3.  Use db

       &#x20;       `use  <db_name>`
   4.  Check the above-mentioned collection name using the below commands

       &#x20;      `db.getCollectionNames();`
   5.  If above mentioned (highlighted in bold) collections are there then drop them off using below commands

       &#x20;        `db.departmentEntity.drop();`

       &#x20;        `db.departmentHierarchyLevel.drop();`

## Steps To Use Department Entity Service&#x20;

Port-forward the Department Entity service in localhost from a specific environment (like QA/UAT/Prod). Below is the command to port-forward :

&#x20;   `kubectl port-forward <pod-name> 8032:8080 -n mgramseva`

## **Technical Doc**

#### ****[Department Entity Service v2.0](department-entity-service-promotion.md#inlinecard-hardbreak) <a href="#inlinecard-hardbreak" id="inlinecard-hardbreak"></a>

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
