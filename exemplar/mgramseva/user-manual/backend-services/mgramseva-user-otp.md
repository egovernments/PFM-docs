# mGramSeva - User OTP

## **Overview**

user-otp service is used to generate OTP for user login, user registration and user password change.

## **Pre-requisites**

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* Prior Knowledge of KAFKA
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc.
* Following services should be up and running:
  * user
  * MDMS
  * Id-Gen
  * URL-Shortening
  * notification-sms

## **Key Functionalities**

* user-otp service generate validates the user details and request type and send OTP for a particular action.

## **Deployment Details**

* Deploy the latest image of the user-otp service available.

## **Configuration Details**

|                       |      |                        |
| --------------------- | ---- | ---------------------- |
| `expiry.time.for.otp` | 3000 | Expiry time of the otp |
|                       |      |                        |

## Integration

### Integration Scope

User OTP service can be integrated with any organization or system that wants OTP based validation for user login, registration.

### Integration Benefits

* Easy to create and simple process of generating bills from demands.
* Easy to generate OTP to validate mobile number for registration, login and password reset with simple API calls

### Steps to Integration

1. otp can be generate calling `/user-otp/v1/_send`

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
