# iFIX Adaptor Build Updates

With this update, the iFIX Adapter services now depend on some of the DIGIT Core services. egov-persister should be deployed and configured.&#x20;

| Category          | Services                       | Docker Artifact ID                                                                                    | **Remarks**                                                                                                                                                                                                                                        |
| ----------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IFIX Adaptor**  | IFIX Department Entity Service | <pre data-overflow="wrap"><code>ifix-department-entity-service-db:develop-5feea0e-2
</code></pre>     | <ul><li>Migrated database from MongoDB to PostgreSQL.</li><li><strong>Non-backward compatible update</strong> to the /_create and <em>/_</em>update APIs, to handle receive status updates in the children array.</li></ul>                        |
|                   | Adapter Master Data Service    | <pre data-overflow="wrap"><code>adapter-master-data-service-db:develop-93349a7-8
</code></pre><p></p> | <ul><li>Migrated database from MongoDB to PostgreSQL.</li><li><strong>Non-backward compatible update</strong> to the /_create and <em>/_</em>update APIs of Project, to handle receive status updates in the departmentEntityIds array. </li></ul> |



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
