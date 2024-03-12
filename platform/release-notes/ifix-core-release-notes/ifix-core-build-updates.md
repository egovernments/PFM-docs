# iFIX Core Build Updates

With the iFIX v2.3-alpha update, some of the DIGIT core services also need to be deployed. The builds of the same are also listed below. These have been picked from DIGIT-v2.7.&#x20;

| Category                  | Services                    | Docker Artifact ID                                                                          | **Remarks**                                                                                                               |
| ------------------------- | --------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **IFIX Domain Services**  | IFIX Master Data Service    | <pre data-overflow="wrap"><code>ifix-master-data-service-db:develop-b3f4ff0-3
</code></pre> | <ul><li>Removed government master from the service</li><li>Migrated chart of account from MongoDB to PostgreSQL</li></ul> |
|                           | Fiscal Event Service        | <pre data-overflow="wrap"><code>fiscal-event-service-db:develop-4c14ba4-8
</code></pre>     | <ul><li>Move to DIGIT architecture</li></ul>                                                                              |
|                           | IFIX ES Pipeline            | <pre data-overflow="wrap"><code>ifix-es-pipeline:develop-2dc38e9-4
</code></pre>            | <ul><li>New kafka stream pipeline to transform data that will be stored in ES. </li></ul>                                 |
|                           | Fiscal Event Post Processor | <pre data-overflow="wrap"><code>fiscal-event-post-processor:develop-4c5c4f8-2
</code></pre> | <ul><li>Changes maintain compatibility with other updated services. </li></ul>                                            |
| **Frontend**              | DIGIT-UI                    | <pre data-overflow="wrap"><code>digit-ui:develop-f26305c-1
</code></pre>                    |                                                                                                                           |
| **Core Services**         | dashboard-analytics         | `dashboard-analytics:v1.1.7-1ffb5fa2fd-49`                                                  |                                                                                                                           |
|                           | egov-mdms-service           | `egov-mdms-service:v1.3.2-72f8a8f87b-12`                                                    |                                                                                                                           |
|                           | egov-indexer                | `egov-indexer:v1.1.7-f52184e6ba-25`                                                         |                                                                                                                           |
|                           | egov-localization           | `egov-localization:v2.5-log4j-12a9331b-2`                                                   |                                                                                                                           |
|                           | egov-persister              | `egov-persister:v1.1.4-72f8a8f87b-6`                                                        |                                                                                                                           |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

&#x20;
