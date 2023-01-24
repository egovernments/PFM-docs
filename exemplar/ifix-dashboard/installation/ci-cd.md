---
description: iFix Dashboard
---

# CI/CD

### The 2 Stages <a href="#the-2-stages" id="the-2-stages"></a>

## **Stage 1 : Jenkins Setup**

Post infra setup (Kubernetes Cluster), We start with deploying the Jenkins and kaniko-cache-warmer.

### Pre-requisites

* Sub Domain to expose CI/CD URL
* GitHub [Oauth App](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app)
* [GitHub User ssh key](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app)
* With [GitHub user generate a personal read only access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)&#x20;
* [Docker hub account details](https://hub.docker.com/signup) (username and password)
*   SSL Certificate for the sub-domain



**Prepare an <**[**ci.yaml**](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/ci.yaml)**> master config file and <**[**ci-secrets.yaml**](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/ci-secrets.yaml)**>, you can name this file as you wish which will have the following configurations.**

* credentials, secrets (You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **ci-secret.yaml** separately)
* Check and Update [**ci-secrets.yaml**](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/ci-secrets.yaml) **** details (like github Oauth app clientId and clientSecret, GitHub user details gitReadSshPrivateKey and gitReadAccessToken etc..)
* To create Jenkins namespace mark this [flag](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo.yaml#L5) **true**
* Add your env's kubconfigs under kubConfigs like [https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/ci-secrets.yaml#L19](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/ci-secrets.yaml#L19)
* KubeConfig env's name and deploymentJobs name from ci.yaml should be the same&#x20;
* Update the [CIOps](https://github.com/misdwss/CIOps) and [DIGIT-DevOps](https://github.com/misdwss/iFix-DevOps) repo name with your forked repo name and provide read-only access to github user to those repo's.
* SSL Certificate for the sub-domain

```
cd iFix-DevOps/deploy-as-code/egov-deployer
```

```
kubectl config use-context <your cluster name>
go run main.go deploy -c -e ci 'jenkins,kaniko-cache-warmer,nginx-ingress'
```

You have launched the Jenkins. You can access the same through your sub-domain which you configured in ci.yaml.

The Jenkins CI pipeline is configured and managed 'as code'.

​Example URL - https://\<Jenkins\_domain>​

## **Stage 2: Continuous Integration (CI)** <a href="#continuous-integration-ci" id="continuous-integration-ci"></a>

****

Since there are many services and the development code is part of various git repos, you need to understand the concept of **cicd-as-service** which is open-sourced. This page also guides you through the process of creating a CI/CD pipeline.

**As a developer -** To integrate any new service/app to the CI/CD below is the starting point:

Once the desired service is ready for the integration: decide the service name, type of service, whether DB migration is required or not. While you commit the source code of the service to the git repository, the following file should be added with the relevant details which are mentioned below:

**Build-config.yml** –It is present under the build directory in each repository

```
https://github.com/misdwss/punjab-mgramseva/blob/master/build/build-config.yml
```

This file contains the below details which are used for creating the automated Jenkins pipeline job for your newly created service.

```
config:
  - name: < Name of the job, foo/bar would create job named bar inside folder foo>
    build:
    - work-dir: < Working directory of the app to be built >
      dockerfile: < Path to the dockerfile, optional, assumes dockerfile in working directory if not provided >
      image-name: < Docker image name  >
```

While integrating a new service/app, the above content needs to be added in the build-config.yml file of that app repository. For example: If we are onboarding a new service called **egov-test,** then the build-config.yml should be added as mentioned below.

```
config:   
  - name: core-services/egov-test     
    build:     - work-dir: egov-test       
    dockerfile: build/maven/Dockerfile       
    image-name: egov-test
```

If a job requires multiple images to be created (DB Migration) then it should be added as below,

```
config:   
  - name: core-services/egov-test     
    build:     
    - work-dir: egov-test       
      dockerfile: build/maven/Dockerfile       
      image-name: egov-test     
    - work-dir: egov-test/src/main/resources/db       
      dockerfile: build/maven/Dockerfile       
      image-name: egov-test-db
```

**Note -** **If a new repository is created then the build-config.yml should be created under the build folder and then the config values are added to it.**

**The git repository URL is then added to the Job Builder parameters**

When the Jenkins Job => job builder is executed the CI Pipeline gets created automatically based on the above details in build-config.yml. Eg: **egov-test** job will be created under the **core-services** folder in Jenkins because the “build-config was edited under core-services” And it should be the “master” branch only. Once the pipeline job is created, it can be executed for any feature branch with build parameters (Specifying which branch to be built – master or any feature branch).

As a result of the pipeline execution, the respective app/service docker image will be built and pushed to the Docker repository.

**Job Builder** – Job Builder is a Generic Jenkins job that creates the Jenkins pipeline automatically which are then used to build the application, create the docker image of it and push the image to the docker repository. The Job Builder job requires the git repository URL as a parameter. It clones the respective git repository and reads the [**build/build-config.yml**](https://github.com/misdwss/punjab-mgramseva/blob/master/build/build-config.yml) file for each git repository and uses it to create the service build job.

‌**Check git repository URL is available in** [**ci.yaml**](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/ci.yaml)​[‌](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/ci.yaml)‌

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F3b7e0c5ac4c5064192777b45de690069ff11a674.png?alt=media)

If git repository URL is available build the Job-Builder Job

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F402d59e5650213e9bbd0631717d6201307e02e2f.png?alt=media)

If the git repository URL is not available ask the Devops team to add it.

## **Continuous Deployment (CD)**‌ <a href="#continuous-deployment-cd" id="continuous-deployment-cd"></a>

The services deployed and managed **on a Kubernetes cluster** in cloud platforms like **AWS, Azure, GCP, OpenStack, etc.** Here, we use **helm charts** to manage and generate the **Kubernetes manifest files** and use them for further deployment to the respective **Kubernetes cluster**. Each service is created as charts which will have the below-mentioned files in them.

```
billing-service/   
# Directory – name of the service/appChart.yaml         
# A YAML file containing information about the chartLICENSE            
# OPTIONAL: A plain text file containing the license for the chartREADME.md          # OPTIONAL: A human-readable README filevalues.yaml        
# The default configuration values for this charttemplates/         
# A directory of templates that, when combined with values, will generate valid Kubernetes manifest files.
```

To deploy a new service, we need to create the helm chart for it. The chart should be created under the **charts/helm** directory in iFix-DevOps repository.

```
Github repository     https://github.com/misdwss/iFix-DevOps
```

We have an automatic helm chart generator utility that needs to be installed on the local machine, the utility prompts for user inputs about the newly developed service (app specifications) for creating the helm chart. The requested chart with the configuration values (created based on the inputs provided) will be created for the user.

‌ _**Name of the service? test-service Application Type? NA Kubernetes health checks to be enabled? Yes Flyway DB migration container necessary? No, Expose service to the internet? Yes, Route through API gateway \[zuul] No Context path? hello**_‌

The generated chart will have the following files.

```
create Chart.yaml
create values.yaml
create templates/deployment.yaml
create templates/service.yaml
create templates/ingress.yaml
```

This chart can also be modified further based on user requirements.

The Deployment of manifests to the Kubernetes cluster is made very simple and easy. We have Jenkins Jobs for each state and are environment-specific. We need to provide the image name or the service name in the respective Jenkins deployment job.

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fe39a9063f0ae56f845ba2230786302c0d4e957e6.png?alt=media)

Enter a caption for this image (optional)

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F5e19cdbb9eb18d76fdd2b4f28c5aed5c8bf377e2.png?alt=media)

Enter a caption for this image (optional)

‌The deployment Jenkins job internally performs the following operations,‌

* Reads the image name or the service name given and finds the chart that is specific to it.
* Generates the Kubernetes manifests files from the chart using the helm template engine.
* Execute the deployment manifest with the specified docker image(s) to the Kubernetes cluster.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
