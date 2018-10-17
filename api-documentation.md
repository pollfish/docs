# Pollfish API Documentation

This document describes Pollfish API Documentation. Pollfish API is an
alternative to SDK and web plugin integration for publishers looking to
monetize their apps or websites with Pollfish surveys.

## Integration step-by-step

### 1. Obtain a Publisher Account

Register as a Publisher
at [www.pollfish.com/publisher](https://www.pollfish.com/login/publisher)

### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com/publisher](http://www.pollfish.com/publisher) and click "Add a new app" on Pollfish Developer Dashboard in section "My Apps". 
Copy the given API key for this app in order to use later on, when initializing Pollfish within your code.

### 3. Request a new survey from Pollfish servers

#### SERVER REGISTER

This call requests a new survey from Pollfish servers

#### REQUEST 

Structure:

```shell
https://wss.pollfish.com/v2/device/register/true?json={}&dontencrypt=true
```

-   This is a GET request

-   All register parameters shall be included in a JSON

-   Include `dontencrypt=true` in every request

-   All JSON parameters must be of type String but able to be converted
    in the required type. 
    ```js 
      // ie: "lat" property is expected to be of type "Long"
      {
        "lat":"30123123"  //valid
      }
    ```
    ```js
      {
        "lat":"foo"  //invalid. Value "foo" cannot be converted to Long.
      }
    ```
    ```js
      {
        "lat": 30123123  //invalid. Value is expected to be a string.
      }
    ```
-   Any param that is not marked as Static should not be filled with
    static content

-   The most params you can pass, the most exposure you might get to
    Pollfish survey inventory.


### JSON Parameters

|   | Name | Type  | Description                       | Value     | Static   |  Required
|---|:-----|:-----------|:-----------------------------|:----------|:---------|:-----------
|1  | **api_key** | String     | Pollfish API Key (step 2) |           | No       | Yes
|2  | **debug** | Boolean | Run Pollfish in Developer or Release mode | true / false ( defaults to false ) | No | Yes
|3  | **ip** | string | IP of user’s device  | | No | Yes
|4  | **device_id** | String | Advertising Identifier  (IDFA or Advertising ID)| | No | Yes
|5  | **timestamp** | Long | Timestamp of the request in milliseconds since January 1, 1970 00:00:00.0 UTC. | | No | Yes
|6  | **encryption** | String | Encrypt request | "NONE" | Yes | Yes
|7  | **version** | Int | Current version of API | 7 | Yes | Yes
|8  | **device_descr** | String | Product model name: <br>Android: device_model(device_product) <br>iOS: device_model | Android: android.os.Build.MODEL (android.os.Build.PRODUCT) <br>iOS: systemInfo.machine | No | No
|9  | **os** | Int | Operating system | Enumeration. See below for the list of possible values | No | Yes
|10 | **os_ver** | String | Framework version | Android: android.os.Build.VERSION.SDK_INT <br>iOS: systemVersion | No | No
|11 | **scr_h** | Int | Screen height in pixels | | No | No
|12 | **scr_w** | Int | Screen width in pixels | | No | No
|13 | **scr_size** | Float | Screen size in inch | | No | No
|14 | **con_type** | String | Network connection type | A human-readable name describe the type of the network, * for example "WIFI" / on iOS (Unknown, None, 3G, Wifi) | No | No
|15 | **lat** | Long | Location latitude (8 or 9 digits in total) | String((int)bestLocation.getLatitude() * 1E6) <br>*ONLY GPS/WIFI data. | No | No
|16 | **lon** | Long | Location longitude (8 or 9 digits in total) | String((int)bestLocation.getLatitude() * 1E6) <br>*ONLY GPS/WIFI data. | No | No
|17 | **accuracy** | Int | Location accuracy in meters | | No | No
|18 | **provider** | String | Name of current registered network operator | | No | No
|19 | **provider_mcc** | String | MCC of current registered network operator | | No | No
|20 | **provider_mnc** | String | MNC of current registered network operator | | No | No
|21 | **manufacturer** | String | Device's manufacturer | Android: android.os.Build.MANUFACTURER <br>iOS: "Apple" | No | No
|22 | **google_play** | Boolean | API used for google play app (“true”) or other market “false” (Android) | true / false | No | No
|23 | **applications** | String | List of installed applications (Android) | Package names comma separated "com.app1,com.app2” | No | No
|24 | **imei** | String | Device's IMEI (Android) | | No | No
|25 | **mac** | String | Device MAC address | | No | No
|26 | **nfc_exists** | Boolean | If NFC exists (Android) | | No | No
|27 | **nfc_enabled** | Boolean | If NFC is enabled (Android) | | No | No
|28 | **locale** | String | Device language code | Required from version 7 | No | Yes
|29 | **app_version** | String | App's version | Android: packageInfo.versionName + packageInfo.versionCode <br>iOS: "CFBundleShortVersionString"."CFBundleVersion" | No | No
|30 | **is_roaming** | Boolean | If device is roaming on current network | true / false | No | No
|31 | **hardware_accelerated** | Boolean | If hardware acceleration is on | true | Yes | No
|32 | **accessibility_enabled** | Boolean | If accessibility is enabled | | No | No
|33 | **developer_enabled** | Boolean | If developer options enabled on device (Android) | true / false | No | No
|34 | **install_non_market_apps** | Boolean | Check if install non market apps is enabled (Android) | true / false | No | No
|35 | **app_api_key** | String | App’s API key as registered in third party provider’s system | | No | No
|36 | **request_uuid** | String | Param passed through s2s postback calls to dev server | | No | No
|37 | **app_id** | String | App's package name | Android: Package name <br> iOS: Bundle ID | No | No
|38 | **app_name** | String | App's name | | No | No
|39 | **app_category** | String | App's category | | No | No
|40 | **app_subcategory** | String | App's subcategory | | No | No
|41 | **survey_id** | Int | Explicitly request a survey based on its id (only for on demand surveys) | | No | No
|42 | **opt_out** | Bool | Opt out from Interest-based advertising | true / false (defaults to false) | No | No
|43 | **usr_agent** | String | User agent | Android: System.getProperty("http.agent") <br>iOS: @"navigator.userAgent" | No | No
|44 | **target** | Int | Target SDK (Android) | | No | No
|45 | **board** | String | The name of the underlying board | Android: like "goldfish" <br>iOS: [[UIDevice currentDevice] model] | No | No
|46 | **serial** | String | A hardware serial number, if available. Alphanumeric only, case-insensitive (Android) | | No | No
|47 | **iap\*\*** | JSON Array | List of installed apps objects (Android) | See below | No | No
|48 <span class="demographics">•</span>| **gender** | Int | The gender of the user | Enumeration. See below for the list of possible values | No | No
|49 <span class="demographics">•</span>| **year_of_birth** | Int | The birth year of the user | A positive integer | No | No
|50 <span class="demographics">•</span>| **marital_status** | Int | The marital status of the user | Enumeration. See below for the list of possible values | No | No
|51 <span class="demographics">•</span>| **parental** | Int | How many kids the user has | Enumeration. See below for the list of possible values | No | No
|52 <span class="demographics">•</span>| **education** | Int | The education level of the user | Enumeration. See below for the list of possible values | No | No
|53 <span class="demographics">•</span>| **employment** | Int | The employment status of the user | Enumeration. See below for the list of possible values | No | No
|54 <span class="demographics">•</span>| **career** | Int | The industry that the user is employed in | Enumeration. See below for the list of possible values | No | No
|55 <span class="demographics">•</span>| **race** | Int | The race of the user | Enumeration. See below for the list of possible values | No | No
|56 <span class="demographics">•</span>| **income** | Int | The level of the income of the user | Enumeration. See below for the list of possible values | No | No
|57 | **personas \*\*\*** | JSON Object | The personas of the user | See below | No | No
|58 | **email** | String | The email of the user | A valid email address | No | No
|59 | **google_id** | String | The Google id of the user | | No | No
|60 | **linkedin_id** | String | The Linkedin id of the user | | No | No
|61 | **twitter_id** | String | The Twitter id of the user | | No | No
|62 | **facebook_id** | String | The Facebbok id of the user | | No | No
|63 | **survey_format** | String | The format of the survey to return (only available in debug mode, should be used for testing). | Enumeration. See below for the list of possible values | No | No


**Demographics**
<table>
  <tr>
    <td><span class="demographics">•</span></td>
    <td>Parameters from #48 to #56 are used in demographic surveys. If you already know this information you can provide them during register call and minimize or avoid demographic surveys.</td>
  </tr>
</table>

### Notes for `device_id`
___________________________

The recommended value is the Advertising Identifier (IDFA or Advertising
ID) which can be retrieved programmatically from the device. If this is
not the case, as when integrating with the API or Webplugin then any
unique identifiable string (UUID) for each user can be used instead
subject to the following recommendations:

-   The same user has the same device\_id most of the time. This ensures
    a user is uniquely identified and we do not repeat the demographic
    questions for every survey.

-   The device_id must identify a user across all apps/integrations.
    This ensures a user is unambiguously identified and is not confused
    for another user of another app/integration.

These rules help Pollfish provide good conversion rates for an
application.

### Enumerations

|  | Key     | Name          | Value
|--|:--------|:--------------|:----------
|9 | **os**  | Android       | 0
|  |         | iOS           | 1
|  |         | Windows Phone | 2
|  |         | Web           | 3

<br>

|  | Key         | Name          | Value
|--|:------------|:--------------|:----------
|48| **gender**  | FEMALE        | 1
|  |             | MALE          | 2
|  |             | OTHER         | 3

<br>

|  | Key                 | Name                | Value
|--|:--------------------|:--------------------|:----------
|50| **marital_status**  | SINGLE              | 0
|  |                     | MARRIED             | 1
|  |                     | DIVORCED            | 2
|  |                     | LIVING_WITH_PARTNER | 3
|  |                     | SEPARATED           | 4
|  |                     | WIDOWED             | 5
|  |                     | PREFER_NOT_TO_SAY   | 6

<br>

|  | Key                 | Name                | Value
|--|:--------------------|:--------------------|:----------
|51| **parental**        | ZERO                | 0
|  |                     | ONE                 | 1
|  |                     | TWO                 | 2
|  |                     | THREE               | 3
|  |                     | FOUR                | 4
|  |                     | FIVE                | 5
|  |                     | SIX_OR_MORE         | 6
|  |                     | PREFER_NOT_TO_SAY   | 7

<br>

|  | Key                 | Name                | Value
|--|:--------------------|:--------------------|:----------
|52| **education**       | ELEMENTARY_SCHOOL   | 0
|  |                     | MIDDLE_SCHOOL       | 1
|  |                     | HIGH_SCHOOL         | 2
|  |                     | VOCATION_TECHNICAL_COLLEGE | 3
|  |                     | UNIVERSITY          | 4
|  |                     | POST_GRADUATE       | 5

<br>

|  | Key                 | Name                | Value
|--|:--------------------|:--------------------|:----------
|53| **employment**      | EMPLOYED_FOR_WAGES  | 0
|  |                     | SELF_EMPLOYED       | 1
|  |                     | UNEMPLOYED_LOOKING  | 2
|  |                     | UNEMPLOYED_NOT_LOOKING | 3
|  |                     | HOMEMAKER           | 4
|  |                     | STUDENT             | 5
|  |                     | MILITARY            | 6
|  |                     | RETIRED             | 7
|  |                     | UNABLE_TO_WORK      | 8
|  |                     | OTHER               | 9

<br>

|  | Key                 | Name                                     | Value
|--|:--------------------|:-----------------------------------------|:----------
|54| **career**          | AGRICULTURE_FORESTRY_FISHING_OR_HUNTING  | 0
|  |                     | ARTS_ENTERTAINMENT_OR_RECREATION         | 1
|  |                     | BROADCASTING                             | 2
|  |                     | CONSTRUCTION                             | 3
|  |                     | EDUCATION                                | 4
|  |                     | FINANCE_AND_INSURANCE                    | 5
|  |                     | GOVERNMENT_AND_PUBLIC_ADMINISTRATION     | 6
|  |                     | HEALTH_CARE_AND_SOCIAL_ASSISTANCE        | 7
|  |                     | HOMEMAKER                                | 8
|  |                     | HOTEL_AND_FOOD_SERVICES                  | 9
|  |                     | INFORMATION_OTHER                        | 10
|  |                     | INFORMATION_SERVICES_AND_DATA            | 11
|  |                     | LEGAL_SERVICES                           | 12
|  |                     | MANUFACTURING_COMPUTER_AND_ELECTRONICS   | 13
|  |                     | MANUFACTURING_OTHER                      | 14
|  |                     | MILITARY                                 | 15
|  |                     | MINING                                   | 16
|  |                     | PROCESSING                               | 17
|  |                     | PUBLISHING                               | 18
|  |                     | REAL_ESTATE_RENTAL_OR_LEASING            | 19
|  |                     | RELIGIOUS                                | 20
|  |                     | RETAIL                                   | 21
|  |                     | RETIRED                                  | 22
|  |                     | SCIENTIFIC_OR_TECHNICAL_SERVICES         | 23
|  |                     | SOFTWARE                                 | 24
|  |                     | STUDENT                                  | 25
|  |                     | TELECOMMUNICATIONS                       | 26
|  |                     | TRANSPORTATION_AND_WAREHOUSING           | 27
|  |                     | UNEMPLOYED                               | 28
|  |                     | UTILITIES                                | 29
|  |                     | WHOLESALE                                | 30
|  |                     | OTHER                                    | 31

<br>

|  | Key                 | Name                | Value
|--|:--------------------|:--------------------|:----------
|55| **race**            | ARAB                | 0
|  |                     | ASIAN               | 1
|  |                     | BLACK               | 2
|  |                     | WHITE               | 3
|  |                     | HISPANIC            | 4
|  |                     | LATINO              | 5
|  |                     | MULTIRACIAL         | 6
|  |                     | OTHER               | 7
|  |                     | PREFER_NOT_TO_SAY   | 8

<br>

|  | Key                 | Name                | Value
|--|:--------------------|:--------------------|:----------
|56| **income**          | LOWER_I             | 0
|  |                     | LOWER_II            | 1
|  |                     | MIDDLE_I            | 2
|  |                     | MIDDLE_II           | 3
|  |                     | HIGH_I              | 4
|  |                     | HIGH_II             | 5
|  |                     | HIGH_III            | 6
|  |                     | PREFER_NOT_TO_SAY   | 7


### JSON Objects

#### \*\* installed apps JSON Array (iap)

<table>
  <tr>
    <td>47</td>
    <td><b>iap</b></td>
  </tr>
</table>


An installed app's JSON object should be added only if package name is
not null. Do not send system apps.

|  | Name            | Type                | Description                 | Required
|--|:----------------|:--------------------|:----------------------------|:------------------
|1 | **pn**          | String              | Package name                | true
|2 | **fi**          | Long                | First installed date        | false
|3 | **lm**          | Long                | Last modified date          | false


### **\*\*personas JSON Object**

<table>
  <tr>
    <td>57</td>
      <td><b>personas</b></td>
  </tr>
</table>

The personas of a user. You can read more about Pollfish personas
[here](https://www.pollfish.com/lp/pollfish-personas/). This is a JSON
object with optional boolean parameters for each persona. Please
specify `true` or `false` only if you know that a user has or doesn't
have the persona, else do not specify a value for the field.

|  | Name              | Type                | Required
|--|:------------------|:--------------------|:---------------------------
|1 | **good_listener** | Boolean             | false
|2 | **workaholic**    | Boolean             | false
|3 | **bookworm**      | Boolean             | false
|4 | **socialite**     | Boolean             | false
|5 | **globetrotter**  | Boolean             | false
|6 | **sportsfan**     | Boolean             | false
|7 | **gamer**         | Boolean             | false
|8 | **value_shopper** | Boolean             | false
|9 | **food_and_dining_lover** | Boolean     | false
|10| **entertainment_enthusiast** | Boolean  | false
|11| **fashionista**   | Boolean             | false

|  | Key                 | Name                | Value
|--|:--------------------|:--------------------|:----------
|63| **survey_format**   | Basic               | 0
|  |                     | Short               | 1
|  |                     | Random              | 2
|  |                     | Third Party         | 3

### Example Requests

Example request

[https://wss.pollfish.com/v2/device/register/true?json={\"api\_key\":\"27278f6e-4197-492a-b8e9-e6478317e253\",\"device\_id\":\"112123-a12331fd\",\"timestamp\":\"1417149043057\",\"encryption\":\"NONE\",\"version\":\"5\",\"device\_descr\":\"IPhone%205S\",\"os\":\"1\",\"os\_ver\":\"1\",\"scr\_h\":\"500\",\"scr\_w\":\"400\",\"scr\_size\":\"4\",\"con\_type\":\"wifi\",\"lat\":\"-32452123\",\"lon\":\"-32452123\",\"accuracy\":\"20\",\"ip\":\"8.8.8.8\",\"provider\":\"T-Mobile\",\"provider\_mcc\":\"202\",\"provider\_mnc\":\"05\",\"manufacturer\":\"nokia\",\"hardware\_accelerated\":\"true\",\"app\_api\_key\":\"provided\_by\_you\",\"request\_uuid\":\"provided\_by\_you\",\"app\_name\":\"Quiz\",\"app\_category\":\"Game\",\"debug\":\"true\"}&dontencrypt=true](https://wss.pollfish.com/v2/device/register/true?json={\"api\_key\":\"27278f6e-4197-492a-b8e9-e6478317e253\",\"device\_id\":\"112123-a12331fd\",\"timestamp\":\"1417149043057\",\"encryption\":\"NONE\",\"version\":\"5\",\"device\_descr\":\"IPhone%205S\",\"os\":\"1\",\"os\_ver\":\"1\",\"scr\_h\":\"500\",\"scr\_w\":\"400\",\"scr\_size\":\"4\",\"con\_type\":\"wifi\",\"lat\":\"-32452123\",\"lon\":\"-32452123\",\"accuracy\":\"20\",\"ip\":\"8.8.8.8\",\"provider\":\"T-Mobile\",\"provider\_mcc\":\"202\",\"provider\_mnc\":\"05\",\"manufacturer\":\"nokia\",\"hardware\_accelerated\":\"true\",\"app\_api\_key\":\"provided\_by\_you\",\"request\_uuid\":\"provided\_by\_you\",\"app\_name\":\"Quiz\",\"app\_category\":\"Game\",\"debug\":\"true\"}&dontencrypt=true)

Example request ( with user attributes ) 

[https://wss.pollfish.com/v2/device/register/true?json={"api_key":"27278f6e-4197-492a-b8e9-e6478317e253","device_id":"112123-a12331fd","timestamp":"1417149043057","encryption":"NONE","version":"5","device_descr":"IPhone%205S","os":"1","os_ver":"1","scr_h":"500","scr_w":"400","scr_size":"4","con_type":"wifi","lat":"-32452123","lon":"-32452123","accuracy":"20","ip":"8.8.8.8","provider":"T-Mobile","provider_mcc":"202","provider_mnc":"05","manufacturer":"nokia","hardware_accelerated":"true","app_api_key":"provided_by_you","request_uuid":"provided_by_you","app_name":"Quiz","app_category":"Game","email":"user@example.com","year_of_birth":"1990","gender":"1","marital_status":"0","parental":"0","education":"2","race":"0","twitter_id":"916809126","personas":{"gamer":"true"},"debug":"true"}&dontencrypt=true](https://wss.pollfish.com/v2/device/register/true?json={"api_key":"27278f6e-4197-492a-b8e9-e6478317e253","device_id":"112123-a12331fd","timestamp":"1417149043057","encryption":"NONE","version":"5","device_descr":"IPhone%205S","os":"1","os_ver":"1","scr_h":"500","scr_w":"400","scr_size":"4","con_type":"wifi","lat":"-32452123","lon":"-32452123","accuracy":"20","ip":"8.8.8.8","provider":"T-Mobile","provider_mcc":"202","provider_mnc":"05","manufacturer":"nokia","hardware_accelerated":"true","app_api_key":"provided_by_you","request_uuid":"provided_by_you","app_name":"Quiz","app_category":"Game","email":"user@example.com","year_of_birth":"1990","gender":"1","marital_status":"0","parental":"0","education":"2","race":"0","twitter_id":"916809126","personas":{"gamer":"true"},"debug":"true"}&dontencrypt=true)


*\* Notice that you might need to change the timestamp to current values
for the links above to operate properly.*

### RESPONSE CODES

The webservice will reply with an HTML response and a response code, as
explained below.


|  | Code              | Description
|--|:------------------|:----------------
|1 | **5xx**           | Internal Error
|2 | **4xx**           | Bad request
|3 | **204**           | No survey available
|4 | **200**           | Survey available         

You can also check if there is a survey available by getting the
Response Code without the HTML response if you perform a HEAD request.

### RESPONSE HEADER

Server responses include a header parameter called **CPA** that shows
the money to be earned from survey received in US dollar cents.

### RESPONSE BODY

A displayable HTML page

#### **MRAID library (optional)**

Pollfish can use MRAID library from IAB (<http://www.iab.net/MRAID>)
implemented in a web container. Pollfish will use the mraid.close()  in
order to operate properly.

## 4. Server-to-server callbacks

You can register and listen for two server-to-server callback events:

-   Survey Completion

-   User Not Eligible

In the following [link](https://www.pollfish.com/docs/s2s) you can find
a step by step guide on how to register and receive these callbacks.

Note: If you want to pass and receive your app\'s api key (param 35)
through server-to-server callbacks you can easily do it by appending
that param to the callback structure as explained in the link above.

<table>
  <tr>
    <td><b>app_api_key</b></td>
    <td>String</td>
    <td>App's api key as registered on third party provider's system</td>
  </tr>
</table>

## 5. Events

When the html file loads on the user side, there are
several javascript events that can be fired through the lifetime of a
Pollfish survey:


|  | Event                  | Description
|--|:-----------------------|:----------------
|1 | **close**              | When a user clicks on close button
|2 | **closeAndNoShow**     | When a user clicks on close button
|3 | **userNotEligible**    | When a user successfully completed a survey <br>(NOTICE: Further investigation of the response will be done on the server side to detect e.g fraudulent activites, so make sure to use the server-to-server callbacks, as described in section 4 to track valid responses prior crediting users)
|4 | **setSurveyCompleted** | When a user was not qualified to complete the survey (screened-out)         
|5 | **userRejectedSurvey** | When a user selected the "No thanks" option on the homescreen, or when a user selected the "I will not participate in this survey" button when on the GDPR page

Below you can find some examples of how to catch and handle the events
described above:

```js
window.onmessage = function(e){
    if(e.data === 'close' || e.data === 'closeAndNoShow'){
        // Handle the event of user clicking to close the survey
    }
}
```
```js
window.onmessage = function(e){
    if(e.data === 'userNotEligible'){
        // Handle the event when a user gets screened out
    }
}
```
```js
window.onmessage = function(e){
    if(e.data === 'setSurveyCompleted'){
        // Handle the event when a user sucessfully completes the survey
    }
}
```
- Get revenue of a survey before rendering to the user

```js
window.onmessage = function(e){
    if(e && e.data && e.data.indexOf && e.data.indexOf('surveyInfo') > -1){
        var data = JSON.parse(e.data);
        if(data.type === 'surveyInfo'){
            // Get revenue of survey
            console.log(data.revenue);   
        }
   }
}
```
```js
window.onmessage = function(e){
    if(e.data === 'userRejectedSurvey'){
        // Handle the event when a user rejected a survey prompt
    }
}
```
You can check out our sample project on how to implement an API
integration here : <https://github.com/pollfish/api-pollfish>


<style>
    .demographics {
        color: #95bde2;
        font-size: 22px;
        padding-top: 15px;
        vertical-align: top;
    }
</style>
