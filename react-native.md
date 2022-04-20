Pollfish React Native plugin, allows integration of Pollfish surveys into Android and iOS apps.

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.

Pollfish React Native Plugin can be found on [npm Registry](https://www.npmjs.com/package/react-native-plugin-pollfish). The source code and an example app can be found on [Github](https://github.com/pollfish/react-native-plugin-pollfish).

<br/>

# Prerequisites

* Android SDK 21 or higher using Google Play Services
* iOS 9.0 or higher
* React Native v0.40 or higher
* CocoaPods v1.10.0 or higher

<br/>

> **Note:** Apps designed for [Children and Families program](https://play.google.com/about/families/ads-monetization/) should not be using Pollfish SDK, since Pollfish does not collect responses from users less than 16 years old

> **Note:** Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower. Offerwall integrations perform better compared to single survey integrations when no IDFA permission is given

<br/>

# Quick Guide

* Create Pollfish Developer account
* Create new apps for each targeting platform (Android & iOS) and grap the API keys
* Install Pollfish plugin and call init function
* Set to Release mode and publish on app store
* Update your app's privacy policy
* Request your account to get verified from Pollfish Dashboard

<br/>

# Migrate to v2

Pollfish React Native Plugin v2 introduces a different API with added customization options during initialization. If you have already integrated Pollfish React Native Plugin < v2 in you app, please take some time reading the migration guide below.

<details><summary>➤ <b>Migration Guide</b> (Click to expand)</summary>
<table>
<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialization** <br/>

```js
var params = new RNPollfish.Builder('API_KEY');
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```js
var params = new RNPollfish.Builder('ANDRPOD_API_KEY', 'IOS_API_KEY');
```

</table>
</details>

<br/>

# Analytical Steps

## 1. Obtain a Developer Account

Register as a Developer at [www.pollfish.com](http://www.pollfish.com)

<br/>

## 2. Add new apps in Pollfish panel and copy the given API Keys

Login at [www.pollfish.com](http://www.pollfish.com) and add a new app at Pollfish panel in section My Apps and copy the given API key for this app to use later in your init function in your app.

<br/>

## 3. Installing the plugin

To add Pollfish plugin just type: 

Using `yarn`
```bash
yarn add react-native-plugin-pollfish
```

Using `npm`
```bash
npm install react-native-plugin-pollfish
```

And for iOS builds

```bash
cd ios && pod install && cd ..
```

<br/>

**Android 12**

Apps updating their target API level to 31 (Android 12) or higher will need to declare a Google Play services normal permission in the AndroidManifest.xml file.

Navigate to the `android/app/src/main` directory inside your project's root, locate the AndroidManifest.xml file and add the following line just before the `<application>`.

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

You can read more about Google Advertising ID changes [here](https://support.google.com/googleplay/android-developer/answer/6048248).

<br/>

## 4. Import `RNPollfish` module

```js
import RNPollfish from 'react-native-plugin-pollfish';
```

<br/>

## 4. Create a `RNPollfish.Builder` instance

The Pollfish plugin must be initialized with one or two api keys depending on which platforms are you targeting. You can retrieve an API key from Pollfish Dashboard when you [sign up](https://www.pollfish.com/signup/publisher) and create a new app.

```js
var builder = new RNPollfish.Builder('ANDROID_API_KEY', 'IOS_API_KEY')
    .rewardMode(true); // Android & iOS
```

```js
var builder = new RNPollfish.Builder('ANDROID_API_KEY', null)
    .rewardMode(true); // Android only
```

```js
var builder = new RNPollfish.Builder(null, 'IOS_API_KEY')
    .rewardMode(true); // iOS only
```

### 4.1 Configure Pollfish behaviour (Optional)

You can set several params to control the behaviour of Pollfish survey panel within your app with the use of the `RNPollfish.Builder` instance. Below you can see all the available options. Apart from the constructor all the other methods are optional.

Param               | Description
--------------------|:---------
**`constructor(String, String)`**           | Sets Your Android and iOS API Keys (from step 2)
**`.indicatorPosition(RNPollfish.Position)`**| Sets the Position where you wish to place the Pollfish indicator. There are six different options RNPollfish.Position.{topLeft, topRight, middleLeft, middleRight, bottomLeft, bottom Right}: 
**`.indicatorPadding(Int)`**                 | Sets the padding from top or bottom depending on the position of the indicator specified before (if used in middle position, padding is calculated from the top).
**`.offerwallMode(Boolean)`**                | Sets Pollfish to offerwall mode
**`.releaseMode(Boolean)`**                  | Choose Debug or Release Mode
**`.rewardMode(Boolean)`**                   | Init in reward mode (skip Pollfish indicator to show a custom prompt)
**`.requestUUID(String)`**                   | Sets a unique id to identify a user and be passed through server-to-server callbacks
**`.userProperties(Json)`**                  | Send attributes that you receive from your app regarding a user, in order to receive a better fill rate and higher priced surveys. You can see a detailed list of the user attributes you can pass with their keys at the following [link](https://www.pollfish.com/docs/demographic-surveys)
**`.rewardInfo(Json)`**                      | An object holding information regarding the survey completion reward. If set, `signature` must be calculated in order to receive surveys. See [here](https://www.pollfish.com/docs/api-documentation) in section **`Notes for sig query parameter`**
**`.clickId`**                               | A pass throught param that will be passed back through server-to-server callback
**`.signature`**                             | An optional parameter used to secure the `rewardConversion` and `rewardName` parameters passed on `rewardInfo` `Json` object

<br/>

Example of Pollfish configuration using all the available options

```js
builder.indicatorPosition(RNPollfish.Position.topLeft)
    .indicatorPadding(10)
    .offerwallMode(false)
    .rewardMode(true)
    .releaseMode(false)
    .requestUUID('REQUEST_UUID')
    .userProperties({
        gender: '1',
        education: '1',
        ... 
    })
    .clickId('CLICK_ID')
    .signature('SINGNATURE')
    .rewardInfo({
        rewardName: 'Points',
        rewardConversion: 1.3
    });
```

<br/>

> ### Debug vs Release Mode
>
> You can use Pollfish either in Debug or in Release mode. 
>  
> * **Debug mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
> * **Release mode** is the mode to be used for a released app (start receiving paid surveys).
> 
> **Note:** Be careful to set the `releaseMode` parameter to `true` when you release your app in a relevant app store!!

<br/>

> ### Reward Mode 
> 
> Setting the `rewardMode` to `false` during initialization enables controlling the behavior of Pollfish in an app from the Pollfish panel. Enabling reward mode ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small button) and always force open Pollfish view to app users. This method is usually used when app developers want to somehow incentivize their users before completing surveys to increase completion rates.

<br/>

## 5. Initialize Pollfish

Last but not least. Build the `Params` object by invoking `.build()` on the `RNPollfish.Builder` instance that you've configured earlier and call `RNPollfish.init(params)` passing the `Params` object as an argument.

```js
var params = builder.build();
RNPollfish.init(params);

// OR

RNPollfish.init(builder.build());
```

<br/>

## 6. Update your Privacy Policy

### Add the following paragraph to your app's privacy policy

<br/>

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Publishers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user's device data (including Advertising ID, Device ID, other available electronic identifiers and further response meta-data is automatically sent, via our app, to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully the Pollfish respondent terms located at [https://www.pollfish.com/terms/respondent](https://www.pollfish.com/terms/respondent). These data will be associated with your answers to the questionnaires whenever Pollfish sends such questionnaires to eligible users. Pollfish may share such data with third parties, clients and business partners, for commercial purposes. By downloading the application, you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by visiting the following link [https://www.pollfish.com/respondent/opt-out](https://www.pollfish.com/respondent/opt-out). We once more invite you to check the Pollfish respondent's terms of use, if you wish to have more detailed view of the way Pollfish works and with whom Pollfish may further share your data."*  

---

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>

<br/>

If you have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://help.pollfish.com/en/collections/24867-faq-publishers">FAQ page</a>

<br/>

> **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process users need to go through in order to join the platform. Bear in mind that if a paid survey is available at that point of time, the demographic questions will be inserted at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this new type of targeting.

<br/>

<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>
<br/>


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

<br/>

## 7.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>

<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.

<br/>

# Optional Section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys. All these steps are optional.

<br/>

## 8. Implement Pollfish Event Listeners 

<br/>

### 8.1. Get notified when a Pollfish survey is received

You can get notified when a Pollfish survey is received. With this notification, you can also get informed about the type of survey that was received, money to be earned if survey gets completed, shown in USD cents and other info around the survey such as LOI and IR.

<br/>

> **Note:** If Pollfish is initialized in offerwall mode then the event parameter will be `undefined`, otherwise it will include info around the received survey.

<br/>

```js
RNPollfish.addEventListener(RNPollfish.PollfishSurveyReceivedListener, (event) => {
    if (event === undefined) {
        console.log("Pollfish Offerwall Received");
    } else {
        console.log(`Pollfish Survey Received - CPA: ${event.surveyCPA}, IR: ${event.surveyIR}, LOI: ${event.surveyLOI}, Class: ${event.surveyClass}, Reward Value: ${event.rewardValue}, Reward Name: ${event.rewardName}, Remaining Completes: ${event.remainingCompletes}`);
    }
});
```

<br/>

### 8.2. Get notified when a Pollfish survey is completed

You can get notified when a user completed a survey. With this notification, you can also get informed about the type of survey, money earned from that survey in USD cents and other info around the survey such as LOI and IR.

```js
RNPollfish.addEventListener(RNPollfish.PollfishSurveyCompletedListener, (event) => {
    console.log(`Pollfish Survey Completed - CPA: ${event.surveyCPA}, IR: ${event.surveyIR}, LOI: ${event.surveyLOI}, Class: ${event.surveyClass}, Reward Value: ${event.rewardValue}, Reward Name: ${event.rewardName}, Remaining Completes: ${event.remainingCompletes}`);
});
```

<br/>

### 8.3. Get notified when a user is not eligible for a Pollfish survey

You can get notified when a user is not eligible for a Pollfish survey. In market research monetization, users can get screened out while completing a survey beucase they are not relevant with the audience that the market researcher was looking for. In that case the user not eligible notification will fire and the publisher will make no money from that survey. The user not eligible notification will fire after the surveyReceived event, when the user starts completing the survey.

```js
RNPollfish.addEventListener(RNPollfish.PollfishUserNotEligibleListener, (_) => {
    console.log("Pollfish User Not Eligible");
});
```

<br/>

### 8.4. Get notified when a Pollfish survey is not available

You can get notified when a Pollfish survey is not available.

```js
RNPollfish.addEventListener(RNPollfish.PollfishSurveyNotAvailableListener, (_) => {
    console.log("Pollfish Survey Not Available");
});
```

<br/>

### 8.5. Get notified when a user has rejected a Pollfish survey

You can get notified when a user has rejected a Pollfish survey.

```js
RNPollfish.addEventListener(RNPollfish.PollfishUserRejectedSurveyListener, (_) => {
    console.log("Pollfish User Rejected Survey");
});
```

<br/>

### 8.6. Get notified when a Pollfish survey panel has opened

You can register and get notified when a Pollfish survey panel has opened. Publishers usually use this notification to pause a game until the pollfish panel is closed again.

```js
RNPollfish.addEventListener(RNPollfish.PollfishOpenedListener, (_) => {
    console.log("Pollfish Opened");
});
```

<br/>

### 8.7. Get notified when a Pollfish survey panel has closed

You can register and get notified when a Pollfish survey panel has closed. Publishers usually use this notification to resume a game that they have previously paused when the Pollfish panel was opened.

```js
RNPollfish.addEventListener(RNPollfish.PollfishClosedListener, (_) => {
    console.log("Pollfish Closed");
});
```

<br/>

## 9. Manually show/hide Pollfish panel

You can manually hide and show Pollfish by calling the functions below, after initialization.

```js
RNPollfish.show();
```

```js
RNPollfish.hide();
```

<br/>

## 10. Check if Pollfish surveys are available on your device

After you initialize Pollfish and a survey is received you can check at any time if the survey is available at the device by calling the following function.

```js
RNPollfish.isPollfishPresent((isPollfishPresent) => {
    console.log(isPollfishPresent ? 'Pollfish is available' : 'Pollfish is not available');
});
```

<br/>

## 11. Check if Pollfish panel is open

You can check at any time if the survey panel is open by calling the following function.

```js
RNPollfish.isPollfishPanelOpen((isPollfishPanelOpen) => {
    console.log(isPollfishPanelOpen ? 'Pollfish panel is open' : 'Pollfish panel is closed');
});
```

<br/>

# Example

If you would like to implement the Rewarded approach or just review an example in code, you can review the example app on [Github](https://github.com/pollfish/react-native-plugin-pollfish/tree/main/example).

<br/>

# More info

You can read more info on how the Native Pollfish SDKs work on Android and iOS or how to set up properly a React Native environment at the following links:

<br/>

[Pollfish Android SDK Integration Guide](https://pollfish.com/docs/android)

[Pollfish iOS SDK Integration Guide](https://pollfish.com/docs/ios)

[React Native Starting Guide](https://reactnative.dev/docs/getting-started)
