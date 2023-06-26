# mGramSeva iFIX Adapter

The mGramSeva iFIX Adapter receives multiple event requests from the mGramSeva service and helps in attributes conversion to map with fix-fiscal-event-service request data.

## Setup Steps

1.  Environment variable

    Configure "fiscal-event-service", "adapter-master-data-service" and "ifix-department-entity-service" in egov-service-host in respective environment yaml file ([<img src="https://github.com/fluidicon.png" alt="" data-size="line">iFix-DevOps/mgramseva-qa.yaml at mgramseva · misdwss/iFix-DevOps](https://github.com/misdwss/iFix-DevOps/blob/mgramseva/deploy-as-code/helm/environments/mgramseva-qa.yaml) ).
2.  Redis data clean up

    Execute the below commands on redis-cli before doing any activity on the mgramseva iFix adapter while performing the deployment first time.

    *   Connecting Redis Client:&#x20;

        `kubectl exec -it <redis-pod> -n mgramseva -- /bin/bash`

        `redis-cli`

        _e.g._

        `kubectl exec -it redis-647449f6b9-gg4gw -n mgramseva -- /bin/bash`

        `redis-cli`

        `keys *  (check all keys)`
    *   Redis cleanup command

        `del <key>`

        _e.g._

        `del "10101" "10102" "10201" "20101" "20201" "20301" "20401"`

        `keys * (check all keys)`



    _**Note:** Make sure all client codes, which have been mentioned in the "ifix\_adapter\_coa\_map" table, are listed in the redis "DEL" command list and recheck those are removed using "keys \*" command._&#x20;

## Steps To Use mGramSeva iFIX Adapter Service

Use the postman tool to verify mGramSeva iFix adapter API end. It is open-end and therefore does not require any access token.

## &#x20;**Technical Doc**

[MGramSeva IFIX Adapter Services v2.0](../../../exemplar/ifix-adapter/adapter-service-documents/mgramseva-ifix-adapter-service.md)





> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._



\
