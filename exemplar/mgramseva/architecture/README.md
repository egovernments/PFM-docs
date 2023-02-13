# Architecture

mGramSeva is built on top of the [DIGIT ](https://docs.digit.org/)Platform. It consists of the following layers

1. [Front End](https://ifix.digit.org/exemplar/mgramseva/user-manual/mgramseva-ui)
2. Back End
   1. Core Services
      1. [User Service](https://ifix.digit.org/exemplar/mgramseva/user-manual/backend-services/user-service) (egov-user)
      2. [User OTP](https://ifix.digit.org/exemplar/mgramseva/user-manual/backend-services/mgramseva-user-otp) (user-otp)
      3. [Access Control](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/access-control-services) (access-control)
      4. [MDMS](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/mdms-services)
      5. [ID Generation Service](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/37060616/ID-Generation-Service) (id-gen)
      6. [Payment Gateway](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/payment-gateway-services) (pg-service)
      7. [Workflow Service ](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/workflow-services)(wf-service)
      8. [Persister](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/37322761/Persister-Service)
      9. [Indexer](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/indexer-service)
      10. [Encryption Service ](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/5832708/Encryption+Service)(data-encryption-service)
      11. [Localization Service ](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/336920792/eGov-Localisation)(localization-service)
      12. [Boundary Service](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/location-services) (location-service)
      13. [URL Shortening Service](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/url-shortening-service) (url-shortening-service)
      14. [PDG Generation Service](https://docs.digit.org/configuration/configure-digit/services-overview/core-services/pdf-generation-services) (pdf-generator)
      15. [SMS Notifications](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/224919569/egov-notification-sms) (notification-sms)
      16. notification-email
      17. [Filestore](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/37060620/File-Store-Service)
      18. [API Gateway](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/36700192/API-Gateway)
   2. Business Services
      1. [Billing Service](https://ifix.digit.org/exemplar/mgramseva/user-manual/backend-services/billing-service)
      2. [Collection service](https://docs.digit.org/configuration/configure-digit/services-overview/business-services/collection-service/collection-service-v2)
      3. [Apportioning Service](https://docs.digit.org/configuration/configure-digit/services-overview/business-services/appropriation-service)
      4. [Dashboard Ingest](https://docs.digit.org/configuration/configure-digit/services-overview/business-services/dss-technical-documentation)
      5. [Dashboard Analytics](https://docs.digit.org/configuration/configure-digit/services-overview/business-services/dashboard-analytics-backend) (DSS)
   3. Municipal services:
      1. [Property Service ](https://docs.digit.org/product/modules/property-tax/property-tax-service)(property-services)
      2. [Water Service Calculator](https://ifix.digit.org/exemplar/mgramseva/user-manual/backend-services/water-service-calculator) (ws-calculator)
      3. [Water Service](https://ifix.digit.org/exemplar/mgramseva/user-manual/backend-services/water-services) (ws-service)
      4. [eChallan](https://ifix.digit.org/exemplar/mgramseva/user-manual/backend-services/e-challan-service) (echallan)
      5. [User Events](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/231407688/egov-user-events) (user-event)
      6. [Vendor](https://docs.digit.org/product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vendor-registry-v1.0)
      7. [IFIX Adaptor Integration Service](https://ifix.digit.org/exemplar/mgramseva/user-manual/backend-services/ifix-adapter-integration-service)

![mGramSeva Architecture Diagram](../../../.gitbook/assets/eGov\_MgramSeva\_Architecture.png)

## Services Architecture

The sequence diagram below illustrates a typical interaction between the various services.

![Sample sequence diagram for a typical flow of digit Microservices](<../../../.gitbook/assets/digit\_sequence\_diagram (1).png>)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
