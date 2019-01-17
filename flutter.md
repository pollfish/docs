
Pollfish Flutter plugin, allows integration of Pollfish surveys into Flutter Android and iOS apps. 

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.


Pollfish Flutter Plugin along with an example can be found on Dart Packages website [here](https://pub.dartlang.org/packages/flutter_pollfish)

## Prerequisites

*	Android 17+ using Google Play Services
*	iOS version 9.0+

## Quick Guide

* Sign Up for a Pollfish Publisher account, create a new app and grap it's API key
* Install and integrate Pollfish plugin and call the init function
* Set to Release mode and publish on app store
* Update your app's privacy policy
* Request your account to get verified from Pollfish Dashboard


![alt tag](https://www.pollfish.com/homeassets/images/rocketMobile.png)

## Steps Analytically

### 1. Obtain a Developer Account

Register as a Developer at [www.pollfish.com](http://www.pollfish.com)

### 2. Add new app in Pollfish panel and copy the given API Key

Login at [www.pollfish.com](http://www.pollfish.com) and add a new app on Pollfish Dashboard. Copy the given API key for this app in order use it later on, in your init function in your app.

### 3. Installing and importing the plugin

Add this to your package's pubspec.yaml file:

```
dependencies:
  flutter_pollfish: ^0.1.2
```
You can install then the package from the command line:

```
flutter packages get
```
You can import then in your Dart code the plugin, as below:

```
import 'package:flutter_pollfish/flutter_pollfish.dart';
```


### 4. Initialize Pollfish

When you initialize Pollfish you should pass the API Key (from step 2) of the app which is a mandatory param:

For example:

```
FlutterPollfish.instance.init(apiKey: 'YOUR_API_KEY')
```
#### 4.1 Other Init functions (optional)

During initialization you can pass different optional params:

1. **pollfishPosition**: int - TOP_LEFT=0 , BOTTOM_LEFT=1, TOP_RIGHT=2, BOTTOM_RIGHT=3, MIDDLE_LEFT=4, MIDDLE_RIGHT=5 (defines the side of the Pollish panel, and position of Pollish indicator)
2. **indPadding**: int - Sets padding (in dp) from the top or bottom according to Position of the indicator
3. **debugMode**: bool - Sets Pollfish SDK to Debug or Release mode. Use Developer mode to test your implementation with demo surveys
4. **customMode**: bool - Initializes Pollfish in custom mode (used when implementing a Rewarded approach)
5. **requestUUID**: String - Sets a unique id to identify a user. This param will be passed backthrough server-to-server callbacks

#### Debug Vs Release Mode

You can use Pollfish either in Debug or in Release mode. 
  
* **Debug mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
* **Release mode** is the mode to be used for a released app (start receiving paid surveys).


#### init Vs custom init

*	**custom mode = false** is the standard way of using Pollfish in your apps. Using init function with custom mode disabled, enables controlling the behavior of Pollfish in an app from Pollfish panel.

*	**custom mode = true** ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small Pollfish icon) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates.

For example:

```
FlutterPollfish.instance.init(
     apiKey: 'YOUR_API_KEY',
     pollfishPosition: 5,
     indPadding: 40,
     customMode: false,
     debugMode: true,
     requestUUID: 'USER_INTERNAL_ID');
```

### 5. Update your Privacy Policy

#### Add the following paragraph to your app's privacy policy


*Survey Serving Technology*

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone)  is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*


*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THE DRAWS. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.*


---
<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

If you have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>
<br/><br/><br/>

| **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process users need to go through in order to join the platform. Bear in mind that if a paid survey is available at that point of time, the demographic questions will be inserted at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this new type of targeting.

<br/>

<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>
<br/>


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://pollfish.zendesk.com/hc/en-us/articles/213287545">here</a>. 


<br/>

### 6\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>
<br/>
<br/>



## Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys. All these steps are optional.
<br/>
<br/>


### 7. Implement Pollfish event listeners (optional)

#### 7.1 Get notified when a Pollfish survey is received (optional)

You can be notified when a Pollfish survey is received.

For example:

```
FlutterPollfish.instance.setPollfishReceivedSurveyListener(onPollfishSurveyReveived);
```

```
void onPollfishSurveyReveived(String result) => setState(() {

    List<String> surveyCharacteristics = result.split(',');

     if (surveyCharacteristics.length >= 4) {
       String _logText =
              'Survey Received: - SurveyInfo with CPA: ${surveyCharacteristics[0]} and IR: ${surveyCharacteristics[1]} and LOI: ${surveyCharacteristics[2]} and SurveyClass: ${surveyCharacteristics[3]}';
    }
 });
```

#### 9.2 Get notified when a Pollfish survey is completed (optional)

You can be notified when a Pollfish survey is completed.

For example:

```
FlutterPollfish.instance.setPollfishCompletedSurveyListener(onPollfishSurveyCompleted);
```

```
void onPollfishSurveyCompleted(String result) => setState(() {

    List<String> surveyCharacteristics = result.split(',');

     if (surveyCharacteristics.length >= 4) {
       String _logText =
              'Survey Completed: - SurveyInfo with CPA: ${surveyCharacteristics[0]} and IR: ${surveyCharacteristics[1]} and LOI: ${surveyCharacteristics[2]} and SurveyClass: ${surveyCharacteristics[3]}';
    }
 });
```

#### 9.3 Get notified when a user is not eligible for a Pollfish survey (optional)

You can be notified when a user is not eligible for a Pollfish survey.

For example:

```
FlutterPollfish.instance.setPollfishUserNotEligibleListener(onPollfishUserNotEligible);
```

```
void onPollfishUserNotEligible() => setState(() {

   String _logText = 'User Not Eligible';
}
```

#### 9.4 Get notified when a Pollfish survey is not available (optional)

You can be notified when a Pollfish survey is not available

For example:

```
FlutterPollfish.instance.setPollfishSurveyNotAvailableSurveyListener(onPollfishSurveyNotAvailable);
```

```
void onPollfishSurveyNotAvailable() => setState(() {
   String _logText = 'Survey Not Available';
});
```

#### 9.5 Get notified when a Pollfish survey panel is open (optional)

You can be notified when Pollfish survey panel is open

For example:

```
FlutterPollfish.instance.setPollfishSurveyOpenedListener(onPollfishSurveyOpened);
```

```
void onPollfishSurveyOpened() => setState(() {
    String _logText = 'Survey Panel Open';
});
```

#### 9.6 Get notified when a Pollfish survey panel is closed (optional)

You can be notified when Pollfish survey panel is closed

For example:

```
pollfishplugin.setEventCallback('onPollfishOpened',app.pollfishPanelClosedEvent);
```

```
void onPollfishSurveyClosed() => setState(() {
   String _logText = 'Survey Panel Closed';
}

```


#### 9.7 Get notified when a user rejected a survey (optional)

You can be notified when Pollfish survey panel is closed

For example:

```
FlutterPollfish.instance.setPollfishUserRejectedSurveyListener(onPollfishUserRejectedSurvey);```
```

```
void onPollfishUserRejectedSurvey() => setState(() {
  String _logText = 'User Rejected Survey';
});
```



### 10. Manually show/hide Pollfish panel (optional)

You can manually hide and show Pollfish panel from your view by calling anywhere after initialization: 

For example:

```
FlutterPollfish.instance.show();
```

or

```
FlutterPollfish.instance.hide();
```


## Example

If you want to have a look at sample code on how you can call and use Pollfish plugin in your app, you can review the example app included.

