# Installation

## Deployment of iFix Adapter <a href="#deploy-mgramseva" id="deploy-mgramseva"></a>

Post infra setup (Kubernetes Cluster), there starts the deployment process.&#x20;

Pipeline as code is a practice of defining deployment pipelines through source code, such as Git. Pipeline as code is part of a larger “as code” movement that includes infrastructure as code. Teams can configure builds, tests, and deployment in code that is trackable and stored in a centralized source repository. Teams can use a declarative [YAML](https://about.gitlab.com/blog/2020/10/01/three-yaml-tips-better-pipelines/) approach or a vendor-specific programming language, such as Jenkins and Groovy, but the premise remains the same.

A pipeline as code file specifies the stages, jobs, and actions for a pipeline to perform. Because the file is versioned, changes in pipeline code can be tested in branches with the corresponding application release.

The pipeline as code model of creating continuous integration pipelines is an industry best practice, but deployment pipelines used to be created very differently.

The deployment process has got 2 stages and 2 modes. We can see the modes first and then the stages.‌

### The 2 Modes of Deployment <a href="#the-2-modes-of-deployment" id="the-2-modes-of-deployment"></a>

Essentially,  iFix adapter deployment means that we need to generate Kubernetes manifests for each individual service. We use the tool called helm, which is an easy, effective and customizable packaging and deployment solution. So depending on where and which env you initiate the deployment there are 2 modes that you can deploy.‌

1. From [**Local machine**](../../ifix-dashboard/installation/local-setup.md) - whatever we are trying in this sample exercise so far.
2. Advanced: **** [**Setup CI/CD System**](../../ifix-dashboard/installation/ci-cd.md) like Jenkins - Depending on how you want to setup your CI/CD and the expertise the steps will vary, however here you can find how we eGov has set up a exemplar CI/CD on Jenkins and the pipelines are created automatically without any manual intervention.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
