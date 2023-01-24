---
description: v2.0-alpha release details
---

# Release Notes

## Release Summary

IFIX 2.2-alpha release details and highlights are available in the below release notes.

* [IFIX Core Release Notes](ifix-core-release-notes/)
* [IFIX Adaptor Release Notes](ifix-adaptor-release-notes/)

## Release Highlights

* iFIX core and adapter service changes to cater to multi-village schemes.
  1. A project spanning 2 or more villages will now have a village as a tenant in mGramSeva.
  2. Tenant(village) to project(scheme) mapping is done through the iFIX adapter.
  3. Entity name in iFIX core refers to village whereas project name refers to project.
  4. Department entity level 6 too refers to a village (Tenant) and entity name level refers to the level in the hierarchy to which it is referred to.
  5. Validation - One village (referred to as department entity level 6 and entity name) cannot be mapped to more than 1 project.
*   Previously all the services were handled by IFIX core. In this release, a few services have been moved to the Adapter. These include -

    1. Department
    2. Department hierarchy
    3. Expenditure
    4. Department entity
    5. Project

    Data flow will be from Adaptor → Core → Druid → Metabase.
* Previously we were using COA ID in Amount Details. In this release, this has changed to COA Code.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
