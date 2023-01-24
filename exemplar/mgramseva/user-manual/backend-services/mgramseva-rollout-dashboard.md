# mGramSeva - Rollout Dashboard

**Objective**

The purpose of the mGramSeva Rollout Dashboard Scripts to aggregate the data points from mgramseva DB and services for Rollout dashboard in Metabase

## Overview <a href="#overview" id="overview"></a>

mGramSeva Rollout Dashboard is a python script for pushing the data from the mGramSeva to s a specific table in DB on a daily basis which can be loaded to Metabase and graphical dashboard built on top of this table in the Metabase.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Python 3.9_
* mGramSeva DB
* mGramseva user details who has access to MDMS service API
* mGramSeva mdms service access

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Collecting the data on certain data points and inserting the data into the rollout dashboard table in the DB\
  User Story with details of the data point: [![](https://digit-discuss.atlassian.net/images/icons/issuetypes/story.svg)IFIX-485: \[1.0.1\] Rollout Dashboards on MetabaseQA SIGNOFF](https://digit-discuss.atlassian.net/browse/IFIX-485)

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

Please deploy the following build.

* **rollout-dashboard-cronjob:develop-2a8d6a44-3**

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

mGramSeva Rollout Dashboard is not directly integrated with any of the services except this scripts fetch the data from the MDMS service and mGramSeva DB

1. Configure the username, tenantId and password of the user for which mdms service access is available on the environment specific yaml file in DevOps. Example below\
   [<img src="https://github.com/fluidicon.png" alt="" data-size="line">iFix-DevOps/mgramseva-qa.yaml at e471be940b88ccd8811b2dfb7a0e4187b0ec39cd · misdwss/iFix-DevOps](https://github.com/misdwss/iFix-DevOps/blob/e471be940b88ccd8811b2dfb7a0e4187b0ec39cd/deploy-as-code/helm/environments/mgramseva-qa.yaml#L224)

### Steps to run locally <a href="#steps-to-run-locally" id="steps-to-run-locally"></a>

please follow the steps below

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">punjab-mgramseva/LOCALSETUP.md at master · misdwss/punjab-mgramseva](https://github.com/misdwss/punjab-mgramseva/blob/master/utilities/rollout-dashboard-cronjob/LOCALSETUP.md)

### Loading to Metabase <a href="#loading-to-metabase" id="loading-to-metabase"></a>

The python script inserts the data into table “`roll_out_dashboard`“ in mgramSevaDb for every run, it cleans the old data and creates new data.

This table has to be loaded into the metabase by adding mGramSeva DB to the metabase.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
