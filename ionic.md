Pollfish Ionic plugin, allows integration of Pollfish surveys into Ionic Android and iOS apps. 

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.

<br/>

# Prerequisites

* Android SDK 21 or higher using Google Play Services
* iOS version 9.0 or higher
* Ionic v6 or higher
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

Pollfish Ionic Plugin v2 introduces a new package name and different API with added customization options during initialization. If you have already integrated Pollfish Cordova Plugin < v2 in you app, please

**1\. Remove the old deprecated package name**

```bash
# Ionic/Cordova
ionic cordova plugin remove com.pollfish.cordova_plugin

# Ionic/Capacitor
npm r com.pollfish.cordova_plugin
```

**2\. Add the new package name**

```bash
# Ionic/Cordova
ionic cordova plugin add cordova-plugin-pollfish

# Ionic/Capacitor
npm r com.pollfish.cordova_plugin
```

**3\. Take some time reading the migration guide below**

<details><summary>➤ <b>Migration Guide</b> (Click to expand)</summary>
<table>

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Installation** <br/>

```bash
npm i com.pollfish.cordova_plugin # Ionic Capacitor
ionic cordova plugin add com.pollfish.cordova_plugin # Ionic Cordova
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```bash
npm i cordova-plugin-pollfish # Ionic Capacitor
ionic cordova plugin add cordova-plugin-pollfish # Ionic Cordova
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialization** <br/>

```js
pollfish.init(
    false, 
    false, 
    'API_KEY',
    5,
    10, 
    'REQUEST_UUID', 
    false);
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```js
var params = new pollfish.Builder('ANDROID_API_KEY', 'IOS_API_KEY');

params.rewardMode(false)
	.offerwallMode(false)
	.releaseMode(false)
	.indicatorPadding(50)
	.indicatorPosition(pollfish.Position.BOTTOM_RIGHT)
	...
	.build();

pollfish.init(params);
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialization with User Properties** <br/>

```js
pollfish.initWithUserAttributes(
    false, 
    false, 
    'API_KEY',
    5,
    10, 
    'REQUEST_UUID', 
    false,
    {
		gender: '1',
		education: '1'
	});
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Show/Hide** <br/>

```js
pollfish.showPollfish();

pollfish.hidePollfish(); 
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```js
pollfish.show();

pollfish.hide();
```

</table>
</details>

<br/>

# Analytical Steps

## 1. Obtain a Developer Account

Register as a Developer at [www.pollfish.com](http://www.pollfish.com)

<br/>

## 2. Add new apps in Pollfish panel and copy the given API Keys

Login at [www.pollfish.com](http://www.pollfish.com), add a new app for each targeting platform (Android & iOS) at Pollfish panel in section My Apps and copy the given API keys to use later in your init function in your app.

<br/>

## 3. Install the plugin

<span style="text-decoration: underline">Cordova</span>

```bash
# Install Core library (once per project)
npm install @ionic-native/core

# Install Pollfish Ionic Native TypeScript wrapper
npm install @ionic-native/pollfish

# Install Pollfish Cordova plugin
ionic cordova plugin add cordova-plugin-pollfish
```

<span style="text-decoration: underline">Capacitor</span>

```bash
# Install Core library (once per project)
npm install @ionic-native/core

# Install Pollfish Ionic Native TypeScript wrapper
npm install @ionic-native/pollfish

# Install Pollfish Cordova plugin
npm install cordova-plugin-pollfish

# Update native platform project(s) to include newly added plugin
npx ionic cap sync
```

<br/>

### 3.1 Uninstalling the plugin

<br/>

<span style="text-decoration: underline">Cordova</span>

```bash
# Uninstall Pollfish Ionic Native TypeScript wrapper
npm r @ionic-native/pollfish

# Uninstall Pollfish Cordova plugin
ionic cordova plugin remove cordova-plugin-pollfish
```

<span style="text-decoration: underline">Capacitor</span>

```bash
# Uninstall Pollfish Ionic Native TypeScript wrapper
npm r @ionic-native/pollfish

# Uninstall Pollfish Cordova plugin
npm r cordova-plugin-pollfish

# Update native platform project(s)
npx ionic cap sync
```

<br/>

## 4. Initialize Pollfish

### 4.1 Inject and import Pollfish

Inject Pollfish dependency. Navigate to `src/app/app.module.ts` 

```js
import { Pollfish } from '@ionic-native/pollfish/ngx';

@NgModule({
  ...
  providers: [
    ...
    Pollfish
  ],
})
export class AppModule {}
```

Import Pollfish in your page

```js
import { Pollfish } from '@ionic-native/pollfish/ngx';

export class HomePage {

  constructor(private pollfish: Pollfish, ...) {}
  ...
}
```

### 4.2 Initialize Pollfish

You can set several params to control the behaviour of Pollfish survey panel within your app with the use of the `pollfish.Builder` instance. Below you can see all the available options. Apart from the constructor all the other methods are optional.

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
**`.rewardInfo(Json)`**                      | An object holding information regarding the survey completion reward
**`.clickId`**                               | A pass throught param that will be passed back through server-to-server callback
**`.signature`**                             | An optional parameter used to secure the `rewardConversion` and `rewardName` parameters passed on `rewardInfo` `Json` object

<br/>

```js
var params = new pollfish.Builder('ANDROID_API_KEY', 'IOS_API_KEY'); // Android & iOS
```

```js
var params = new pollfish.Builder('ANDROID_API_KEY', null); // Android only
```

```js
var params = new pollfish.Builder(null, 'IOS_API_KEY'); // iOS only
```

```js
params.rewardMode(false)
	.offerwallMode(false)
	.releaseMode(false)
	.indicatorPadding(50)
	.indicatorPosition(pollfish.Position.BOTTOM_RIGHT)
	.requestUUID('REQUEST_UUID')
	.userProperties({
		gender: '1',
		education: '1'
	})
	.clickId('CLICK_ID')
	.rewardInfo({
		rewardName: 'Points',
		rewardConversion: 1.3
	})
	.signature('SIGNATURE')
	.build();

pollfish.init(params);
```

#### Debug Vs Release Mode

You can use Pollfish either in Debug or in Release mode. 
  
* **Debug mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
* **Release mode** is the mode to be used for a released app (start receiving paid surveys).

> **Note:** In Android debugMode parameter is ignored. Your app turns into debug mode once it is signed with a debug key. If you sign your app with a release key it automatically turns into Release mode.

> **Note:** Be careful to turn the releaseMode parameter to true when you release your app in a relevant app store!!

<br/>

#### Reward Mode 

Reward mode false during initialization enables controlling the behavior of Pollfish in an app from Pollfish panel. Enabling reward mode ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small button) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates.

<br/>

## 5. Update your Privacy Policy

### Add the following paragraph to your app's privacy policy

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

## 6.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>

<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.

<br/>

# Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys. All these steps are optional.

<br/>

## 7. Implement Pollfish event listeners

<br/>

### 7.1 Get notified when a Pollfish survey is received

You can get notified when a Pollfish survey is received. With this notification, you can also get informed about the type of survey that was received, money to be earned if survey gets completed, shown in USD cents and other info around the survey such as LOI and IR.

<br/>

> **Note:** If Pollfish is initialized in offerwall mode then the event parameter will be `undefined`, otherwise it will include info around the received survey.

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishSurveyReceived, (result) => {
    console.log("Survey Received: " + JSON.stringify(result));
});
```

<br/>

### 7.2 Get notified when a Pollfish survey is completed

You can get notified when a user completed a survey. With this notification, you can also get informed about the type of survey, money earned from that survey in USD cents and other info around the survey such as LOI and IR.


```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishSurveyCompleted, (result) => {
    console.log("Survey Completed: " + JSON.stringify(result));
});
```

<br/>

### 7.3 Get notified when a user is not eligible for a Pollfish survey

You can get notified when a user is not eligible for a Pollfish survey. In market research monetization, users can get screened out while completing a survey beucase they are not relevant with the audience that the market researcher was looking for. In that case the user not eligible notification will fire and the publisher will make no money from that survey. The user not eligible notification will fire after the surveyReceived event, when the user starts completing the survey.

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishUserNotEligible, (_) => {
    console.log("Pollfish User Not Eligible");
});
```

<br/>

### 7.4 Get notified when a Pollfish survey is not available

You can get notified when a Pollfish survey is not available

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishSurveyNotAvailable, (_) => {
    console.log("Pollfish Survey not available");
});
```

<br/>

### 7.5 Get notified when a Pollfish survey panel is open

You can get notified when Pollfish survey panel is open

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishOpened, (_) => {
    console.log("Pollfish Survey panel is open");
});
```

<br/>

### 7.6 Get notified when a Pollfish survey panel is closed

You can get notified when Pollfish survey panel is closed

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishClosed, (_) => {
    console.log("Pollfish Survey panel is closed");
});
```

<br/>

### 7.7 Get notified when a user rejected a survey

You can get notified when use has rejected a Pollfish survey

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishUserRejectedSurvey, (_) => {
    console.log("Pollfish User Rejected Survey");
});
```

<br/>

## 8. Manually show/hide Pollfish panel

You can manually hide and show Pollfish by calling anywhere after initialization: 

For example:

```js
pollfish.show();
```

or

```js
pollfish.hide();
```

<br/>

## 9. Check if Pollfish surveys are available on your device

After you initialize Pollfish and a survey is received you can check at any time if the survey is available at the device by calling the following function.

```js
pollfish.isPollfishPresent((result) => {
	console.log(result)
});
```

<br/>

# More info

You can read more info on how the Native Pollfish SDKs work on Android and iOS or how to set up properly Ionic environment at the following links:

<br/>

[Pollfish Android SDK Integration Guide](https://pollfish.com/docs/android)

[Pollfish iOS SDK Integration Guide](https://pollfish.com/docs/ios)

[Ionic Starting Guide](https://ionicframework.com/docs)