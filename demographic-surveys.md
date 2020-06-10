## Demographic Surveys

When a user is first introduced to the platform, if no paying surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure to our clients' survey inventory. This survey returns no payment to app publishers, as it is part of the process users need to go through in order to join the platform. Bear in mind that if a paid survey is available at that point in time, the demographic questions will be inserted at the beginning of the paying survey, before the actual survey questions.

Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this new type of targeting.

 
You can see an example of how we use this info on our targeting page of the DIY survey tool below:

![alt text](https://user-images.githubusercontent.com/2513939/67956229-68cb6000-fbfc-11e9-9ff3-360e8172d344.png)

and in our Results page:

![alt text](https://user-images.githubusercontent.com/2513939/67956237-6b2dba00-fbfc-11e9-8658-2fb1bbbf1d82.png)

<b>Publishers have the power</b>

In our efforts to include publishers in this process and be as transparent as possible, we are providing full control over the process. We are letting publishers decide whether their users are served these standalone surveys or not in three ways:

1) By monitoring the process in code and excluding any users by listening to the relevant notifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Bear in mind that by filtering out all surveys with PPS 0 will also stop all free internal surveys, since they also have a PPS of 0.

2) By providing an option to disable Standalone Demographic Surveys through the Settings section of an app on Pollfish Developer Dashboard, without the need to make any changes in code. (Changes are effective immediately.)

![alt text](https://user-images.githubusercontent.com/2513939/67956242-6c5ee700-fbfc-11e9-87bf-2d408115829d.png)

3) By submitting known user attributes like gender or age, during initialization in code, you may skip some or all of the questions in our Demographic surveys.  

| **Note:** <b> Bear in mind, that you need to contact our Support Department to ask them to acknowledge the information you have provided and mark you as eligible for providing such info through the library!</b>


If you know upfront some user attributes like gender, age, education and others you can pass them during initialization.

Below you can find the list of demographic info you can send over along with the relevant keys and mappings.

### Keys & Mappings

 **Note:** Both key and values should be eventually converted to strings prior sending over through the relevant functions within the library

| Key | Description | Value |
| --- | --- | --- |
| `gender` | FEMALE | 1
|  | MALE | 2
|  | OTHER | 3

</br>

| Key | Description | Value |
| --- | --- | --- |
| `marital_status` | SINGLE | 0
|  | MARRIED | 1
|  | DIVORCED | 2
|  | LIVING_WITH_PARTNER | 3
|  | SEPARATED | 4
|  | WIDOWED | 5
|  | PREFER_NOT_TO_SAY | 6

</br>

| Key | Description | Value |
| --- | --- | --- |
| `parental` | ZERO | 0
|  | ONE | 1
|  | TWO | 2
|  | THREE | 3
|  | FOUR | 4
|  | FIVE | 5
|  | SIX_OR_MORE | 6
|  | PREFER_NOT_TO_SAY | 7

</br>

| Key | Description | Value |
| --- | --- | --- |
| `education` | ELEMENTARY_SCHOOL | 0
|  | MIDDLE_SCHOOL | 1
|  | HIGH_SCHOOL | 2
|  | VOCATIONAL_TECHNICAL_COLLEGE | 3
|  | UNIVERSITY | 4
|  | POST_GRADUATE | 5

</br>

| Key | Description | Value |
| --- | --- | --- |
| `employment` | EMPLOYED_FOR_WAGES | 0
|  | SELF_EMPLOYED | 1
|  | UNEMPLOYED_LOOKING | 2
|  | UNEMPLOYED_NOT_LOOKING | 3
|  | HOMEMAKER | 4
|  | STUDENT | 5
|  | MILITARY | 6
|  | RETIRED | 7
|  | UNABLE_TO_WORK | 8
|  | OTHER | 9

</br>

| Key | Description | Value |
| --- | --- | --- |
| `career` | AGRICULTURE_FORESTRY_FISHING_OR_HUNTING | 0
|  | ARTS_ENTERTAINMENT_OR_RECREATION | 1
|  | BROADCASTING | 2
|  | CONSTRUCTION | 3
|  | EDUCATION | 4
|  | FINANCE_AND_INSURANCE | 5
|  | GOVERNMENT_AND_PUBLIC_ADMINISTRATION | 6
|  | HEALTH_CARE_AND_SOCIAL_ASSISTANCE | 7
|  | HOMEMAKER | 8
|  | HOTEL_AND_FOOD_SERVICES | 9
|  | INFORMATION_OTHER | 10
|  | INFORMATION_SERVICES_AND_DATA | 11
|  | LEGAL_SERVICES | 12
|  | MANUFACTURING_COMPUTER_AND_ELECTRONICS | 13
|  | MANUFACTURING_OTHER | 14
|  | MILITARY | 15
|  | MINING | 16
|  | PROCESSING | 17
|  | PUBLISHING | 18
|  | REAL_ESTATE_RENTAL_OR_LEASING | 19
|  | RELIGIOUS | 20
|  | RETAIL | 21
|  | RETIRED | 22
|  | SCIENTIFIC_OR_TECHNICAL_SERVICES | 23
|  | SOFTWARE | 24
|  | STUDENT | 25
|  | TELECOMMUNICATIONS | 26
|  | TRANSPORTATION_AND_WAREHOUSING | 27
|  | UNEMPLOYED | 28
|  | ENERGY_UTILITIES_OIL_AND_GAS | 29
|  | WHOLESALE | 30
|  | OTHER | 31
|  | ADVERTISING | 32
|  | AUTOMOTIVE | 33
|  | CONSULTING | 34
|  | FASHION_APPAREL | 35
|  | HUMAN_RESOURCES | 36
|  | MARKET_RESEARCH | 37
|  | MARKETING_SALES | 38
|  | SHIPPING_DISTRIBUTION | 39
|  | PERSONAL_SERVICES | 40
|  | SECURITY | 41

</br>

| Key | Description | Value |
| --- | --- | --- |
| `race` | ARAB | 0
|  | ASIAN | 1
|  | BLACK | 2
|  | WHITE | 3
|  | HISPANIC | 4
|  | LATINO | 5
|  | MULTIRACIAL | 6
|  | OTHER | 7
|  | PREFER_NOT_TO_SAY | 8

</br>

| Key | Description | Value |
| --- | --- | --- |
| `income` | LOWER_I | 0
|  | LOWER_II | 1
|  | MIDDLE_I | 2
|  | MIDDLE_II | 3
|  | HIGH_I | 4
|  | HIGH_II | 5
|  | HIGH_III | 6
|  | PREFER_NOT_TO_SAY | 7

</br>

| Key | Description | Value |
| --- | --- | --- |
| `spoken_languages` | ENGLISH | 0
|  | ARABIC | 1
|  | BULGARIAN | 2
|  | CHINESE | 3
|  | CZECH | 4
|  | DANISH | 5
|  | DUTCH | 6
|  | FILIPINO | 7
|  | THAI | 8
|  | FINNISH | 9
|  | FRENCH | 10
|  | GERMAN | 11
|  | GREEK | 12
|  | HINDI | 13
|  | INDONESIAN | 14
|  | ITALIAN | 15
|  | JAPANESE | 16
|  | POLISH | 17
|  | PORTUGUESE | 18
|  | ROMANIAN | 20
|  | RUSSIAN | 21
|  | SERBIAN | 22
|  | SPANISH | 23
|  | SWEDISH | 24
|  | TURKISH | 25
|  | VIETNAMESE | 26
|  | KOREAN | 27
|  | HUNGARIAN | 28
|  | CHINESE_TRANDITIONAL | 29
|  | NORWEGIAN | 30
|  | EGYPTIAN | 31
|  | UKRANIAN | 32
|  | HEBREW | 33
|  | BENGALI | 34
|  | SLOVAK | 35
|  | PERSIAN | 36
|  | AZERBAIJANI | 37
|  | GEORGIAN | 38
|  | LITHUANIAN | 39
|  | PUNJABI | 40
|  | PASHTO | 41
|  | ESTONIAN | 42
|  | UZBEK | 43

| Key | Description | Value |
| --- | --- | --- |
| `organization_role` | OWNER_PARTNER | 0
|  | PRESIDENT_CEO_CHAIRPERSON | 1
|  | C_LEVEL_EXECUTIVE | 2
|  | MIDDLE_MANAGEMENT | 3
|  | CHIEF_FINANCIAL_OFFICER | 4
|  | CHIEF_TECHNICAL_OFFICER | 5
|  | SENIOR_MANAGEMENT | 6
|  | DIRECTOR | 7
|  | HR_MANAGER | 8
|  | PRODUCT_MANAGER | 9
|  | SUPPLY_MANAGER | 10
|  | PROJECT_MANAGEMENT | 11
|  | SALES_MANAGER | 12
|  | BUSINESS_ADMINISTRATOR | 13
|  | SUPERVISOR | 14
|  | ADMINISTRATIVE_CLERICAL | 15
|  | CRAFTSMAN | 16
|  | FOREMAN | 17
|  | TECHNICAL_STAFF | 18
|  | FACULTY_STAFF | 19
|  | SALES_STAFF | 20
|  | BUYER_PURCHASING_AGENT | 21
|  | OTHER_NON_MANAGEMENT | 22
|  | NOT_WORK | 23
|  | PREFER_NOT_TO_SAY | 24

</br>

| Key | Description | Value |
| --- | --- | --- |
| `number_of_employees` | ONE | 0
|  | TWO_TO_FIVE | 1
|  | SIX_TO_TEN | 2
|  | ELEVEN_TO_TWENTY_FIVE | 3
|  | TWENTY_SIX_TO_FIFTY | 4
|  | FIFTY_ONE_TO_HUNDREND | 5
|  | HUNDREND_ONE_TO_TWO_HUNDRENDS_FIFTY | 6
|  | TWO_HUNDRENDS_FIFTY_ONE_TO_FIVE_HUNDRENDS | 7
|  | FIVE_HUNDRENDS_ONE_TO_THOUSAND | 8
|  | THOUSAND_ONE_TO_FIVE_THOUSANDS | 9
|  | GREATER_THAN_FIVE_THOUSANDS | 10
|  | DO_NOT_WORK | 11
|  | PREFER_NOT_TO_SAY | 12

If you need to find household income mapping for a specific country you can have a look at the following [link](https://www.pollfish.com/pf/household-income-mapping)

### Server-to-server callbacks for demographics

Publishers can get all the demographic data that we collect from their users via server-to-server callbacks. This feature can be enabled per app by specifying a "Demographics URL" in the app's settings in the Pollfish dashboard.

When this URL is specifed Pollfish will make an HTTP **PUT** request to that URL with a JSON body that contains all demographic information that we currently know about the user.

For example if you specify the following URL template: http://www.example.com?user=[[device_id]] when a user with device_id "ed9111bb-8859-4f55-8bf6-0f7f4a289d7c" answers the demographic questions we will make a PUT request to:

```
http://www.example.com?user=ed9111bb-8859-4f55-8bf6-0f7f4a289d7c
```

with an example body:

```
{
  "device_id":"ed9111bb-8859-4f55-8bf6-0f7f4a289d7c",
  "gender":2,
  "year_of_birth":1980,
  "marital_status":1,
  "parental":1,
  "education":3,
  "employment":0,
  "career":13,
  "race":8,
  "income":6,
  "spoken_languages":[0,23],
  "organization_role":15,
  "number_of_employees":3,
  "postal_code":"11527"
}
```

Please note that because we will make the request if the user answers all the demographic question or if he/she answers some of the questions and quits the survey you might receive multiple requests for the same user.

**NOTE!:** This is only working for production surveys. When debugging (and flag debug is true) these events will not fire
