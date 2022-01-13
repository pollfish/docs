Pollfish Flutter plugin, allows integration of Pollfish surveys into Flutter Android and iOS apps. 

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.


Pollfish Flutter Plugin can be found on Dart Packages [website](https://pub.dartlang.org/packages/flutter_pollfish). The source code and an example app can be found on [Github](https://github.com/pollfish/flutter-plugin-pollfish).

<br/>

# Prerequisites

*	Android SDK 21 or higher using Google Play Services
*	iOS version 9.0 or higher
* Flutter version 1.20.0 or higher
* Dart SDK version 2.12.0 or higher
* CocoaPods version 1.10.0 or higher

<br/>

> **Note:** Apps designed for [Children and Families program](https://play.google.com/about/families/ads-monetization/) should not be using Pollfish SDK, since Pollfish does not collect responses from users less than 16 years old    

> **Note:** Pollfish iOS SDK utilizes Apple's Advertising ID (IDFA) to identify and retarget users with Pollfish surveys. As of iOS 14 you should initialize Pollfish Flutter plugin in iOS only if the relevant IDFA permission was granted by the user

<br/>

# Quick Guide

* Sign Up for a Pollfish Developer account,
* Create new apps for each targeting platform (Android & iOS) and grap the API keys
* Install Pollfish plugin and call init function
* Set to Release mode and publish on app store
* Update your app's privacy policy
* Request your account to get verified from Pollfish Dashboard

<br/>

# Migrate to v4

Pollfish Flutter Plugin v4 introduces a different API with added customization options during initialization. If you have already integrated Pollfish Flutter Plugin < v4 in you app, please take some time reading the migration guide below.

<details><summary>➤ <b>Migration Guide</b> (Click to expand)</summary>
<table>
<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialization** <br/>

```dart
FlutterPollfish.instance.init(
    apiKey: 'YOUR_API_KEY',
    pollfishPosition: 5,
    indicatorPadding: 40,
    rewardMode: false,
    releaseMode: true,
    requestUUID: 'REQUEST_UUID',
    offerwallMode: false,
    userProperties: <String, dynamic>{ 
      'gender': '1',
      'education': '1',
      ...
    });
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```dart
FlutterPollfish.instance.init(
    androidApiKey: 'ANDROID_API_KEY', // Required
    iOSApiKey: 'IOS_API_KEY',         // Required
    pollfishPosition: Position.bottomRight,
    indicatorPadding: 40,
    rewardMode: false,
    releaseMode: true,
    requestUUID: 'REQUEST_UUID',
    offerwallMode: false,
    userProperties: <String, dynamic>{ 
      'gender': '1',
      'education': '1',
      ...
    });
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

Add this to your package's pubspec.yaml file:

```yaml
dependencies:
  ...
  flutter_pollfish: ^4.0.1
```

Execute the following command

```bash
flutter packages get
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

## 4. Initialize Pollfish

Import Pollfish

```dart
import 'package:flutter_pollfish/flutter_pollfish.dart';
```

Initialize Pollfish using the Api keys from step 2. If your are targing only one platform (eg iOS) you can set the other's platform api key (Android) to `null`.

For example:

```dart
FlutterPollfish.instance.init(androidApiKey: 'ANDROID_API_KEY', iOSApiKey: 'IOS_API_KEY'); // Android and iOS
```

```dart
FlutterPollfish.instance.init(androidApiKey: 'ANDROID_API_KEY', iOSApiKey: null); // Android only
```

```dart
FlutterPollfish.instance.init(androidApiKey: null, iOSApiKey: 'IOS_API_KEY'); // iOS only
```

<br/>

### 4.1 Other Init params (optional)

During initialization you can pass different optional params:

1. **`indicatorPosition`**: Position - `Position.topLeft`, `.topRight`, `.middleLeft`, `.middleRight`, `.bottomLeft`, `.bottomRight` (defines the side of the Pollfish panel, and position of Pollfish indicator)
2. **`indicatorPadding`**: int - Sets padding from the top or bottom according to Position of the indicator
3. **`releaseMode`**: bool - Sets Pollfish SDK to Debug or Release mode. Use Developer mode to test your implementation with demo surveys
4. **`rewardMode`**: bool - Initializes Pollfish in reward mode (used when implementing a Rewarded approach)
5. **`requestUUID`**: String - Sets a unique id to identify a user. This param will be passed back through server-to-server callbacks
5. **`offerwallMode`**: bool - Sets Pollfish to Offerwall mode
6. **`userProperties`**: Map<String, Object> - Send attributes that you receive from your app regarding a user, in order to receive a better fill rate and higher priced surveys. You can see a detailed list of the user attributes you can pass with their keys at the following [link](https://www.pollfish.com/docs/demographic-surveys)
7. **`clickId`**: String - A pass throught param that will be passed back through server-to-server callback
8. **`signature`**: String - An optional parameter used to secure the `rewardConversion` and `rewardName` parameters passed on `RewardInfo` object
9. **`rewardInfo`**: RewardInfo - An object holding information regarding the survey completion reward

<br/>

#### Debug Vs Release Mode

You can use Pollfish either in Debug or in Release mode. 
  
* **Debug mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
* **Release mode** is the mode to be used for a released app (start receiving paid surveys).

> **Note:** In Android debugMode parameter is ignored. Your app turns into debug mode once it is signed with a debug key. If you sign your app with a release key it automatically turns into Release mode.

> **Note:** Be careful to turn the `releaseMode` parameter to `true` when you release your app in a relevant app store!!

<br/>

### Reward Mode 

Reward mode false during initialization enables controlling the behavior of Pollfish in an app from Pollfish panel. Enabling reward mode ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small button) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates.

<br/>

```dart
FlutterPollfish.instance.init(
  androidApiKey: 'ANDROID_API_KEY',
  iOSApiKey: 'IOS_API_KEY',
  pollfishPosition: 5,
  indicatorPadding: 40,
  rewardMode: false,
  releaseMode: true,
  requestUUID: 'REQUEST_UUID',
  offerwallMode: false,
  userProperties: <String, dynamic>{ 
    'gender': '1',
    'education': '1',
    ...
  }),
  signature: 'SIGNATURE',
  clickId: 'CLICK_ID',
  rewardInfo: RewardInfo('Point', 1.3));
```

<br/>

## 5. Update your Privacy Policy

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

## 6. Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>

<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.

<br/>

# Optional Section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how to be eligible to more targeted (high-paid) surveys. All these steps are optional.

<br/>

## 7. Implement Pollfish Event Listeners

<br/>

### 7.1. Get notified when a Pollfish survey is received

You can get notified when a Pollfish survey is received. With this notification, you can also get informed about the type of survey that was received, money to be earned if survey gets completed, shown in USD cents and other info around the survey such as LOI and IR.

<br/>

> **Note:** If Pollfish is initialized in offerwall mode then the event parameter will be `null`, otherwise it will include info around the received survey.

```dart
FlutterPollfish.instance.setPollfishSurveyReceivedListener(onPollfishSurveyReceived);

void onPollfishSurveyReceived(SurveyInfo? surveyInfo) => setState(() {
  if (surveyInfo == null) {
    print("Offerwall Ready");
  } else {
    print("Survey Received - ${surveyInfo.toString()}");
  }
});
```

<br/>

### 7.2. Get notified when a Pollfish survey is completed

You can get notified when a user completed a survey. With this notification, you can also get informed about the type of survey, money earned from that survey in USD cents and other info around the survey such as LOI and IR.

```dart
FlutterPollfish.instance.setPollfishSurveyCompletedListener(onPollfishSurveyCompleted);

void onPollfishSurveyCompleted(SurveyInfo sureyInfo) => setState(() {
    print('Survey Completed: - ${surveyInfo.toString()}');
});
```

<br/>

### 7.3. Get notified when a user is not eligible for a Pollfish survey

You can get notified when a user is not eligible for a Pollfish survey. In market research monetization, users can get screened out while completing a survey beucase they are not relevant with the audience that the market researcher was looking for. In that case the user not eligible notification will fire and the publisher will make no money from that survey. The user not eligible notification will fire after the surveyReceived event, when the user starts completing the survey.

```dart
FlutterPollfish.instance.setPollfishUserNotEligibleListener(onPollfishUserNotEligible);

void onPollfishUserNotEligible() => setState(() {
   print('User Not Eligible');
}
```

<br/>

### 7.4. Get notified when a Pollfish survey is not available

You can be notified when a Pollfish survey is not available.

```dart
FlutterPollfish.instance.setPollfishSurveyNotAvailableListener(onPollfishSurveyNotAvailable);

void onPollfishSurveyNotAvailable() => setState(() {
   print('Survey Not Available');
}
```

<br/>

### 7.5. Get notified when a user has rejected a Pollfish survey

You can be notified when a user has rejected a Pollfish survey.

```dart
FlutterPollfish.instance.setPollfishUserRejectedSurveyListener(onPollfishUserRejectedSurvey);

void onPollfishUserRejectedSurvey() => setState(() {
   print('User Rejected Survey');
}
```

<br/>

### 7.6. Get notified when a Pollfish survey panel has opened

You can register and get notified when a Pollfish survey panel has opened. Publishers usually use this notification to pause a game until the pollfish panel is closed again.

```dart
FlutterPollfish.instance.setPollfishOpenedListener(onPollfishOpened);

void onPollfishOpened() => setState(() {
   print('Survey Panel Open');
}
```

<br/>

### 7.7. Get notified when a Pollfish survey panel has closed

You can register and get notified when a Pollfish survey panel has closed. Publishers usually use this notification to resume a game that they have previously paused when the Pollfish panel was opened.

```dart
FlutterPollfish.instance.setPollfishClosedListener(onPollfishClosed);

void onPollfishClosed() => setState(() {
   print('Survey Panel Closed');
}
```

<br/>

### 7.8 Unsubscribe from Pollfish Listeners

Please ensure you unsubscribe from Pollfish notification listeners at the end of the state's lifecycle

```dart
@override
void dispose() {
    FlutterPollfish.instance.removeListeners();
    super.dispose();
}
```

<br/>

## 8. Manually show/hide Pollfish panel

During the lifetime of a survey, you can manually hide and show Pollfish by calling the following functions.

```dart
FlutterPollfish.instance.show();
```

or

```dart
FlutterPollfish.instance.hide();
```

<br/>

## 9. Check if Pollfish surveys are available on your device

After a Pollish survey is received you can check at any time if the survey is available at the device by calling the following function.

```dart
FlutterPollfish.instance.isPollfishPresent().then((isPresent) => {
  print("isPresent: $isPresent");
});
```

<br/>

## 10. Check if Pollfish panel is open

You can check at any time if the survey panel is open by calling the following function.

```dart
FlutterPollfish.instance.isPollfishPanelOpen().then((isOpen) => {
  print("isOpen: $isOpen");
});
```

<br/>

# Example

If you would like to implement the Rewarded approach or just review an example in code, you can review the example app on [Github](https://github.com/pollfish/flutter-plugin-pollfish/tree/master/example).

<br/>

# More info

You can read more info on how the Native Pollfish SDKs work on Android and iOS or how to set up properly a Flutter environment at the following links:

<br/>

[Pollfish Android SDK Integration Guide](https://pollfish.com/docs/android)

[Pollfish iOS SDK Integration Guide](https://pollfish.com/docs/ios)

[Flutter Starting Guide](https://flutter.dev/docs/get-started)
