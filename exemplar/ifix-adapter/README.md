# iFIX Adapter

## Overview

iFIX Adapter enables existing or new source systems to integrate seamlessly with iFIX. iFIX Adapter has been developed as a reference implementation for developers of source systems who want to integrate their departmental system with iFIX.&#x20;

iFix Adapter works as a mediator between iFIX and its clients. This system will receive requests from the client system and converts the data into the iFIX fiscal event or associated formats.&#x20;

## Pre-requisites <a href="#pre-requisites." id="pre-requisites."></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* PSQL server is running
* Redis
* Following services should be up and running:
  * Client Service Like mgramseva-ifix-adapter
  * Target service IFIX- fiscal-event-service
  * Target Service IFIX-keycloak

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* iFIX client requests pushed to IFIX
* Auth token is fetched from keycloak and cached. Token will be re-fetched 5 minutes before expiry
* Every push to iFIX is recoded with http status
  * status series 200 series considered success
  * status 400 are marked client error and reported back to client
  * status 500 resubmitted by scheduler

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Update the keycloak credentials client-id and secrets in the environment file
2. Map the coa in HeadCodeToCoaMapping.yml
3. Map project in ProjectMapping.yml
4. Deploy the latest version of ifix-reference-adapter

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

1. Update Key cloak credentials in dev.yaml, qa.yaml, prod.yaml according to environment

## Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

![](<../../.gitbook/assets/image (41).png>)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
