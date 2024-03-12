# iFIX Fiscal Event Aggregator

## Overview

Fiscal Event Aggregator is a Java standalone application, which runs as Cron Job to aggregate the fiscal event data from the Druid data store to Postgres DB.

### Version History

Current Version: 2.0.0

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met

1. Java 8
2. Druid DB & Postgres DB should be up and running

## Features

Fiscal-Event-Aggregator computes the aggregate of data over a selected time period. Aggregator will apply the time range filter according to the following approach :

{% hint style="info" %}
Fiscal periods will be picked up as per the current system time. The current year will be the current fiscal period starting from the 1st of April of the current year to the 31st March of (current year+1). And it will also aggregate the data of one previous fiscal year starting from the 1st of April of (current year -1)  to the 31st of March of the current year.
{% endhint %}

Follow the steps below to aggregate the final fiscal event data as per the fiscal time periods.

1. Group the sum of the  amount based on department entity ancestry\[6] id (`attributes.departmentEntity.ancestry[6].id`) that is GP (Gram Panchayat), COA (chart of account) id, and event type.
2. Difference of the sum of the amount of "DEMAND" and "RECEIPT" event type with respect to distinct department entity ancestry\[6] id (`attributes.departmentEntity.ancestry[6].id`) that is GP (Gram Panchayat).
3. Difference of the sum of the amount of "BILL" and "PAYMENT" event type with respect to distinct department entity ancestry\[6] id (`attributes.departmentEntity.ancestry[6].id`) that is GP(Gram Panchayat).

Upsert the final aggregated fiscal event data into the Postgres DB.

## Environment

_Note: Below environment variables need to be configured with respect to the environment_

<table><thead><tr><th width="187.33333333333331">Key</th><th width="187">Value</th><th>Description</th></tr></thead><tbody><tr><td><code>DRUID_CONNECT_PROTOCOL</code></td><td><code>HTTP</code></td><td>This is a hardcoded value And won’t change w.r.t environment. And It depends upon the druid broker’s protocol that is getting used to connect.</td></tr><tr><td><code>DRUID_CONNECT_PORT</code></td><td><code>8082</code></td><td>This is a hardcoded value And won’t change w.r.t environment. It depends upon the druid broker protocol that we are using and the corresponding port of that druid broker.</td></tr><tr><td><code>DRUID_HOST</code></td><td><code>druid-broker.olap</code></td><td>this is kept under <code>configmaps</code>.</td></tr><tr><td><code>FISCAL_EVENT_DATASOURCE</code></td><td><code>fiscal-event</code></td><td>This is the data Source present in Druid DB. It is the same as defined in Druid DB.</td></tr></tbody></table>

## Interaction Diagram

<div align="left">

<img src="../../../../.gitbook/assets/image (19).png" alt="">

</div>

## Configuration

Update the configurations in the dev.yaml, qa.yml, prod.yaml file.
