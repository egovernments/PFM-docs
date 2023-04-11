# iFIX Core Release Notes

## Release Summary <a href="#release-summary" id="release-summary"></a>

iFIX Core v2.0 contains the following changes.

* Removed project and department entity dependency from iFIX Fiscal Event Service.
* Removed project, department, expenditure dependency from iFIX Master Data Service.
* Removed project and department entity dependency from iFIX Fiscal Event Post Processor.
* Updated the Unit test cases.

## Enhancements <a href="#enhancements" id="enhancements"></a>

| **Updated Feature**              | **Description**                                                                                                                                                                                                     |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| iFIX Fiscal Event Service        | Removed the project and department entity dependency from fiscal event service. Now, all the details of the project and department entity are part of “attributes” in the fiscal event bulk request.                |
| iFIX Fiscal Event Post Processor | Removed the project and department entity dependency from fiscal event post-processor service. Now, all the details of the project and department entity are part of “attributes” that get unbundled and flattened. |
| iFIX Master Data Service         | Removed project, department, expenditure dependency from iFIX Master Data Service and have been moved to Adapter Master Data service.                                                                               |
| Unit test cases                  | <p></p><p>Updated the Junit test cases for all the core service</p><ul><li>iFIX Master Data Service</li><li>Fiscal event service</li><li>Fiscal event post-processor</li></ul>                                      |

## Document Resources and Links <a href="#document-resources-and-links" id="document-resources-and-links"></a>

| **Technical Documents**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><a href="broken-reference">iFIX Core Architecture Overview</a></p><p><a href="../../configuration/services/master-data-setup/domain-services/">Domain Service</a>s</p><p><a href="../../configuration/services/master-data-setup/">iFIX Master Data Setup</a></p><p><a href="../../configuration/promotion-docs/fiscal-event-and-fiscal-event-post-processor-service-promotion.md">Fiscal Event And Fiscal Event Post-processor Service Promotion</a></p><p><a href="../../configuration/promotion-docs/master-data-service-promotion-doc.md">Master Data Service Promotion</a></p> |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

&#x20;
