---
description: Platform architecture
---

# Architecture

## Architecture Overview

The iFIX platform architecture and the interacting systems are divided into 3 parts:

1. iFIX Platform
2. External Agency Systems
3. Common Reference Data

<div align="left">

<img src="../../.gitbook/assets/image (17) (2).png" alt="">

</div>

### iFIX Platform

1. **Fiscal Event Service:** It receives/sends fiscal events from/to the external systems.&#x20;
2. **Fiscal Event Store:** After basic checks, the raw fiscal events are stored in the fiscal event store.&#x20;
3. **Fiscal Event Post Processor:** Post Processor de-references the master data and flattens the object to store the event in the analytical data store.&#x20;
4. **Fiscal Event Analytical Store:** Fiscal Events will be stored in a separate analytical store to run analytics queries.&#x20;
5. **Fiscal Event Analytical Service:** All the analytics queries might not be able to run on the raw fiscal events, so a new fiscal event analytical service is developed to process the raw data and prepare it for the analytics queries.&#x20;
6. **Client Registry:** All the registered clients of iFIX are maintained in this registry.&#x20;

### External Agency System

1. **Fiscal Event Producer:** They are the on-ground systems that generate new financial transactional information.&#x20;
2. **Producer Adapter:** It helps the producer systems send the fiscal information to the iFIX Platform and link that transaction with some common reference data.&#x20;
3. **Fiscal Event Consumer:** There are systems on the other end of the transaction that executes some process based on fiscal transaction information.&#x20;
4. **Consumer Adapter:** It helps communicate fiscal events from the iFIX Platform to the consumer systems.&#x20;
5. **Reference Dashboard:** Based on the consumed fiscal events, reference dashboards can be built with aggregated amounts by reference data.&#x20;

### Common Reference Data

We can link fiscal events with common reference data to derive more value from the fiscal events data. This allows us to run better analytics queries.&#x20;

1. **Administrative Registry:** It will maintain the hierarchy of entities for a department integrated with iFIX. &#x20;
2. **Program Registry:** It will maintain the master data for government missions/schemes.&#x20;
3. **Location Registry:** It will maintain location reference data. This data is shared across all iFIX clients.&#x20;
4. **Chart of Account Registry:** It will maintain the chart of account details.&#x20;



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

