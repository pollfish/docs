Pollfish Cordova plugin, allows integration of Pollfish surveys into Cordova Android and iOS apps. 

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.

Pollfish Cordova Plugin can be found on [npm Registry](https://www.npmjs.com/package/cordova-plugin-pollfish). The source code and an example app can be found on [Github](https://github.com/pollfish/cordova-plugin-pollfish).

<br/>

# Prerequisites

* Android SDK 21 or higher using Google Play Services
* iOS 11.0 or higher
* Apache Cordova v3.0.0 or higher
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

Pollfish Cordova Plugin v2 introduces a new package name and different API with added customization options during initialization. If you have already integrated Pollfish Cordova Plugin < v2 in you app, please

**1\. Remove the old deprecated package name**

```bash
cordova plugin remove com.pollfish.cordova_plugin
```

**2\. Add the new package name**

```bash
cordova plugin add cordova-plugin-pollfish
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
cordova plugin add com.pollfish.cordova_plugin
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```bash
cordova plugin add cordova-plugin-pollfish
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Plugin reference** <br/>

```js
pollfishplugin.<method>
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```js
pollfish.<method>
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialization** <br/>

```js
pollfishplugin.init(
    releaseMode,
    rewardMode,
    apiKey,
    position,
    padding,
    requestUUID, 
    offerwallMode); 
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```js
var params = new pollfish.Builder('ANDROID_API_KEY', 'IOS_API_KEY')
	.rewardMode(false)
	.offerwallMode(false)
	.releaseMode(false)
	...
	.build();
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Show/Hide** <br/>

```js
pollfishplugin.showPollfish();

pollfishplugin.hidePollfish(); 
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

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialization with User Properties** <br/>

```js
pollfishplugin.initWithUserAttributes(
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

</table>
</details>

<br/>

# Analytical Steps

## 1. Obtain a Developer Account

Register as a Developer at [www.pollfish.com](https://www.pollfish.com)

<br/>

## 2. Add new apps in Pollfish panel and copy the given API Keys

Login at [www.pollfish.com](http://www.pollfish.com), add a new app for each targeting platform (Android & iOS) at Pollfish panel in section My Apps and copy the given API keys to use later in your init function in your app.

<br/>

## 3. Install the plugin

To add Pollfish plugin just type:

```bash
cordova plugin add cordova-plugin-pollfish
```

To remove Pollfish plugin type:

```bash
cordova plugin remove cordova-plugin-pollfish
```

*In iOS if pollfish framework is not added automatically you may need to add it manually to your XCode project. In Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location (located in /src/ios/framework) and select it. The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane). The framework is a folder and you should add the whole folder into your project.*

<br/>

**Android 12**

Apps updating their target API level to 31 (Android 12) or higher will need to declare a Google Play services normal permission in the AndroidManifest.xml file.

Navigate to the `platforms/android/app/src/main` directory inside your project's root, locate the AndroidManifest.xml file and add the following line just before the `<application>`.

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

You can read more about Google Advertising ID changes [here](https://support.google.com/googleplay/android-developer/answer/6048248).

<br/>

**iOS 14+**

Request IDFA Permission (Recommended but optional)

Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower. Offerwall integrations perform better compared to single survey integrations when no IDFA permission is given. Our recommendation is that you should ask for IDFA usage permission prior to Pollfish initialization.

<br/>

## 4. Create `pollfish.Builder` instance

The Pollfish plugin must be initialized with one or two api keys depending on which platforms are you targeting. You can retrieve an API key from Pollfish Dashboard when you [sign up](https://www.pollfish.com/signup/publisher) and create a new app.


```js
var builder = new pollfish.Builder('ANDROID_API_KEY', 'IOS_API_KEY')
	.rewardMode(true); // Android & iOS
```

```js
var builder = new pollfish.Builder('ANDROID_API_KEY', null)
	.rewardMode(true); // Android only
```

```js
var builder = new pollfish.Builder(null, 'IOS_API_KEY')
	.rewardMode(true); // iOS only
```

<br/>

### 4.1. Configure Pollfish behaviour (Optional)

You can set several params to control the behaviour of Pollfish survey panel within your app with the use of the `pollfish.Builder` instance. Below you can see all the available options.

<br/>

> **Note:** All the params are optional, except the **`releaseMode`** setting that turns your integration in release mode prior publishing to the Google Play or App Store.

<br/>

No      | Description
--------|---------
4.1.1	| **`.indicatorPosition(pollfish.Position)`** 	<br/> Sets the Position where you wish to place the Pollfish indicator.
4.1.2	| **`.indicatorPadding(Int)`**                	<br/> Sets the padding from top or bottom depending on the position of the indicator.
4.1.3	| **`.offerwallMode(Boolean)`** 				<br/> Sets Pollfish SDK to offerwall mode
4.1.4	| **`.releaseMode(Boolean)`**      	            <br/> Sets Pollfish SDK to Debug or Release Mode
4.1.5	| **`.rewardMode(Boolean)`**           		    <br/> Initializes Pollfish in reward mode (skip Pollfish indicator to show a custom prompt)
4.1.6 	| **`.requestUUID(String)`**               		<br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
4.1.7 	| **`.userProperties(Json)`**                  	<br/> Send attributes that you receive from your app regarding a user, in order to receive a better fill rate and higher priced surveys.
4.1.8   | **`.rewardInfo(Json)`**                     	<br/> An object holding information regarding the survey completion reward.
4.1.9 	| **`.clickId(String)`**         		                <br/> A pass throught param that will be passed back through server-to-server callback
4.1.10  | **`.userId(String)`**									<br/> A unique id used to identify a user
4.1.11  | **`.signature(String)`**            	                <br/> An optional parameter used to secure the `rewardConversion` and `rewardName` parameters passed on `rewardInfo` `Json` object. 

<br/>

### 4.1.1. **`indicatorPosition(pollfish.Position)`**

Sets the Position where you wish to place Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png) 

<br/>

Also this setting sets from which side of the screen you would like Pollfish survey panel to slide in.

<br/> 

Pollfish indicator is shown only if Pollfish is used in a non rewarded mode.

<br/>

<span style="text-decoration: underline">There are six different options available: </span> 

* `Position.TOP_LEFT`
* `Position.BOTTOM_LEFT`
* `Position.MIDDLE_LEFT`
* `Position.TOP_RIGHT`
* `Position.MIDDLE_RIGHT`
* `Position.BOTTOM_RIGHT` 

If you do not set explicity a position for Pollfish indicator, it will appear by default at `Position.TOP_LEFT`

<br/>

> **Note:** If you would like to skip the Pollfish Indicator please set the `rewardMode` to `true`

<br/>

Below you can see an example on how you can set Pollfish indicator to slide from top right corner of the screen:

<br/>

```js
builder.indicatorPosition(pollfish.Position.TOP_RIGHT);
```

<br/>

### 4.1.2. **`.indicatorPadding(int)`**

The padding from the top or bottom of the screen according to position of the indicator (small icon) specified above (`.TOP_LEFT` is the default value)

```js
builder.indicatorPadding(8);
```

> **Note:** if used in MIDDLE position, padding is calculating from the top

<br/>

### 4.1.3. **`.offerwallMode(boolean)`**

Enables Pollfish in offerwall mode. If not specified Pollfish shows one survey at a time.

<br/>

Below you can see an example on how you can intialize Pollfish in Offerwall mode:

```js
builder.offerwallMode(true);
```

<br/>

### 4.1.4. **`.releaseMode(boolean)`** 

Sets Pollfish SDK to Developer or Release mode. If you do not set this param it will turn the SDK to Developer mode by default in order for the publisher to be able to test the survey flow.

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).  
*   **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

> **Note:** Be careful to set release mode parameter to true prior releasing to Google Play or AppStore!  

```js
builder.releaseMode(true);
```

<br/>

### 4.1.5. **`.rewardMode(boolean)`**

Initializes Pollfish in reward mode. This means that Pollfish Indicator (section 4.1.1) will not be shown and Pollfish survey panel will be automatically hidden until the publisher explicitly calls Pollfish `show` function (The publisher should wait for the Pollfish Survey Received Callback). This behaviour enables the option for the publishers, to show a custom prompt to incentivize the users to participate in a survey.

> **Note:** If not set, the default value is false and Pollfish indicator is shown.

This mode should be used if you want to incentivize users to participate to surveys. We have a detailed guide on how to implement the rewarded approach [here](https://www.pollfish.com/docs/rewarded-surveys)

> **Note:** Reward mode should be used along with the Survey Received callback so the publisher knows when to prompt the user and call `pollfish.show()`

```js
builder.rewardMode(true);
```

<br/>

### 4.1.6. **`.requestUUID(String)`**

Sets a unique id to identify a user or a request and be passed back to the publisher through server-to-server callbacks. You can read more on how to retrieve this param through the callbacks [here](https://www.pollfish.com/docs/s2s)

<br/>

Below you can see an example on how you can pass a requestUUID during initialization:

```js
builder.requestUUID(true);
```

<br/>

### 4.1.7. **`.UserProperties(Json)`**

Passing user attributes to skip or shorten Pollfish Demographic surveys.

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and archieve better fill rate and higher priced surveys.

> **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default.

> **Note:** You can read more on demographic surveys along with a list with all the available options [here](https://www.pollfish.com/docs/demographic-surveys)

An example of how you can pass user demographics can be found below:

```js
const userProperties = {
	"gender": "1",
	"year_of_birth": "1974",
	"marital_status": "2",
	"parental": "3",
	"education": "1",
	"employment": "1",
	"career": "2",
	"race": "3",
	"income": "1",
};

builder.userProperties(userProperties);
```

<br/>

### 4.1.8. **`.rewardInfo(Json)`**

A Json object passing information during initialization regarding the reward settings, overriding the values as speciefied on the Publisher's Dashboard

We strogly advise that you should use the Publisher Dashboard to provide Reward Info if your use case does not require a dynamic value.

<br/>

Field                  | Description
-----------------------|------------
**`rewardName`**       | Overrides the reward name as specified in the Publisher's Dashboard
**`rewardConversion`** | Overrides the reward conversion as specified on the Publisher's Dashboard. Conversion is expecting a number matching this function ( ```1 USD = X Points``` ) where ```X``` is a ```Double``` number.

<br/>

```js
const rewardInfo = {
	rewardName: 'Dollars',
	rewardConversion: 1.2
};

builder.rewardInfo(rewardInfo);
```

<br/>

> **Warning:** If a `rewardInfo` is set, please make sure to calculate and set the correct signature (4.1.11). By skipping this step you will be unable to receive surveys.

<br/>

### 4.1.9. **`.clickId(String)`**

A pass through parameter that will be returned back to the publisher through server-to-server callbacks as specified [here](https://www.pollfish.com/docs/s2s)

<br/>

```js
builder.clickId("CLICK_ID");
```

<br/>

### 4.1.10. **`.userId(String)`**

A unique id used to identify the user

Setting the `userId` will override the default behaviour and use that instead of the Advertising Id, of the corresponding platform, in order to identify a user

<span style="color: red">You can pass the id of a user as identified on your system. Pollfish will use this id to identify the user across sessions instead of an ad id/idfa as advised by the stores. You are solely responsible for aligning with store regulations by providing this id and getting relevant consent by the user when necessary. Pollfish takes no responsibility for the usage of this id. In any request from your users on resetting/deleting this id and/or profile created, you should be solely liable for those requests.</span>

<br/>

```js
builder.userId("USER_ID");
```

<br/>

### 4.1.11. **`.signature(String)`**

An optional parameter used to secure the `rewardName` and `rewardConversion` parameters as provided in the `RewardInfo` object (4.1.10). If `rewardConversion` and `rewardName` are defined, `signature` is required to be calculated and set as well.

This parameter can be used to prevent tampering around reward conversion, if passed during initialisation. The platform supports url validation by requiring a hash of the `rewardConversion`, `rewardName`, and `clickId`. Failure to pass validation will result in no surveys return and firing **`PollfishSurveyNotAvailable`** callback.

In order to generate the `signature` field you should sign the combination of `${rewardConversion}${rewardName}${clickId}` parameters using the HMAC-SHA1 algorithm and your account's secret_key that can be retrieved from the Account Information section on your Pollfish Dashboard.

> **Note:** Although `rewardConversion` and `rewardName` are mandatory for the hashing to work, `clickId` parameter is optional and you should add them for extra security.

<br/>

> **Note:** Please keep in mind if your `rewardConversion` is a whole number, you have to calculate the signature useing the floating point value with 1 decimal point.

<br/>

```js
builder.signature("SIGNATURE");
```

<br/>

Sample JavaScript code to generate valid signatures.

Add crypto-js library to your `index.html` file right above the `cordova.js` script tag. You can obtain the latest version from [cdnjs.com](https://cdnjs.com/libraries/crypto-js).

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js" integrity="sha512-E8QSvWZ0eCLGk4km3hxSsNmGWbLtSCSUcewDQPQWZF6pEU8GlT8a5fF32wOl1i8ftdMhssTrF/OhyGWwonTcXA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>

<script type="text/javascript" src="cordova.js"></script>
<script type="text/javascript" src="js/index.js"></script>
```

<br/>

```js
const secret = '<ACCOUNT_SECRET_KEY>';
const rewardConversion = '<REWARD_CONVERSION>';
const rewardName = '<REWARD_NAME>';
const clickId = '<CLICK_ID>';

const message = `${rewardConversion}${rewardName}${clickId}`;
let hash = CryptoJS.HmacSHA1(message, secret);
let signature = CryptoJS.enc.Base64.stringify(hash);
```

<br/>

Example of Pollfish configuration using the available options


```js
var builder = builder
	.offerwallMode(false)
	.releaseMode(false)
	.indicatorPadding(50)
	.indicatorPosition(pollfish.Position.BOTTOM_RIGHT)
	.requestUUID('REQUEST_UUID')
	.userProperties({
		gender: '1',
		education: '1',
		...
	})
	.clickId('CLICK_ID')
	.signature('SIGNATURE')
	.rewardInfo({
		rewardName: 'Points',
		rewardConversion: 1.3
	})
	.build();

pollfish.init(params); 
```

<br/>

## 5. Initialize Pollfish

Last but not least. Build the `Params` object by invoking `.build()` on the `pollfish.Builder` instance that you've configured earlier and call `pollfish.init(params)` passing the `Params` object as an argument.

```js
var params = builder.build();
pollfish.init(params);

// OR

pollfish.init(builder.build());
```

<br/>


## 6. Update your Privacy Policy

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

## 7.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>

<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.

<br/>

# Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how to be eligible to more targeted (high-paid) surveys. All these steps are optional.

<br/>

## 8. Implement Pollfish event listeners

<br/>

### 8.1 Get notified when a Pollfish survey is received

You can get notified when a Pollfish survey is received. With this notification, you can also get informed about the type of survey that was received, money to be earned if survey gets completed, shown in USD cents and other info around the survey such as LOI and IR.

<br/>

> **Note:** If Pollfish is initialized in offerwall mode then the event parameter will be `undefined`, otherwise it will include info around the received survey.

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishSurveyReceived, (result) => {
    console.log("Survey Received: " + JSON.stringify(result));
});
```

<br/>

### 8.2 Get notified when a Pollfish survey is completed

You can get notified when a user completed a survey. With this notification, you can also get informed about the type of survey, money earned from that survey in USD cents and other info around the survey such as LOI and IR.

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishSurveyCompleted, (result) => {
    console.log("Survey Completed: " + JSON.stringify(result));
});
```

<br/>

### 8.3 Get notified when a user is not eligible for a Pollfish survey

You can get notified when a user is not eligible for a Pollfish survey. In market research monetization, users can get screened out while completing a survey beucase they are not relevant with the audience that the market researcher was looking for. In that case the user not eligible notification will fire and the publisher will make no money from that survey. The user not eligible notification will fire after the surveyReceived event, when the user starts completing the survey.

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishUserNotEligible, (_) => {
    console.log("Pollfish User Not Eligible");
});
```

<br/>

### 8.4 Get notified when a Pollfish survey is not available

You can get notified when a Pollfish survey is not available

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishSurveyNotAvailable, (_) => {
    console.log("Pollfish Survey not available");
});
```

<br/>

### 8.5 Get notified when a Pollfish survey panel has opened

You can register and get notified when a Pollfish survey panel has opened. Publishers usually use this notification to pause a game until the pollfish panel is closed again.


```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishOpened, (_) => {
    console.log("Pollfish Survey panel is open");
});
```

<br/>

### 8.6 Get notified when a Pollfish survey panel has closed

You can register and get notified when a Pollfish survey panel has closed. Publishers usually use this notification to resume a game that they have previously paused when the Pollfish panel was opened.

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishClosed, (_) => {
    console.log("Pollfish Survey panel is closed");
});
```

<br/>

### 8.7 Get notified when a use has rejected a survey

You can be notified when use has rejected a Pollfish survey

```js
pollfish.setEventCallback(pollfish.EventListener.OnPollfishUserRejectedSurvey, (_) => {
    console.log("Pollfish User Rejected Survey");
});
```

<br/>

## 9. Manually show/hide Pollfish panel 

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

## 10. Check if Pollfish surveys are available on your device

After you initialize Pollfish and a survey is received you can check at any time if the survey is available at the device by calling the following function.

```js
pollfish.isPollfishPresent((result) => {
	console.log(result)
});
```

<br/>

## 11. Check if Pollfish panel is open

You can check at any time if the survey panel is open by calling the following function.

```js
pollfish.isPollfishPanelOpen((result) => {
	console.log(result)
});
```

<br/>

# Example

If you want to have a look at sample code on how you can call and use Pollfish plugin in your app, you can a review files located [here](https://github.com/pollfish/cordova-plugin-pollfish/tree/master/test)

<br/>

# More info

You can read more info on how the Native Pollfish SDKs work on Android and iOS or how to set up properly a Cordova environment at the following links:

<br/>

[Pollfish Android SDK Integration Guide](https://pollfish.com/docs/android)

[Pollfish iOS SDK Integration Guide](https://pollfish.com/docs/ios)

[Cordova Starting Guide](http://cordova.apache.org/docs/en/latest/guide/cli/index.html)

