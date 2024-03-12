# MongoDB Migration

As part of the iFIX-2.0-alpha release, we have migrated the following master data from ifix\_db to mgramseva\_db:

1. Adapter Master Data Service
   1. Department
   2. Expenditure
   3. Project
2. Department Entity Service
   1. Department Entity
   2. Department Hierarchy

Out of these, the project data SHOULD NOT be copied to the new DB because a new feature of the multi-tenant (GP) project is introduced with this release. New projects can be created and linked to multiple GPs.

Other master data can be copied.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Make sure the playground pod is “dwssio/playground:mongo-v2” or newer.
2. Keep the MongoDB Credentials handy in the following format
   * Host(in this format): “\<host-address>:27017”
   * Username - a user that has access to BOTH source and destination dbs
   * Password
   * Source and Destination DB Names
   * List of collection names to be copied
3.  The `mongo-migration.sh` script copied to the playground pod. (You must have necessary kube permissions to copy a file to a pod.)

    * Sample Command to copy the file:\
      `kubectl cp mongo_migration.sh ifix/<playground pod>:/`



<div align="left">

<img src="../../../.gitbook/assets/2 (1).jpg" alt="">

</div>

## Migration Instructions <a href="#migration-instructions" id="migration-instructions"></a>

A MongoDB Dump script is provided that will copy a list of collections from a source DB to the destination DB.

1. Execute the provided script using following parameters:
   * \-h = Host Address
   * \-u = username
   * \-p = password
   * \-s = source db
   * \-d = destination db
   * \-c = collection name - You can provide multiple collection as depicted in the following example
2. ./mongo-migration.sh -h \<host-address>[:27017](http://aws.com:27017/)  -u \<ifix username> -p \<ifix password> - s \<ifix db> -d \<mgramseva db> -c department -c expenditure -c departmentHierarchyLevel -c departmentEntity

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

&#x20;
