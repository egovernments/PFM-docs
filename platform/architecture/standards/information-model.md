# Information Model

### Government

{% tabs %}
{% tab title="Description" %}
This object captures the fiscal information of external systems.
{% endtab %}

{% tab title="Attributes" %}
| Field | Type           | Description                                                    |
| ----- | -------------- | -------------------------------------------------------------- |
| id    | String (64,1)  | Unique Identifier                                              |
| name  | String (256,2) | Name of the Government or Tenant - e.g. India, Nigeria, Punjab |
{% endtab %}
{% endtabs %}

### Department

{% tabs %}
{% tab title="Description" %}
Captures the department attributes.
{% endtab %}

{% tab title="Attributes" %}
| Field | Type   | Description                                                             |
| ----- | ------ | ----------------------------------------------------------------------- |
| id    | string | Unique Identifier                                                       |
| name  | string | Name of the Department - e.g. Department of Water Supply and Sanitation |
| code  | string | Unique Code e.g. DWSS                                                   |
{% endtab %}
{% endtabs %}

### Chart of Account

{% tabs %}
{% tab title="Description" %}
Captures the COA data as a map.
{% endtab %}

{% tab title="Attributes" %}
| Field            | Type    | Description                                            |
| ---------------- | ------- | ------------------------------------------------------ |
| name             | String  | Name of the Account                                    |
| coaCode          | String  | Full Chart of Account String eg: 1234-123-123-12-12-12 |
| majorHead        | String  | Major head code                                        |
| majorHeadName    | String  | Major head name                                        |
| majorHeadType    | String  | Major head code type                                   |
| subMajorHead     | String  | Sub-Major head code                                    |
| subMajorHeadName | String  | Sub-Major head name                                    |
| minorHead        | String  | Minor head code                                        |
| minorHeadName    | String  | Minor head name                                        |
| subHead          | String  | Sub-Head code                                          |
| subHeadName      | String  | Sub-Head name                                          |
| groupHead        | String  | Group head code                                        |
| groupHeadName    | String  | Group head name                                        |
| objectHead       | String  | Object head code                                       |
| objectHeadName   | String  | Object head name                                       |
{% endtab %}
{% endtabs %}

### Expenditure

{% tabs %}
{% tab title="Description" %}
Captures the Expenditure attributes - encapsulates all scheme and non-scheme expenditure details.
{% endtab %}

{% tab title="Attributes" %}
| Field | Type   | Description                                                                                            |
| ----- | ------ | ------------------------------------------------------------------------------------------------------ |
| id    | String | Unique Identifier                                                                                      |
| name  | String | Name of the Expenditure - This could be a scheme or a non-scheme expenditure - e.g. Jal Jeevan Mission |
| code  | String | Unique Code e.g. JJM                                                                                   |
| type  | Enum   | Type of Expenditure - \[Scheme, Non-Scheme]                                                            |
{% endtab %}
{% endtabs %}

### Project

{% tabs %}
{% tab title="Description" %}
Captures the Project attributes.
{% endtab %}

{% tab title="Attributes" %}
| Field | Type   | Description                                                     |
| ----- | ------ | --------------------------------------------------------------- |
| id    | String | Unique Identifier                                               |
| name  | String | Name of the Project - e.g. Kartarpur Sahib Water Supply Project |
| code  | String | Code of the Project - e.g. S572                                 |
{% endtab %}
{% endtabs %}

### Amount

{% tabs %}
{% tab title="Description" %}

{% endtab %}

{% tab title="Attributes" %}
| Field             | Type            | Description                                                          |
| ----------------- | --------------- | -------------------------------------------------------------------- |
| id                | String          | Unique Identifier                                                    |
| amount            | Number          | Transaction Amount                                                   |
| coaId             | String          | Chart of Account ID                                                  |
| fromBillingPeriod | Integer($int64) | Start date of the billing period for which transaction is applicable |
| toBillingPeriod   | Integer($int64) | End date of the billing period for which transaction is applicable   |
{% endtab %}
{% endtabs %}

### Fiscal Event

{% tabs %}
{% tab title="Description" %}

{% endtab %}

{% tab title="Attributes" %}
| Field         | Type            | Description                                                 |
| ------------- | --------------- | ----------------------------------------------------------- |
| version       | String          | Version of the Information Model                            |
| id            | String          | System Generated Unique ID                                  |
| tenantId      | String          | Government ID                                               |
| projectId     | String          | Unique ID of the Associated Project                         |
| eventType     | String          | Type of Fiscal Event e.g. Demand, Bill, Payment, Receipt    |
| eventTime     | integer($int64) | Time Stamp when the event occurred in the source system     |
| referenceId   | String          | Unique Transaction Reference ID in the source system        |
| parentEventId | String          | Unique ID of the Parent Event to which this event is linked |
| amountDetails | Array\[Amount]  | Array of type Amount                                        |
{% endtab %}
{% endtabs %}

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
