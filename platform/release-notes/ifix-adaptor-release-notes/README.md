# iFIX Adaptor Release Notes

## Release Summary <a href="#release-summary" id="release-summary"></a>

MGramSeva iFix Adapter v2.2.0 has the below changes.

* It supports PSPCL events and works as bridge between iFix service and mGramSeva service.
* It fetches PSPCL events from iFix fiscal event service and pushes to mGramSeva service.

## Enhancements <a href="#enhancements" id="enhancements"></a>

| **Updated Feature**           | **Description**                                                                                                                  |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| PSPCL Event Identification    | It collects only PSPCL events with has been tagged by _PSPCL Adapter_ (before iFix core service)                                 |
| Duplicate events rejection    | It identifies which event has been processed before and segregate only those which are newly generated.                          |
| It supports its own Cron job. | It doesn’t rely on the system environment Cron time interval. It has own time interval which is being used for event collection. |
| Event type process            | It identifies event type (PSPCL event), based on that it trigger different processes.                                            |

## Document Resources and Links <a href="#document-resources-and-links" id="document-resources-and-links"></a>

| **Technical Documents**                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [MGramSeva iFix Adapter Service (PSPCL Enhancement)](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2203844609/MGramSeva+iFix+Adapter+Service+PSPCL+Enhancement) |
| [PSPCL iFix Adapter](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/2174681125/PSPCL+iFix+Adapter)                                                               |



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
