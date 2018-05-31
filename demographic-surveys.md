## Demographic Surveys

When a user is first introduced to the platform, if no paying surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure to our clients' survey inventory. This survey returns no payment to app publishers, as it is part of the process users need to go through in order to join the platform. Bear in mind that if a paid survey is available at that point in time, the demographic questions will be inserted at the beginning of the paying survey, before the actual survey questions.

Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this new type of targeting.

 
You can see an example of how we use this info on our targeting page of the DIY survey tool below:

![alt text](https://pollfish.zendesk.com/hc/article_attachments/208100469/targeting.png)

and in our Results page:

![alt text](https://pollfish.zendesk.com/hc/article_attachments/208100489/results.png)

<b>Publishers have the power</b>

In our efforts to include publishers in this process and be as transparent as possible, we are providing full control over the process. We are letting publishers decide whether their users are served these standalone surveys or not in three ways:

1) By monitoring the process in code and excluding any users by listening to the relevant notifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Bear in mind that by filtering out all surveys with PPS 0 will also stop all free internal surveys, since they also have a PPS of 0.

2) By providing an option to disable Standalone Demographic Surveys through the Settings section of an app on Pollfish Developer Dashboard, without the need to make any changes in code. (Changes are effective immediately.)

![alt text](https://pollfish.zendesk.com/hc/en-us/article_attachments/208795189/receiving.png)

3) By submitting known user attributes like gender or age, during initialization in code, you may skip some or all of the questions in our Demographic surveys.  

| **Note:** <b> Bear in mind, that you need to contact our Support Department to ask them to acknowledge the information you have provided and mark you as eligible for providing such info through the library!</b>


If you know upfront some user attributes like gender, age, education and others you can pass them during initialization.

Below you can find the list of demographic info you can send over along with the relevant keys and mappings:

### Keys

![alt text](https://storage.googleapis.com/pollfish-images/demographic.png)

| **Note:** Both key and values should be eventually converted to strings prior sending over through the relevant functions within the library

### Mappings

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
|  | UTILITIES | 29
|  | WHOLESALE | 30
|  | OTHER | 31

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
|  | HIGHT_I | 4
|  | HIGHT_II | 5
|  | HIGHT_III | 6
|  | PREFER_NOT_TO_SAY | 7

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
  "device_id":"ed9111bb-8859-4f55-8bf6-0f7f4a289d7c"
  "gender":2,
  "year_of_birth":1980,
  "marital_status":1,
  "parental":1,
  "education":3,
  "employment":0,
  "career":13,
  "race":8,
  "income":6
}
```

Please note that because we will make the request if the user answers all the demographic question or if he/she answers some of the questions and quits the survey you might receive multiple requests for the same user.
