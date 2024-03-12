---
description: Infrastructure Setup
---

# iFIX Service Setup

## Introduction

iFIX/mGramSeva is a microservices-based distributed cloud-native application. The microservices streamline processes to meet outcomes at scale and speed. Each of the microservices is dockerized and deployed on Kubernetes infrastructure. &#x20;

## Pre-reads <a href="#pre-read" id="pre-read"></a>

It is essential to understand some of the key concepts, benefits and best practices of Kubernetes platform before we understand the deployment of the iFix/mGramSeva. &#x20;

* Know the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)​
* Know the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands
* Know Kubernetes manifests: [https://www.youtube.com/watch?v=ohSUtEfDefc](https://www.youtube.com/watch?v=ohSUtEfDefc)​
* Know how to manage env values, secrets of any service deployed in Kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)​
* Know how to port forward to a pod running inside k8s cluster and work locally [https://www.youtube.com/watch?v=TT3nd5n5Yus](https://www.youtube.com/watch?v=TT3nd5n5Yus)​
* Know sops to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)​

## 1. Choose Installation Type <a href="#v-1-choose-the-cloud-1" id="v-1-choose-the-cloud-1"></a>

Choose the target infra type and follow the instructions to set up a Kubernetes cluster before moving on to the deployment.



{% content-ref url="infra-setup/quickstart.md" %}
[quickstart.md](infra-setup/quickstart.md)
{% endcontent-ref %}

{% content-ref url="infra-setup/on-aws.md" %}
[on-aws.md](infra-setup/on-aws.md)
{% endcontent-ref %}

{% content-ref url="infra-setup/on-azure.md" %}
[on-azure.md](infra-setup/on-azure.md)
{% endcontent-ref %}

## 2. Deployment <a href="#v-1-choose-the-cloud" id="v-1-choose-the-cloud"></a>

Before we begin the deployment, it is important to understand the deployment architecture that starts from the source code to the production-ready stage. Deploying and managing Kubernetes have emerged as a streamlined way to deploy containers in the cloud infrastructure. When running Kubernetes at scale, managing, operating, and scaling its infrastructure to maximize cluster utilization can be challenging. There are too many parameters the development team needs to manage and configure. This includes selecting the best instance type and size, determining when to scale up or down, and making sure all of the containers are scheduled and running on the best instances — and that is even before starting to think about cost resource optimization.

![](https://lh4.googleusercontent.com/JkymqACmPBvb3Y77UrqghaQifq1YYC\_IfujLtK9eaXcIcMwvkBBx0thuGO7UD2BssAflbyyE2u9teNkqKLywDet09cl0fVO6GfgqFnRjUIRSLahvj5v7mT97sl8MKuYcFj2qfntM8Zs=s0)

The simplest way to get started with the **deployment process** is to manage deployment **configuration as code**. Each service deployment configuration is defined as Helm charts and deployed into the Kubernetes cluster. We can collocate the deployment-as-code as source code, leveraging all the benefits of source control including change tracking and branching, and then package it. So below is the source code repo that contains all the deployment-as-code for iFIX.

#### 1. mGramSeva Installation

{% content-ref url="installation/" %}
[installation](installation/)
{% endcontent-ref %}

#### 2. iFIX-adapter Installation

{% content-ref url="../../exemplar/ifix-adapter/installation/" %}
[installation](../../exemplar/ifix-adapter/installation/)
{% endcontent-ref %}

#### 3. iFIX Ref Dashboard Installation

{% content-ref url="../../exemplar/ifix-dashboard/installation/" %}
[installation](../../exemplar/ifix-dashboard/installation/)
{% endcontent-ref %}

## 3. Destroy the Setup <a href="#id-5-destroy-the-cluster" id="id-5-destroy-the-cluster"></a>

Clean up the cluster Setup using the command below, if required. This deletes the entire cluster and other cloud resources that were provisioned for the mGramSeva Infra Setup.

```
cd iFix-DevOps/infra-as-code/terraform/my-iFix-eksterraformdestroy​
```

## Conclusion <a href="#conclusion" id="conclusion"></a>

All done, the infra on local, cloud, and deployment of iFIX into the Kubernetes cluster is completed successfully.



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
