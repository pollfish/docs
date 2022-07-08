## Google Play Data Safety Questionnaire

All publishers must declare how they collect and handle user data for the apps they publish on Google Play and provide details about how they protect this data through security practices.

This declaration includes data collected and handled through any third party libraries or SDKs used in their apps. For more information please have a look at Google Play&#39;s Data safety section [here](https://support.google.com/googleplay/android-developer/answer/10787469).

In order to help with this process, we&#39;ve listed the data that Pollfish collects below. The following are relevant only to the data collected by the Pollfish SDK. The publishers are responsible for providing any additional disclosures for their app, including other third-party SDKs used. This guide is provided for convenience only and Pollfisht does not make any representations regarding such information, including but not limited to its accuracy or completeness.

Pollfish collects data in order to provide Market Research services and deliver targeted surveys to users while collecting insights for its clients. The main purpose for the data collection is Market Research however since that category is not available,we suggest listing the collected data under Advertising or Marketing purpose.

Pollfish submits all data collected under the https protocol. The data collected by Pollfish is not processed ephemerally, due to the nature of Pollfish Market Research monetization service.

Data listed here do not replace the Pollfish privacy policy. Publishers are requested to read the [Pollfish privacy policy](https://www.pollfish.com/terms/publisher) prior integrating the Pollfish SDK.

### **Data collection survey**

| **Question** | **Answer** | **Comments** |
| --- | --- | --- |
| Does the SDK collect or share any of the required user data types? | Yes |  |
| Is all of the data collected by the SDK encrypted in transit? | Yes | All submitted data are transmitted under the https protocol |
| Does the SDK provide a way for users to request that their data is deleted? | Yes | Users can reach out at any time at [support@pollfish.com](mailto:support@pollfish.com) with their requests or reset their Ad ID on their own |

### **Data handling**

Android Advertising ID collection happens automatically through the SDK if the relevant consent is provided by the user and the publisher has included the relevant permission in the Manifest.This Ad ID is used later on to target users with relevant surveys. The Ad ID can be reset or deleted at any time from the relevant Settings area on the device. If access to the Ad ID is limited, the SDK creates a one-off session id to be able to target users with non-personalised surveys.

### **Data types**

| **Location** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s approximate location? | Yes | Yes | No | Yes | Advertising or marketing, analytics,fraud prevention, security, and compliance | Pollfish collects and processes IP address, and infers approximate geolocation from IP address. |
| Does the SDK collect the user&#39;s precise location? | No | (N/A) | N/A | N/A | N/A | N/A |
&nbsp;
| **Personal information** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s name? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect the user&#39;s email address? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect the user&#39;s personal identifiers? | Yes | Yes | No | No | Advertising or marketing, analytics,fraud prevention, security, and compliance | Pollfish automatically collects the Ad ID of the user if access is not limited and the publisher provided the relevant permission. Publishers can also pass other user identifiers to the SDK. |
| Does the SDK collect the user&#39;s address? | No | N/A | N/A | N/A |  | N/A |
| Does the SDK collect the user&#39;s phone number? | No | N/A | N/A | N/A |  | N/A |
| Does the SDK collect the user&#39;s race and ethnicity? | Yes | Yes | No | No | Advertising or marketing,fraud prevention, security, and compliance | Users will answer similar questions if they wish as part of the demographic survey during onboarding https://www.pollfish.com/docs/demographic-surveys |
| Does the SDK collect the user&#39;s political or religious beliefs? | Yes | Yes | No | No | Advertising or marketing,fraud prevention, security, and compliance | Surveys from clients might ask such questions. The users decide if they would like to participate. |
| Does the SDK collect the user&#39;s sexual orientation or gender identity? | Yes | Yes | No | No | Advertising or marketing,fraud prevention, security, and compliance | Users will answer similar questions if they wish as part of the demographic survey during onboarding https://www.pollfish.com/docs/demographic-surveys |
| Does the SDK collect any of the user&#39;s other personal information? | Yes | Yes | No | No | Advertising or marketing,fraud prevention, security, and compliance | Users will answer different questions within the surveys if they decide to participate |
&nbsp;
| **Financial info** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s purchase history? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect the user&#39;s credit info? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect the user&#39;s credit card, debit card, or bank account number? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect any of the user&#39;s other financial info? | Yes | Yes | No | No | Advertising or marketing | Surveys from clients might ask such questions. The users decide if they would like to participate. |
&nbsp;
| **Health and fitness** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s health information? | Yes | Yes | No | No | Advertising or marketing | Surveys from clients might ask such questions. The users decide if they would like to participate. |
| Does the SDK collect the user&#39;s fitness information? | Yes | Yes | No | No | Advertising or marketing | Surveys from clients might ask such questions. The users decide if they would like to participate. |
&nbsp;
| **Messages** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s emails? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect the user&#39;s SMS or MMS messages? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect any of the user&#39;s other in-app messages? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **Photos and videos** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s photos? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect the user&#39;s videos? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **Audio files** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s voice or sound recordings? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect the user&#39;s music files? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect any of the user&#39;s other audio files? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **Files and docs** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s files and or documents? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **Calendar** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s calendar events? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **Contacts** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect the user&#39;s contacts? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **App activity** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect data on page views and taps in the app? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect in-app search history? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect data on installed apps? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect data on any other user-generated content? | Yes | Yes | No | No | Advertising or marketing | Surveys from clients might ask such questions. The users decide if they would like to participate. |
| Does the SDK collect data on any other app activity? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **Web browsing** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect data on the user&#39;s web browsing history? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **App info and performance** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect crash logs? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect app diagnostics? | No | N/A | N/A | N/A | N/A | N/A |
| Does the SDK collect any other app performance data? | No | N/A | N/A | N/A | N/A | N/A |
&nbsp;
| **Device or other identifiers** | **Collected** | **Shared** | **Ephemeral** | **Required** | **Purpose** | **Comments** |
| --- | --- | --- | --- | --- | --- | --- |
| Does the SDK collect data on the user&#39;s device or other identifiers? | Yes | Yes | No | No | Advertising or marketing, analytics, app functionality, fraud prevention, security, and compliance | Pollfish automatically collects the Ad ID of the user if access is not limited and the publisher provided the relevant permission. Publishers can also pass other user identifiers to the SDK |
