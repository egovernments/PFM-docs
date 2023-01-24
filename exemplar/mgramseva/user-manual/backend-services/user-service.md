# mGramSeva - User Service

## Overview

User service is responsible for user data management and providing functionality to log in and log out of the DIGIT system.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* Encryption and MDMS services are running
* PSQL server is running and the database
* Redis is running

## Key Functionalities

* Store, update and search user data
* Provide authentication
* Provide login,logout functionality into MgramSeva platform
* Store user data PIIs in encrypted form

## Interaction Diagram

![](<../../../../.gitbook/assets/image (35).png>)

![](<../../../../.gitbook/assets/image (91).png>)

## Deployment Details

1. Setup latest version of egov-enc-service and egov-mdms- service
2. Deploy the latest version of egov-user service
3. Add Role-Action mapping for API’s

## Configuration Details

Following are the properties in application.properties file in user service which is configurable.

| **Property**                                | **Value** | **Remarks**                                        |
| ------------------------------------------- | --------- | -------------------------------------------------- |
| `egov.user.search.default.size`             | 10        | default search record number limit                 |
| `citizen.login.password.otp.enabled`        | true      | whether citizen login otp based                    |
| `employee.login.password.otp.enabled`       | false     | whether employee login otp based                   |
| `citizen.login.password.otp.fixed.value`    | 123456    | fixed otp for citizen                              |
| `citizen.login.password.otp.fixed.enabled`  | false     | allow fixed otp for citizen                        |
| `otp.validation.register.mandatory`         | true      | whether otp compulsory for registration            |
| `access.token.validity.in.minutes`          | 10080     | validity time of access token                      |
| `refresh.token.validity.in.minutes`         | 20160     | validity time of refresh token                     |
| `default.password.expiry.in.days`           | 90        | expiry date of a password                          |
| `account.unlock.cool.down.period.minutes`   | 60        | unlock time                                        |
| `max.invalid.login.attempts.period.minutes` | 30        | window size for counting attempts for lock         |
| `max.invalid.login.attempts`                | 5         | max failed login attempts before account is locked |
| `egov.state.level.tenant.id`                | pb        |                                                    |

## Integration

### Integration Scope

User data management and functionality to log in and log out into the DIGIT system using OTP and password.

### Integration Benefits

Providing the following functionality to citizen and employee type users

* &#x20;Employee:
  * User registration
  * Search user
  * Update user details
  * Forgot password
  * Change password
  * User role mapping(Single ULB to multiple roles)
  * Enable employees to login into the DIGIT system based on the password.
* Citizen:
  * Create user
  * Update user
  * Search user
  * User registration using OTP
  * OTP based login

### Steps to Integration

* To integrate, the host of egov-user should be overwritten in the helm chart.
* Use `/citizen/_create` endpoint for creating users into the system. This endpoint requires the user to validate his mobile Number using OTP. The first OTP will be sent to his mobile number and then that OTP will be sent as `otpReference` in the request body
* Use `/v1/_search` and `/_search` endpoints to search users in the system depending on various search parameters
* Use `/profile/_update` for updating the user profile. The user will be validated (either by OTP based validation or password validation) when this API is called
* &#x20;`/users/_createnovalidate` and `/users/_updatenovalidate` are endpoints to create user data into the system without any validations (no OTP or password required). They should be strictly used only for creating/updating user’s internally and should not be exposed outside
* **Forgot password:** In case the user forgets the password it can be reset by first calling `/user-otp/v1/_send` which will generate and send OTP on employee’s mobile number, the password can then be updated using this OTP by calling API `/password/nologin/_update` in which a new password along with the OTP has to be sent.
* Use `/password/_update` to update the existing password by logging in. In the request body, both old and new password has to be sent. Details of the API can be found in the attached swagger documentation
* Use `/user/oauth/token` for generating tokens, `/_logout`for logout and `/_details` for getting user information from his token
* **Multi Tenant User** : The Multi-tenant User functionality allows a user to perform actions across multiple ULB’s. For example, an employee belonging to Amritsar can perform the role of say Trade License Approver for Jalandhar by assigning a tenant level role of tenantId pb.jalandhar to him. Following is an example of such a user:

```
 {
        "id": 24226,
        "uuid": "11t0e02b-0145-4de2-bc42-c97b96264807",
        "userName": "xyz",
        "name": "abc",
        "mobileNumber": "9999999999",
        "emailId": "abc@gmail.com",
        "locale": null,
        "type": "EMPLOYEE",
        "roles": [
            {
                "name": "GP Admin",
                "code": "GP_ADMIN",
                "tenantId": "pb.massewal"
            },
            {
                "name": "Collector",
                "code": "COLLECTION_OPERATOR",
                "tenantId": "pb.lodhipur"
            }
        ],
        "active": true,
        "tenantId": "pb"
    }
```

\
&#x20;If an employee has a role with state level `tenantId` he can perform actions corresponding to that role across all tenants

* **Refresh Token:** Whenever the `/user/oauth/token` is called to generate the `access_token` , along with the `access_token` one more token is generated called `refresh_token` . The refresh token is used to generate new `access_token` whenever the existing one expires. Till the time the refresh token is valid the user won’t have to log in even if his `access_token` get’s expired, as it will be generated using `refresh_token`. The validity time of the refresh token is configurable and can be configured using the property: `refresh.token.validity.in.minutes`

## Reference Docs

### Doc Links

| **Title**                              | **Link**                                                                           |
| -------------------------------------- | ---------------------------------------------------------------------------------- |
| User Data encryption promotion details | [User data encryption promotion](https://digit-discuss.atlassian.net/l/c/xSSnmk12) |
| Encryption Service                     | [Encryption Service](https://digit-discuss.atlassian.net/l/c/HJwxmms6)             |

### API List

|                             | **Link**                                                                                                                   |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `/citizen/_create`          | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/users/_createnovalidate`  | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/_search`                  | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/v1/_search`               | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/_details`                 | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/users/_updatenovalidate`  | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/profile/_update`          | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/password/_update`         | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/password/nologin/_update` | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/_logout`                  | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |
| `/user/oauth/token`         | [https://www.getpostman.com/collections/15443fcb25c8aacd8897](https://www.getpostman.com/collections/15443fcb25c8aacd8897) |

&#x20;_(Note: All the API’s are in the same postman collection therefore the same link is added in each row)_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
