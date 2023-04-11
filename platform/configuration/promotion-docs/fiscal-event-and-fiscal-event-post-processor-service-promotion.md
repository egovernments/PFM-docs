# Fiscal Event And Fiscal Event Post-processor Service Promotion

The fiscal event post-processor receives a collection of fiscal event lists and after processing those events it pushes them to the Mongo DB and Druid DB. Before deploying the fiscal event post-processor build to the respective environment, make sure you have ingested the updated druid config file to the Druid DB as per the instructions given [here](https://github.com/misdwss/iFix-Dev/blob/master/domain-services/fiscal-event-post-processor/README.md).

## **Fiscal Events Data Clean up** <a href="#fiscal-events-data-clean-up" id="fiscal-events-data-clean-up"></a>

Before upgrading the iFIX fiscal event service v2.0, clean up the existing fiscal event data. This is a one-time activity. Follow the steps outlined in the [doc here](../services/ifix-core-data-cleanup.md).

## **Steps To Use iFIX Fiscal Event Service** <a href="#steps-to-use-ifix-fiscal-event-service" id="steps-to-use-ifix-fiscal-event-service"></a>

Get the access token from keycloak server and pass it as a bearer token while requesting to iFIX fiscal event service.

## **Technical Doc** <a href="#technical-doc" id="technical-doc"></a>

[IFIX Core Fiscal Event Service v2.0](../services/master-data-setup/domain-services/ifix-core-fiscal-event-service.md)

[iFix Core Fiscal Event Post Processor v2.0](../services/master-data-setup/domain-services/ifix-core-fiscal-event-post-processor.md)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
