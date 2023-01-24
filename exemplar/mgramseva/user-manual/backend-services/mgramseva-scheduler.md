# mGramSeva Scheduler

## **Overview** <a href="#hardbreak-overview" id="hardbreak-overview"></a>

Schedulers are designed to run a particular service at a scheduled time, without triggering manually. We can have multiple schedulers for an application. It will consider the GMT time format only.

### **How CronJob Works**

The python script (name) would read the mdms-read-cronjob json from the mdms service which users CRONJOB user for a token to access mdms service.&#x20;

Try to identify the API's configured in this mdms with the argument passed while invoking the script.

With the identified configs from the mdms, the script calls the respective API configured there.

### **Schedulers Available in mGramSeva**

Total 7 schedulers are available in the mGramSeva:\
**\_schedulerTodaysCollection:** This scheduler will run daily to send the day collection amount to the collection employee.\
**\_jobscheduler/true:** This is to send the notification to the ULB employee when the bulk demand auto-generation is failed.

**\_schedulermarkexpensebill:** This scheduler is used to mark the expense as paid for the paid expenses once for every fortnight.\
**\_schedulernewexpenditure:** This is used to send the notification once for every fortnight regarding the no of expenditures created.\
**\_schedulermonthsummary:** This is to send the monthly summary details to the ULB employee.\
**\_schedulerpendingcollection:** This is to send the total pending amount details to the respective ULB employee user once every fortnight.\
**\_jobscheduler/false:** This is used to generate the bulk demand automatically once every month.

As we have 7 different schedulers in mGramSeva which will be running in 4 different time slots so we have to configure, all of them run the same python scripts  with the different argument which you can see in the file under command -> args

The Time of the scheduler to run should be configured under cron-> schedule option.&#x20;

&#x20;Example of failedBulkDemand scheduler.

You can observer&#x20;

1. command->args value is failedbulkdemand ( through which python script understand to invoke only api configured in mdms-read-cronjob mdms json file with the name as “failedbulkdemand”
2. cron->schedule  value is “ 30 3 5 \* \*” which define the time to kick this scheduler i.e at 3.30 on 5th day of every month. As the crontab follows GMT timezone converting this time to IST this jobs run on 9am of on 5th day of every month\
   [![](https://crontab.guru/favicon.ico)Crontab.guru - The cron schedule expression editor](https://crontab.guru/) helps to define the pattern for the schedule cron.[![](https://crontab.guru/favicon.ico)Crontab.guru - The cron schedule expression editor](https://crontab.guru/)

## **Configuration**

#### **Infraops configuration changes**

**PriorNote:** In Devops for every configuration app name will change according to the name of the cron job file given and the schedule will change according to the time set, and argument will be as per job name given in mdms configuration.

&#x20;**labels:** app: monthly-cronjob  // This name will change based on the cronjob schedular we are using group: mdms-read-cronjob // this is same for all as we are using same python script

**cron:** schedule: 30 3 4 \* \*  // This depends on the time we need to run the schedular

**image:** repository: api-cronjob tag: v1

**command:**&#x20;

* python3
* cronJobAPIConfig.py

**args:**

* monthly   // This will be the job name which will differ with the requirement of scheduler type.

**env:** |

* name: JOB\_NAME

&#x20;   valueFrom:

&#x20;     fieldRef:

&#x20;       fieldPath: [metadata.name](http://metadata.name/)                   &#x20;

resources: |

&#x20; requests: {}

The remaining fields will be the same for all the schedulers.

**Monthly**: This will run and send the notification to the ULB employee or consumer on the 4th of every month morning at 9 am as per the scheduled time.\
**Fortnightevening**: This scheduler will run on the 1st and 15th of every month evening at 6 pm to send the respective notification to the Consumer.\
**Failedbulkdemand**: When the bulk demand generation is failed this scheduler will run and share the message to ULB employees to generate demand manually.\
**Dailyevening**: This schedular will run daily and send notifications to the collection operator on a daily basis.\
Here are the links

* [Monthly](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/charts/utilities/mdms-read-cronjob/monthly-values.yaml)
* [Failed Bulk Demand](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/charts/utilities/mdms-read-cronjob/failedbulkdemand-values.yaml)
* [Fortnight Evening](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/charts/utilities/mdms-read-cronjob/fortnightevening-values.yaml)
* [Daily Evening](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/charts/utilities/mdms-read-cronjob/values.yaml)

MDMS Object details and Configuration:\
{

&#x20; "jobName": "monthly",  // This will change based on the job name

&#x20; "active": "true",  // when it is true schedular will run automatically and when it is false schedular won’t run.

&#x20; "method": "POST",

&#x20; "url": "[http://echallan-services.mgramseva:8080/echallan-services/eChallan/v1/\_schedulermonthsummary](http://echallan-services.mgramseva:8080/echallan-services/eChallan/v1/\_schedulermonthsummary)",  // This is the respective service url to call that service as per the scheduler

&#x20; "payload": {

&#x20;   "RequestInfo": "{DEFAULT\_REQUESTINFO}"  // this is common in all the schedulers to send the request info

&#x20; },

&#x20; "header": {

&#x20;   "Content-Type": "application/json" // This is one of the common property for all the schedulers

&#x20; }

}

Here is the Configuration for all the schedulers:[ Click here to see](https://github.com/misdwss/mdms-mgramseva/blob/QA/data/pb/common-masters/CronJobAPIConfig.json)

```
{

      "jobName": "monthly",

      "active": "true",

      "method": "POST",

      "url": "http://ws-calculator.mgramseva:8080/ws-calculator/waterCalculator/_jobscheduler/false",

      "payload": {

        "RequestInfo": "{DEFAULT_REQUESTINFO}"

      },

      "header": {

        "Content-Type": "application/json"

      }

    },

    {

      "jobName": "fortnightevening",

      "active": "true",

      "method": "POST",

      "url": "http://ws-services.mgramseva:8080/ws-services/wc/_schedulerpendingcollection",

      "payload": {

        "RequestInfo": "{DEFAULT_REQUESTINFO}"

      },

      "header": {

        "Content-Type": "application/json"

      }

    },

    {

      "jobName": "monthly",

      "active": "true",

      "method": "POST",

      "url": "http://echallan-services.mgramseva:8080/echallan-services/eChallan/v1/_schedulermonthsummary",

      "payload": {

        "RequestInfo": "{DEFAULT_REQUESTINFO}"

      },

      "header": {

        "Content-Type": "application/json"

      }

    },

    {

      "jobName": "fortnightevening",

      "active": "true",

      "method": "POST",

      "url": "http://echallan-services.mgramseva:8080/echallan-services/eChallan/v1/_schedulernewexpenditure",

      "payload": {

        "RequestInfo": "{DEFAULT_REQUESTINFO}"

      },

      "header": {

        "Content-Type": "application/json"

      }

    },

    {

      "jobName": "fortnightevening",

      "active": "true",

      "method": "POST",

      "url": "http://echallan-services.mgramseva:8080/echallan-services/eChallan/v1/_schedulermarkexpensebill",

      "payload": {

        "RequestInfo": "{DEFAULT_REQUESTINFO}"

      },

      "header": {

        "Content-Type": "application/json"

      }

    },

    {

      "jobName": "failedbulkdemand",

      "active": "true",

      "method": "POST",

      "url": "http://ws-calculator.mgramseva:8080/ws-calculator/waterCalculator/_jobscheduler/true",

      "payload": {

        "RequestInfo": "{DEFAULT_REQUESTINFO}"

      },

      "header": {

        "Content-Type": "application/json"

      }

    },

    {

      "jobName": "dailyevening",

      "active": "true",

      "method": "POST",

      "url": "http://ws-services.mgramseva:8080/ws-services/wc/_schedulerTodaysCollection",

      "payload": {

        "RequestInfo": "{DEFAULT_REQUESTINFO}"

      },

      "header": {

        "Content-Type": "application/json"

      }

    }


```

### **USER Creation**

Need to create a user with CRONJOB as name and type as SYSTEM and ROLE as SYSTEM AND EMPLOYEE here is the sample curl to create the user.

```
curl --location --request POST 'http://localhost:8090/user/users/_createnovalidate'

--header 'Content-Type: application/json'

--data-raw '{
  "RequestInfo": {
    "api_id": "1",
    "ver": "1",
    "ts": null,
    "action": "create",
    "did": "",
    "key": "",
    "msg_id": "",
    "requester_id": "",
    "userInfo": {
      "userName": "XXYY",
      "name": "NAME",
      "gender": "male",
      "mobileNumber": "XXYY",
      "active": true,
      "type": "EMPLOYEE",
      "tenantId": "pb",
      "password": "eGov@123",
      "roles": [
        {
          "code": "SUPERUSER",
          "tenantId": "pb"
        }
      ]
    }
  },
  "User": {
    "userName": "CRONJOB",
    "name": "CRONJOB",
    "gender": "male",
    "mobileNumber": "XXXXXX",
    "active": true,
    "type": "SYSTEM",
    "tenantId": "pb",
    "password": "eGov@123",
    "roles": [
      {
        "code": "SYSTEM",
        "tenantId": "pb"
      }
    ]
  }
}'
```

## **Deployment**

When you build the cronjob you will get the build id like below.\
api-cronjob:develop-c0aa08a-2\
From this you will take the only id instead of complete name like develop-c0aa08a-2.  This will be used as the id for your respective yaml files and will be deployed the same to you required environment to test the cron job.\
**For example :**

Mdms-read-cronjob:develop-c0aa08a-2,

fAiledbulkdemand:develop-c0aa08a-2,

Fortnightevening:develop-c0aa08a-2,

monthly:develop-c0aa08a-2\
**Note:**   develop-c0aa08a-2 is the common build id for all the files which you are using.

**How to run the cronjob manually**

Please delete the existing cron jobs if they are already exists with same name.

kubectl delete cronjob mdms-read-cronjob -n mgramseva

Please deploy these builds in QA environments, which are related to cronjob schedulars.

mdms-read-cronjob:develop-c0aa08a-2,failedbulkdemand:develop-c0aa08a-2,fortnightevening:develop-c0aa08a-2,monthly:develop-c0aa08a-2

Steps to test the cron job schedular.

* kubectl get cronjob -n mgramseva   -- to check the list of cron jobs

We will create the job manually to test the messages.

Here are the commands to create the jobs.

Will receive a message for the respective schedular each time we run it.

We can increase the no to test again like failedbulkdemand-manually-1 next it will be failedbulkdemand-manually-2

* kubectl create job --from=cronjob/failedbulkdemand failedbulkdemand-manually-1 -n mgramseva
* kubectl create job --from=cronjob/fortnightevening fortnightevening-manually-1 -n mgramseva
* kubectl create job --from=cronjob/mdms-read-cronjob mdms-read-cronjob-manually-1 -n mgramseva
*   kubectl create job --from=cronjob/monthly monthly-manually-1 -n mgramseva

    &#x20;
* kubectl get job -n mgramseva   -- to check the list of jobs

**To check the cronjob image**

kubectl describe cronjob mdms-read-cronjob -n mgramseva

**To delete specific job**

kubectl delete jobs mdms-read-cronjob-manually-1 -n mgramseva\


> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
