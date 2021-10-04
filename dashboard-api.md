# Pollfish Dashboard API documentation

This document describes Pollfish Dashboard API that allows to easily
create, update, delete or retrieve stats of Pollfish apps.

| Base URL|
|:--------|
| https://www.pollfish.com/

## Endpoints

|#|     **URL**                                           | **Description**
|---|:--------------------------------------------------- |:-----------------------------------------------------------------------
|1|    **GET /api/public/v2/apps/:api_key**               |   returns an app object
|2|    **POST /api/public/v2/apps**                       |   creates a new app
|3|    **PUT /api/public/v2/apps/:api_key**               |   updates info of an existing app
|4|    **DELETE /api/public/v2/apps/:api_key**            |   deletes an app
|5|    **GET /api/public/v2/apps**                        |   returns an array of apps of a user
|6|    **GET /api/public/v3/apps/performance**            |   returns the performance metrics for all the apps of the developer
|7|    **GET /api/public/v3/apps/:api_key/performance**  |   returns the performance metrics of the specified app of the developer
|8|    **GET** **/api/public/v3/apps/revenue**           |   returns the revenue per provider for all the apps of the developer
|9|    **GET /api/public/v3/apps/:api_key/revenue**      |   returns the revenue per provider of the specified app of the developer
|10|    **GET /api/public/v3/apps/demographics**          |   returns the demographic data for a particular user
|11|    **GET /api/public/v3/apps/:api_key/users_log**    |   returns the user logs for a given device_id or request_uuid
|12|    **GET** **/api/public/v3/apps/revenuePerCountry**           |   returns the revenue per country for all the apps of the developer
|13|    **GET /api/public/v3/apps/:api_key/revenuePerCountry**      |   returns the revenue per country of the specified app of the developer
|14|    **GET /api/public/v3/apps/:api_key/performanceByCountry**  |   returns the performance metrics of the specified app of the developer grouped by country

### Removed Endpoints

|#|     **URL**                                           | **Description**
|---|:--------------------------------------------------- |:-----------------------------------------------------------------------
|1|    **GET /api/public/v2/apps/:api_key/stats**         |   use the newer /v3/apps/:api_key/performance
|2|    **GET /api/public/v2/apps/revenue**                |   use the newer v3/apps/revenue
|3|    **GET /api/public/v2/apps/:api_key/revenue**       |   use the newer v3/apps/:api_key/revenue


## Usage Steps


### 1) Obtain a Publisher Account

Register
at [www.pollfish.com/publisher](https://www.pollfish.com/login/publisher)

### 2) Retrieve Account Secret Key

Log in as a Publisher with Pollfish email. On the side menu click
Account Information and copy your Account Secret Key

### 3) Authentication

Use Basic Authentication over HTTPS

<br>

**Username:** Pollfish email (step 1)

**Password:** Account Secret Key (step 2)

### 4) Calls

## `4.1 GET /api/public/v2/apps/:api_key`

*Returns an app object*

### Server Response

|   | **Code**  | **Description**
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 403       | If an app with the specified api_key does not exist or you don\'t have the permissions to access the app

#### Example Response

```json
{
  "api_key": "b77bb0f8-5962-4882-a23c-2e6c9e99a84a",
  "behavior": 1,
  "category": "IAB3",
  "subcategory": "IAB3-2",
  "id": 16659,
  "image": "",
  "incentive": true,
  "name": "TestApp",
  "platform": "Android",
  "revenue": 0.0,
  "short_surveys_enabled": true,
  "third_party_surveys_enabled": true,
  "data_collection_surveys_enabled": true,
  "url": "http://www.example.com/test-app",
  "rewarded_survey": {
    "currency_name": "Diamonds",
    "variable_amount": 300,
    "fixed_amount": true
  },
  "offerwall": {
    "currency_name": "Points",
    "variable_amount": 100
  }
}
```

## `4.2 POST /api/public/v2/apps`

*Creates a new app*


The body of the request must contain a JSON document with following
information

### JSON fields

|   | Name | JSON Type  | Description                  |  Required
|---|:-----|:-----------|:-----------------------------|:----------------
|1  | name | string     | Name of the app              | Yes
|2  | category | string | Category of the app *        | Yes
|3  | subcategory | string | Subcategory of the app *  | Yes
|4  | url | string      | Public url of the app        | Yes
|5  | platform | number | Platform of the app. (0 for android,1 for ios, 2 for windows phone, 3 for web) | Yes
|6  | callback_url | string | The URL for server-to-server callbacks | No
|7  | behavior | number | Just indicators: 0, Dynamic (Recommended): 1, Force slide regularly: 2, Force all the time: 3 | No
|8  | data_collection_surveys_enabled | boolean | Whether the apps should receive data collection surveys | No
|9  | third_party_surveys_enabled | boolean | Whether the app should receive third party surveys | No
|10  | rewarded_survey | object | Reward information in case of single survey | No
|11  | offerwall | object | Reward information in case of offerwall | No

### JSON object rewarded_survey

|   | Name | JSON Type  | Description                  
|---|:-----|:-----------|:-----------------------------
|1  | currency_name | string     | Name of the reward             
|2  | variable_amount | float | Value of reward per survey        
|3  | fixed_amount | boolean | Whether the app uses a fixed amount per survey 

### JSON object offerwall

|   | Name | JSON Type  | Description                  
|---|:-----|:-----------|:-----------------------------
|1  | currency_name | string     | Name of the reward             
|2  | variable_amount | float | Value of reward per survey       

### Server Response

|   | **Code**  | **Description**
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid paramters

\*You can find an extensive list of categories and subcategories codes
in the relevant document

### Example Request

*http -a test\@gmail.com:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 \--json
POST https://www.pollfish.com/api/public/v2/apps name=MyNewApp
category=IAB22 subcategory=IAB22-2
url=\'https://play.google.com/store/apps/details?id=com.pollfish.demo\'
platform:=0*

### Example Response
```json
{
  "api_key": "b77bb0f8-5962-4882-a23c-2e6c9e99a84a",
  "behavior": 1,
  "category": "IAB22",
  "subcategory": "IAB22-2",
  "id": 16659,
  "image": "",
  "incentive": true,
  "name": "MyNewApp",
  "platform": "Android",
  "revenue": 0.0,
  "short_surveys_enabled": true,
  "third_party_surveys_enabled": true,
  "data_collection_surveys_enabled": true,
  "url": "https://play.google.com/store/apps/details?id=com.pollfish.demo",
  "rewarded_survey": {
    "currency_name": "Diamonds",
    "variable_amount": 300,
    "fixed_amount": true
  },
  "offerwall": {
    "currency_name": "Points",
    "variable_amount": 100
  }
}
```

## `4.3 PUT /api/public/v1/apps/:api_key`

*Updates info of an existing app*

The body of the request must contain a JSON document with the app
properties that you want to update. 

### JSON fields

|   | Name | JSON Type  | Description                  |  Required
|---|:-----|:-----------|:-----------------------------|:----------------
|1  | name | string     | Name of the app              | No
|2  | category | string | Category of the app *        | No
|3  | subcategory | string | Subcategory of the app *  | No
|4  | url | string      | Public url of the app        | No
|5  | callback_url | string | The URL for server-to-server callbacks | No
|6  | behavior | number | Just indicators: 0, Dynamic (Recommended): 1, Force slide regularly: 2, Force all the time: 3 | No
|7  | data_collection_surveys_enabled | boolean | Whether the apps should receive data collection surveys | No
|8  | third_party_surveys_enabled | boolean | Whether the app should receive third party surveys | No                                            No
|9  | rewarded_survey | object | Reward information in case of single survey | No
|10  | offerwall | object | Reward information in case of offerwall | No

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid paramters
|3  | 403       | If an app with the specified api_key does not exist or you don't have the permissions to access the app

\*You can find an extensive list of categories and subcategories codes
in the relevant document

### Example Request

*http -a test@gmail.com:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 PUT https://www.pollfish.com/api/public/v2/apps/b77bb0f8-5962-4882-a23c-2e6c9e99a84a  name=MyNewApp2 third_party_surveys_enabled:=false*

### Example Response
```json
{
  "api_key": "b77bb0f8-5962-4882-a23c-2e6c9e99a84a",
  "behavior": 1,
  "category": "IAB22",
  "subcategory": "IAB22-2",
  "id": 16659,
  "image": "",
  "incentive": true,
  "name": "MyNewApp2",
  "platform": "Android",
  "revenue": 0.0,
  "short_surveys_enabled": true,
  "third_party_surveys_enabled": false,
  "data_collection_surveys_enabled": true,
  "url": "https://play.google.com/store/apps/details?id=com.pollfish.demo",
  "rewarded_survey": {
    "currency_name": "Diamonds",
    "variable_amount": 300,
    "fixed_amount": true
  },
  "offerwall": {
    "currency_name": "Points",
    "variable_amount": 100
  }
}
```


## `4.4 DELETE /api/public/v2/apps/:api_key`

*Deletes an app*

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 204       | Successfully deleted the app
|2  | 403       | If an app with the specified api_key does not exist or you don\'t have the permissions to access the app

## `4.5 GET /api/public/v2/apps`

*Returns an array of apps of the user*

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response

###  Example Response

```json
[
  {
    "api_key": "b77bb0f8-5962-4882-a23c-2e6c9e99a84a",
    "behavior": 1,
    "category": "IAB3",
    "subcategory": "IAB3-2",
    "id": 16659,
    "image": "",
    "incentive": true,
    "name": "TestApp",
    "platform": "Android",
    "revenue": 0.0,
    "short_surveys_enabled": true,
    "third_party_surveys_enabled": true,
    "data_collection_surveys_enabled": true,
    "url": "http://www.example.com/test-app",
    "rewarded_survey": {
      "currency_name": "Diamonds",
      "variable_amount": 300,
      "fixed_amount": true
    },
    "offerwall": {
      "currency_name": "Points",
      "variable_amount": 100
    }
  }
]
```

## `4.6 GET /api/public/v3/apps/performance`

*returns the performance metrics for all the apps of the developer for a
designated time period*

The url can contain the following query parameters

### Parameter

|   | Name  | JSON Type     | Description                      | Required
|---|:------|:--------------|:---------------------------------|:--------
| 1 | from  | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the beginning of the time period for the query. <br>If omitted, the default is one month before parameter to. | No
| 2 | to    | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the end of the time period for the query. <br>If omitted, the default is the current date. | No


### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters <br>- **from** not is ISO 8601 format <br>- **to** not in ISO 8601 format


### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/performance?from=2018-07-01&to=2018-07-10](https://www.pollfish.com/api/public/v2/apps)*

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/performance?from=2018-07-04](https://www.pollfish.com/api/public/v2/apps)*

### Example Response

```json
[
  {
        "data": [
            {
                "accepted": 43,
                "completed": 32,
                "date": "2018-07-10",
                "seen": 89,
                "served": 127
            },
      {
        "accepted": 43,
        "completed": 32,
        "date": "2018-07-11",
        "seen": 89,
        "served": 127
      }
        ],
        "name": "Pollfish"
    },
  {
    "data": [
      {
        "accepted": 12,
        "completed": 29,
        "date": "2018-07-10",
        "seen": 60,
        "served": 100
      },
      {
        "accepted": 12,
        "completed": 29,
        "date": "2018-07-11",
        "seen": 60,
        "served": 100
      }
    ],
    "name": "Cint"
  }
]
```

## `4.7 GET /api/public/v3/apps/:api_key/performance`

returns the performance metrics of the specified app for a designated
time period

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters <br>- **from** not is ISO 8601 format <br>- **to** not in ISO 8601 format <br>- The **api_key** is invalid or does not belong to the user


### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/84e1a754-a261-40cf-b566-baa375b64e21/performance?from=2018-07-01&to=2018-07-10](https://www.pollfish.com/api/public/v2/apps)*

### Example Response

Same as above but include the performance metrics only for the specified
app.

## `4.8 GET /api/public/v3/apps/revenue`

returns the total revenue per provider for all the apps of the developer
for a designated time period and for selected countries

The url can contain the following query parameters

### **Parameter**

|   | Name  | JSON Type     | Description                      | Required
|---|:------|:--------------|:---------------------------------|:--------
| 1 | from  | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the beginning of the time period for the query. <br>If omitted, the default is one month before parameter to. | No
| 2 | to    | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the end of the time period for the query. <br>If omitted, the default is the current date. | No
| 3 | countries    | string        | A comma separated list of ISO Alpha-2 country codes for which the cummulative revenue is computed. <br>If omitted, all countries are assumed. | No

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters <br>- **from** not is ISO 8601 format <br>- **to** not in ISO 8601 format <br>- The **api_key** is invalid or does not belong to the user

### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/revenue?from=2018-07-01&to=2018-07-10](https://www.pollfish.com/api/public/v2/apps)*

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/revenue?from=2018-07-04](https://www.pollfish.com/api/public/v2/apps)*

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/revenue?countries=US,FR](https://www.pollfish.com/api/public/v2/apps)*

### Example Response

```json
[
    {
        "data": [
            {
                "amount": 20.0,
                "date": "2018-07-10"
            },
            {
                "amount": 20.0,
                "date": "2018-07-11"
            }
        ],
        "name": "Pollfish",
        "total": 40.0
    },
    {
        "data": [
            {
                "amount": 15.0,
                "date": "2018-07-10"
            },
            {
                "amount": 15.0,
                "date": "2018-07-11"
            }
        ],
        "name": "Pollfish-Playful",
        "total": 30.0
    },
    {
        "data": [
            {
                "amount": 5.0,
                "date": "2018-07-10"
            },
            {
                "amount": 5.0,
                "date": "2018-07-11"
            }
        ],
        "name": "Pollfish-Basic",
        "total": 10.0
    },
    {
        "data": [
            {
                "amount": 5.0,
                "date": "2018-07-10"
            },
            {
                "amount": 1.0,
                "date": "2018-07-11"
            }
        ],
        "name": "Toluna",
        "total": 6.0
    },
    {
        "data": [
            {
                "amount": 2.0,
                "date": "2018-07-10"
            },
            {
                "amount": 1.0,
                "date": "2018-07-11"
            }
        ],
        "name": "Cint",
        "total": 3.0
    },
    {
        "data": [
            {
                "amount": 7.0,
                "date": "2018-07-10"
            },
            {
                "amount": 3.0,
                "date": "2018-07-11"
            }
        ],
        "name": "Lucid",
        "total": 10.0
    }
]
```

## `4.9 GET /api/public/v3/apps/:api_key/revenue`

returns the total revenue per provider of the specified app for a
designated time period

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters <br>- **from** not is ISO 8601 format <br>- **to** not in ISO 8601 format <br>- The **api_key** is invalid or does not belong to the user

### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/84e1a754-a261-40cf-b566-baa375b64e21/revenue?from=2018-07-01&to=2018-07-10](https://www.pollfish.com/api/public/v2/apps)*

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/84e1a754-a261-40cf-b566-baa375b64e21/revenue?from=2018-07-01&to=2018-07-10&countries=US](https://www.pollfish.com/api/public/v2/apps)*

### Example Response

Same as above but include the revenue only for the specified app.


## `4.10 GET /api/public/v3/apps/demographics`

returns the demographic data for a particular user

The url can contain the following query parameters

### **Parameter**

|   | Name  | JSON Type     | Description                             | Required
|---|:------|:--------------|:----------------------------------------|:--------
| 1 | user  | string        | The device id to fetch demographics for | Yes

### Server Response

|   | Code      | Description
|---|:----------|:-----------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters


### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/demographics?user=4daf6394-4e9e-4d90-97b0-d665efad734b](https://www.pollfish.com/api/public/v2/apps)*

### Example Response

The codes are documented at
<https://www.pollfish.com/docs/demographic-surveys>

```json
{
    "career": 1,
    "device_id": "7ed91b48-b286-4d33-be87-f9f176fcc59e",
    "education": 2,
    "employment": 2,
    "gender": 1,
    "income": 1,
    "marital_status": 3,
    "parental": 2,
    "race": 2,
    "year_of_birth": 1985
}
```

## `4.11 GET /api/public/v3/apps/:api_key/users_log`

returns the user logs for a given device_id or request_uuid

The url can contain the following query parameters

### **Parameter**

|   | Name  | JSON Type     | Description                                  | Required
|---|:------|:--------------|:---------------------------------------------|:--------
| 1 | key   | string        | The search term (device_id or request_uuid)  | Yes
| 2 | page  | Int           | The Page number if results are paginated     | No
| 3 | rows  | Int           | The number of rows returned                  | No

### Server Response

|   | Code      | Description
|---|:----------|:-----------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters


### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/27278f6e-4197-492a-b8e9-e6478317e253/users_log?key=1](https://www.pollfish.com/api/public/v3/apps/27278f6e-4197-492a-b8e9-e6478317e253/users_log?key=1)*

### Example Response

```json
{
  "totalCount":3,
  "results":[
    {
      "id":"s_2_1544539226922_p",
      "survey_started":1544539226922,
      "completed":false,
      "disqualified_reason":"Survey Closed"
    },
    {
      "id":"s_4_1544539226922_p",
      "survey_started":1544539226922,
      "completed":true,
      "disqualified_reason": null
    },
    {
      "id":"s_5_15445657226922_p",
      "survey_started":1544264926922,
      "completed":false,
      "disqualified_reason": "Quota Full"
    }
  ]
}
```

### **List of available public termination reasons**


|    | Disqualification Reason  | Description                                 
|----|:-------------------------|:---------------------------------------------
| 1  | Quota Full               | The respondent selected a targeting question that had fulfilled its Quota.
| 2  | Survey Closed            | The respondent successfully answered a survey which was completed/closed while answering.
| 3  | Profiling                | The respondent was disqualified based on the targeting of the survey received.
| 4  | Screenout                | The respondent was screened out of the survey.
| 5  | Duplicate                | When a respondent has been received as a duplicate participation (ex: having the same id, found to be resetting their device_id to get the same survey twice etc...).
| 6  | Security                 | When we decide that there is a security reason to reject a respondent (ex: the respondent is banned from answering).
| 7  | VPN                      | The respondent is using a VPN.
| 8  | GeoMissmatch             | The respondent received a survey targeted for a different country than the one they are in.
| 9  | Quality                  | The respondent answered incorrectly in our Quality checks
| 10 | Hasty Answers            | The respondent answered consistently way faster than expected for the given questions.
| 11 | Gibberish                | The repondents answers contained gibberish in open-ended questions
| 12 | Captcha                  | A captcha check failed for the respondent.
| 13 | Third Party Termination  | A respondent was disqualified by a mediation partner.
| 14 | Banned Phrases           | The respondent answered in opened questions with phrases that are banned
| 15 | Disqualification Rules   | The respondent was disqualified since the responses between different similar questions were not consistent

> Note: We are working on making **Third Party Termination** reasons more verbose

## `4.12 GET /api/public/v3/apps/revenuePerCountry`

returns the total revenue per country for all the apps of the developer
for a designated time period and for selected countries

The url can contain the following query parameters

### **Parameter**

|   | Name  | JSON Type     | Description                      | Required
|---|:------|:--------------|:---------------------------------|:--------
| 1 | from  | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the beginning of the time period for the query. <br>If omitted, the default is one month before parameter to. | No
| 2 | to    | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the end of the time period for the query. <br>If omitted, the default is the current date. | No
| 3 | countries    | string        | A comma separated list of ISO Alpha-2 country codes for which the cummulative revenue is computed. <br>If omitted, all countries are assumed. | No

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters <br>- **from** not is ISO 8601 format <br>- **to** not in ISO 8601 format <br>- The **api_key** is invalid or does not belong to the user

### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 https://www.pollfish.com/api/public/v3/apps/revenuePerCountry?from=2018-07-01&to=2018-07-10*

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 https://www.pollfish.com/api/public/v3/apps/revenuePerCountry?from=2018-07-04*

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 https://www.pollfish.com/api/public/v3/apps/revenuePerCountry?countries=US,FR*

### Example Response

```json
[
  {
    "date": "2019-01-01",
    "total": 38.17,
    "countries": [
      {
        "iso_code": "us",
        "amount": 0.77
      },
      {
        "iso_code": "gb",
        "amount": 17.00 
      }
      ...
    ]
  },
  {
    "date": "2019-01-02",
    "total": 35.8,
    "countries": [
      {
        "iso_code": "us",
        "amount": 0.95
      },
      {
        "iso_code": "gb",
        "amount": 0.6
      }
      ...
    ]
  }
]
```

## `4.13 GET /api/public/v3/apps/:api_key/revenuePerCountry`

returns the total revenue per country of the specified app for a
designated time period

### **Parameter**

|   | Name  | JSON Type     | Description                      | Required
|---|:------|:--------------|:---------------------------------|:--------
| 1 | from  | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the beginning of the time period for the query. <br>If omitted, the default is one month before parameter to. | No
| 2 | to    | string        | A date in ISO8601 format (yyyy-MM-dd) . The timezone is UTC. This is the end of the time period for the query. <br>If omitted, the default is the current date. | No
| 3 | countries    | string        | A comma separated list of ISO Alpha-2 country codes for which the cummulative revenue is computed. <br>If omitted, all countries are assumed. | No

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters <br>- **from** not is ISO 8601 format <br>- **to** not in ISO 8601 format <br>- The **api_key** is invalid or does not belong to the user

### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 https://www.pollfish.com/api/public/v3/apps/84e1a754-a261-40cf-b566-baa375b64e21/revenuePerCountry?from=2018-07-01&to=2018-07-10*

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 https://www.pollfish.com/api/public/v3/apps/84e1a754-a261-40cf-b566-baa375b64e21/revenue?from=2018-07-01&to=2018-07-10&countries=US*

### Example Response

Same as above (section 4.12) but include the revenue only for the specified app.

## `4.14 GET /api/public/v3/apps/:api_key/performanceByCountry`

returns the performance metrics of the specified app for a designated
time period grouped by country

### Server Response

|   | Code      | Description
|---|:----------|:----------------------------------------------------------------------------------------------------------
|1  | 200       | Successful response
|2  | 400       | Missing or invalid parameters <br>- **from** not is ISO 8601 format <br>- **to** not in ISO 8601 format <br>- The **api_key** is invalid or does not belong to the user


### Example Requests

*http -a <test@gmail.com>:e1ecf034-ee26-4945-8db9-e5e8e0d22e53 [https://www.pollfish.com/api/public/v3/apps/84e1a754-a261-40cf-b566-baa375b64e21/performanceByCountry?from=2018-07-01&to=2018-07-10](https://www.pollfish.com/api/public/v2/apps)*

### Example Response

```
[
   {
      "countryISO" : "US",
      "data" : [
         {
            "network" : "Pollfish",
            "data" : [
               {
                  "accepted" : 0,
                  "date" : "2020-07-10",
                  "seen" : 0,
                  "served" : 0,
                  "completed" : 0
               },
               {
                  "completed" : 0,
                  "served" : 0,
                  "date" : "2020-07-11",
                  "seen" : 0,
                  "accepted" : 0
               }
               ...
            ]
         },
         {
            "network" : "Cint",
            "data" : [
               {
                  "accepted" : 0,
                  "seen" : 0,
                  "date" : "2020-07-10",
                  "served" : 0,
                  "completed" : 0
               },
               {
                  "seen" : 0,
                  "date" : "2020-07-11",
                  "accepted" : 0,
                  "served" : 0,
                  "completed" : 0
               }
              ...
            ]
         },
         ...
      ]
   },
   ...
]
```
