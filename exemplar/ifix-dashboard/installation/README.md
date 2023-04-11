---
description: Installation and deployment steps for iFIX dashboard
---

# Installation

## Deployment of iFix Dashboard <a href="#deploy-mgramseva" id="deploy-mgramseva"></a>

Post infra setup (Kubernetes Cluster), the deployment has got 2 stages and 2 modes. We can see the stages first and then the modes.‌

### The 2 Modes of Deployment <a href="#the-2-modes-of-deployment" id="the-2-modes-of-deployment"></a>

Essentially,  iFix dashboard deployment means that we need to generate Kubernetes manifests for each individual service of the required OLAP components like a druid, metabase. We use the tool called helm, which is an easy, effective and customizable packaging and deployment solution. So depending on where and which env you initiate the deployment there are 2 modes that you can deploy.‌

1. From[ **Local machine**](../../../platform/installation/installation/local-setup.md) - whatever we are trying in this sample exercise so far.
2. Advanced: [**Setup CI/CD System**](ci-cd.md) like Jenkins - Depending on how you want to set up your CI/CD and the expertise the steps will vary, however here you can find how we eGov has set up an exemplar CI/CD on Jenkins and the pipelines are created automatically without any manual intervention.

You can choose the infra type and the env to either [single fat server](https://druid.apache.org/docs/latest/operations/single-server.html) or [distributed setup](https://druid.apache.org/docs/latest/tutorials/cluster.html) on Docker compose or Kubernetes.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
