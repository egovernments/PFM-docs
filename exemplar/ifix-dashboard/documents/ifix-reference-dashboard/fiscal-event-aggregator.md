# iFIX Fiscal Event Aggregator

## Overview

Fiscal Event Aggregator is a java standalone application, which runs as Cron Job to aggregate the fiscal event data from the Druid data store to Postgres DB.

### Version History

Current Version : 2.0.0

## Prerequisites

Before you proceed with the configuration, make sure the following pre-requisites are met

1. Java 8
2. Druid DB & Postgres DB should be up and running

## Features

Fiscal-Event-Aggregator computes the aggregate of data over a selected time period. Aggregator will apply the time range filter according to the following approach :

{% hint style="info" %}
_Fiscal periods will be picked up as per the current system time. The current year will be the current fiscal period starting from 1st of April of the current year to 31st March of (current year+1). And it will also aggregate the data of one previous fiscal year starting from 1st of April of (current year -1)  to 31st March of the current year._
{% endhint %}

Follow the steps below to aggregate the final fiscal event data as per the fiscal time periods.

1. Group the sum of the  amount based on department entity ancestry\[6] id (`attributes.departmentEntity.ancestry[6].id`) that is GP (Gram Panchayat), COA (chart of account) id, and event type.
2. Difference of the sum of amount of "DEMAND" and "RECEIPT" event type with respect to distinct department entity ancestry\[6] id (`attributes.departmentEntity.ancestry[6].id`) that is GP (Gram Panchayat).
3. Difference of the sum of amount of "BILL" and "PAYMENT" event type with respect to distinct department entity ancestry\[6] id (`attributes.departmentEntity.ancestry[6].id`) that is GP(Gram Panchayat).

Upsert the final aggregated fiscal event data into the Postgres DB.

## Environment

_Note: Below environment variables need to be configured with respect to the environment_

| **Key**                   | **Value**           | **Description**                                                                                                                                                            |
| ------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `DRUID_CONNECT_PROTOCOL`  | `HTTP`              | This is a hardcoded value And won’t change w.r.t environment. And It depends upon the druid broker’s protocol that is getting used to connect.                             |
| `DRUID_CONNECT_PORT`      | `8082`              | This is a hardcoded value And won’t change w.r.t environment. It depends upon the druid broker protocol that we are using and the corresponding port of that druid broker. |
| `DRUID_HOST`              | `druid-broker.olap` | this is kept under `configmaps`.                                                                                                                                           |
| `FISCAL_EVENT_DATASOURCE` | `fiscal-event`      | This is the data Source present in Druid DB. It is the same as defined in Druid DB.                                                                                        |

## Interaction Diagram

![](<../../../../.gitbook/assets/image (18).png>)

## Configuration

Update the configurations in the dev.yaml, qa.yml, prod.yaml file.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
