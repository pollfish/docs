<div class="changelog" data-version="6.0.3">
v6.0.2

- Updated with Pollfish iOS SDK v6.0.3

v6.0.1

- Updated with Pollfish Android SDK v6.1.3 and Pollfish iOS SDK v6.0.2

v6.0.0

- New Event Subscribtion mechanism
- Bug fixes
- New Public interface

v5.7.7
	
- Updated with Pollfish Android SDK v6.1.2 and Pollfish iOS SDK v6.0.1

v5.7.6
	
- Updated with Pollfish Android SDK v6.1.1

v5.7.5

- Updated with Android SDK v6.1.0

v5.7.4

- Updated with Android SDK v6.0.4
- Updated with unity-jar-resolver v1.2.165
- Fixed XCode build `Multiple commands produce` issue

v5.7.3
	
- Fixed issue with builds on Windows

v5.7.2

- Updated with Android SDK v6.0.3

v5.7.1
	
- Fixed issue with empty UserProperties dictionary
	
v5.7.0
	
- Update with Android SDK v6.0.2 and iOS SDK v6.0.0

v5.6.3

- Updated with iOS SDK (v5.5.2)

v5.6.2

- Updated Google Jar Resolver. 
- Added Pod support for iOS builds.

v5.6.1

- Updated with iOS SDK (v5.4.1) and Android SDK (v5.6.0)

v5.6.0

- Updated with iOS SDK (v5.3.0)

v5.5.1

- Updated with Android SDK (v5.5.1) that aligns with the latest Google Play policy changes

v5.5.0

- Updated with Android SDK (v5.5.0)

v5.4.1

- Updated with Android SDK (v5.4.1)

v5.4.0

- Updated with Android SDK (v5.4.0)

	
v5.3.0

- Added support for Unity 2019.3+
- Updated with the latest External Dependency Manager from Google Ads
- Updated with iOS SDK (v5.2.5) and Android SDK (v5.3.0)

v5.2.0

- Updated with iOS SDK (v5.2.0) and Android SDK (v5.1.0)

v5.1.0

- Updated with iOS SDK v5.1.0

v5.0.0

- Added support for offerwall
- New Android minimum supported version is 16
- Updated with Pollfish Android & iOS SDKs v5.0.x

v4.5.1

- Fixed crash issues relevant with with AndroidManifest and UnityPlayerActivity

v4.5.0

- Updated with Pollfish latest Android & iOS SDK v4.5.x

v4.4.0

- Added support for Unity 2018
- Updated with Pollfish latest Android & iOS SDK v4.4.0
- Added user rejected event
- Fixed bugs

v4.3.6

- Updated with Pollfish latest Android & iOS SDK v4.3.4

v4.3.6

- Updated with Pollfish latest iOS SDK v4.2.4 to fix bitcode issue

v4.3.5

- Removed rendering workaround for Unity 5.6 after 5.6.1p4 patch release

v4.3.4

- Added support for sending user attributes during init
- Deprecated setCustomAttributes
- Fixed rendering bug of Unity 5.6
- Updated to latest Google's Unity Jar Resolver
- Updated Android & iOS SDK to the latest

v4.3.3

- Updated iOS SDK to the latest

v4.3.2

- Updated iOS SDK to latest with support for ATS

v4.3.1

- Updated Android SDK to latest on with 3rd party survey providers support
- Updated to jar resolver from Google in order to support Google Play Services

v4.2.0

- New updated iOS and Android SDKs
- Added video, rating, slider, open ended, open ended numerical and description questions support
- Improved performance, bug fixes
- Deprecated shouldQuit events and replaces with function

v4.1.0

- Support of manual set of devMode for android by ignoring key of signing
- Respect and submit of Google Advertising Id

v4.0.0

- Initial Release
- Support for Lollipop
</div>
<br/>

#### **Requirements**

Pollfish Unity Plugin works with:

*   Unity 2020 +
*   iOS 9.0 +
*   Android 21 +

Please set minimum version of your project accordingly.

> **Note:** Pollfish does not work on Editor, so please do try only on mobile devices

> **Note:** Pollfish SDK requires minSdk 21. If your app supports a lower minSdk you can still build your app and exlude Pollfish from targets lower than 21 by exporting an Android project from the Unity's Build Settings and adding the following block on the `AndroidManifest.xml` of the `unityLibrary` module.

**AndroidManifest.xml**

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    ... >

    <uses-sdk tools:overrideLibrary="com.pollfish.pollfish" />

    <application
	... >
        ...
    </application>
```

<br/>

> **Note:** Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower. Offerwall integrations perform better compared to single survey integrations when no IDFA permission is given

<br/>

You can find instructions on how to install ios-support package and request for IDFA permission from a Unity script [here](https://github.com/Unity-Technologies/com.unity.ads.ios-support)

> **Note:** If you are updating from version 5.7.6 or lower to 6.0.0 or higher we recommend to clean your project from any of Pollfish Unity Plugin files and then import the lastest version. A comparisson between the v5 and v6 public API can be found on the following migration guide

<br/>

## Migrate from to v6

<details><summary>➤ <b>Usage Diff</b> (Click to expand)</summary>
<table>
<tr>
<td>

<br/>

<span style="color:red">-</span>

<td>

#### **Initialization** <br/>

```csharp
Pollfish.PollfishInitFunction(apiKey, pollfishParams);
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```csharp
Pollfish.Init(pollfishParams)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **PollfishParams** <br/>

```csharp
Pollfish.PollfishParams pollfishParams = new Pollfish.PollfishParams();
  
pollfishParams.OfferwallMode(offerwallMode);
pollfishParams.IndicatorPadding(indicatorPadding);
pollfishParams.ReleaseMode(releaseMode);
pollfishParams.RewardMode(rewardMode);
pollfishParams.IndicatorPosition((int) indicatorPosition);
pollfishParams.RequestUUID(requestUUID);
pollfishParams.UserAttributes(userAttributes);
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```dart
Pollfish.Params pollfishParams = new Pollfish.Params(apiKey)
  .OfferwallMode(offerwallMode)
  .IndicatorPadding(indicatorPadding)
  .ReleaseMode(releaseMode)
  .RewardMode(rewardMode)
  .IndicatorPosition(indicatorPostion)
  .RequestUUID(requestUUID)
  .UserProperties(userProperties);
		
Pollfish.Init(pollfishParams);
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Event Subscription** <br/>

`PollfishEventListener` class has been removed where it used to track the status of Pollfish Surveys.

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

Publishers have the option to subscribe to the listeners of their choice and get notified asynchronously for Pollfish Surveys lifecycle events.

```csharp
Pollfish.SurveyCompletedEvent += SurveyCompleted;
...

public void SurveyCompleted(SurveyInfo surveyInfo)
{
  ....
}
```

</table>
</details>

<br/>

## Analytical Steps 

<br/>

## 1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](www.pollfish.com/login/publisher)

<br/>

## 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click **"Add a new app"** on Pollfish Developer Dashboard in section **"My Apps"**. Copy then the given API key for this app, in order to use later on, when initializing Pollfish within your code.

> **Note:** If your app supports both Android and iOS it would be better to create 2 different apps on the dashboard and use different API keys for each platform in your Unity code

<br/>

## 3. Import Pollfish in your project

Download Pollfish Unity Plugin from the website. In Pollfish Unity Plugin .zip file you will find the **PollfishUnityPlugin.unitypackage** file. You can use this file to easily import plugin’s necessary files.

### Import Pollfish unity package

*   Open your Unity project and right click on your Assets folder in your Project area or select Assets from the menu and then choose **Import Package**, then **Custom Package** and finally select **PollfishUnityPlugin.unitypackage**

    ![](https://storage.googleapis.com/pollfish_production/doc_images/import_package.png)
*   If you want to exlude demo scene please uncheck **Assets/Pollfish/Demo** folder. Have in mind that in demo folder you will find **PollfishDemo.cs** file which demonstrates Pollfish Unity Plugin usage within a scene.

*   Review the package files and then select Import. If you are targeting only Android platform for example you can uncheck the iOS folder and vice versa.

### Check/uncheck files to import

Imported files will be listed in the following directories:

![alt text](https://storage.googleapis.com/pollfish_production/doc_images/import_unity_new_2.png)

- **Assets/ExternalDependencyManager** – Files to help with plugin dependencies retrieval using <a href="https://github.com/googlesamples/unity-jar-resolver">unity-jar-resolver</a>.
<div style="margin-left: 40px;">

**If you target iOS** ![alt text](https://storage.googleapis.com/pollfish-images/ios-icon.png)

**External Dependency Manager** will automatically create a **Pod** XCode workspace with Pollfish SDK dependency.

> **Note**: Make sure that you use the *.xcworkspace and **NOT** the *.xcodeproj for any additional changes after the iOS project build through Unity.

**If you target Android** ![alt text](https://storage.googleapis.com/pollfish-images/android-icon.png)

**External Dependency Manager** will automatically add Google Play Services in your Android project.

> **Note:** Please have in mind that in order to use Pollfish you have to include Google Play Services in your Unity project. You can easily do that by selecting **Assets –> External Dependency Manager -> Android Resolver -> Resolve**. If you do not have Google Play Services you can install them through Android SDK Manager.


![alt text](https://storage.googleapis.com/pollfish_production/doc_images/resolve_new.png)



> **Note:** If you do not want to use External Depency Manager you need to manually add the following dependencies to your Android project:
>
>```groovy  
>dependencies {
>  ...
>  implementation 'com.pollfish:pollfish-googleplay:6.1.2'
>}
>```
>
>and then include the Pollfish iOS SDK framework in you iOS XCode project in order for Pollfish to work properly. 
>Please visit this <a href="https://www.pollfish.com/docs/ios">guide</a> to download the latest framework version and import it on a XCode project.

</div>

- **Assets/Pollfish/Plugins/Android** – Android Pollfish libraries and resources.

- **Assets/Pollfish/Plugins/iOS** – Pollfish bridge file.

- **Assets/Pollfish/Editor** – Pollfish C# files that allow communication between Unity and Java for Android and Unity and Objective-C for iOS.

- **Assets/Pollfish/Demo** – A simple scene that demonstrates Pollfish plugin integration.

<br/>

## 4. Initializing Pollfish

You should use a MonoBehaviour object for your scene that will enable interaction with Pollfish Unity plugin. Pollfish should be initialized when an app starts or resumes (this way you will always receive new surveys when available).

### Pollfish API Key

In order to initialize Pollfish you need to create a `Pollfish.Params` instance:

```csharp
Pollfish.Init(pollfishParams);
```

<br/>

### `Pollfish.Params` object

In order to initialize `Pollfish.Params`, you need an API Key as described in step 2.

**`new Pollfish.Params(bool apiKey)`** - Your API Key. This is the key that allows you to use Pollfish in your app. You can find it on Pollfish website after your registration, when you create an app in “My apps” section in the panel.  

```csharp
Pollfish.Params pollfishParams = new Pollfish.Params(apiKey)
  .OfferwallMode(offerwallMode)
  .IndicatorPadding(indicatorPadding)
  .ReleaseMode(releaseMode)
  .RewardMode(rewardMode)
  .IndicatorPosition(indicatorPosition)
  .RequestUUID(requestUUID)
  .UserProperties(userProperties);
```

`Pollfish.Params` can be configured with the following methods:

1\. **`IndicatorPosition(Position indicatorPosition)`** - Sets the Position where you wish to place Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png)

Also this setting sets from which side of the screen you would like Pollfish survey panel to slide in.

<span style="text-decoration: underline">There are six different options available: </span> 

*   **Position.TOP_LEFT**  
*   **Position.TOP_RIGHT**  
*   **Position.BOTTOM_LEFT**  
*   **Position.BOTTOM_RIGHT**  
*   **Position.MIDDLE_LEFT** 
*   **Position.MIDDLE_RIGHT**  

2\. **`.IndicatorPadding(int indicatorPadding)`** - The padding from the top or bottom of the screen according to PollfishPosition of the indicator (small icon) specified before (`.TOP_LEFT` is the default value)  

> **Note:** if used in MIDDLE position, padding is calculating from the top

3\. **`.ReleaseMode(bool releaseMode)`** – Debug or Release mode  

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).  
*   **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

> **Note:** Be careful to set release mode parameter to true prior releasing to Google Play or AppStore!  

4\. **`.RewardMode(bool rewardMode)`** – Initializes Pollfish in reward mode if set to true. By default this is set to false.

**true Vs false**

*   **true** -  ignores Pollfish panel behavior from Pollfish Developer Dashboard. It always skips showing Pollfish indicator (small Pollfish icons) and hides Pollfish survey panel view from users. This method is aimed to be used when app developers want to incentivize first somehow their users. 
*   **false** - is the standard way of using Pollfish in your apps. This option enables controlling behavior (intrusiveness) of Pollfish panel in an app from Pollfish Developer Dashboard.

5\. **`.OfferwallMode(bool offerwallMode)`** – Enables offerwall mode. If not set, one single survey is shown each time.

6\. **`.RequestUUID(string requestUUID)`** – Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

7\. **`.UserProperties(Dictionary<string, string> userProperties)`** – Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and also achieve a better fill rate and higher priced surveys.

> **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default

An example of how you can pass user demographics can be found below:

```csharp
Dictionary<string, string> userProperties = new Dictionary<string, string>
  {
    { "gender", "1" },
    { "year_of_birth", "1974" },
    { "marital_status", "2" },
    { "parental", "3" },
    { "education", "1" },
    { "employment", "1" },
    { "career", "2" },
    { "race", "3" },
    { "income", "1" }
  };

Pollfish.Params pollfishParams = new Pollfish.Params();

pollfishParams.UserProperties(userProperties);
```

You can check values mapping for demographic surveys in the following [section](https://www.pollfish.com/docs/demographic-surveys)

<br/>

Below you can see an example of the `Init` function. Remember to set your API key for each platform prior calling init:

```csharp
#if UNITY_ANDROID
	public string apiKey = "YOUR_ANDROID_API_KEY";
#elif UNITY_IPHONE
	public string apiKey = "YOUR_IOS_API_KEY";
#endif
	
private Position pollfishPosition = Position.MIDDLE_LEFT;
private bool releaseMode = false;
private bool rewardMode = false;
private int indicatorPadding = 10;
private int offerwallMode = false;

public void OnEnable()
{
  Pollfish.Params pollfishParams = new Pollfish.Params()
    .OfferwallMode(offerwallMode)
    .IndicatorPadding(indicatorPadding)
    .ReleaseMode(releaseMode)
    .RewardMode(rewardMode)
    .IndicatorPosition(pollfishPosition);
		
  Pollfish.Init(apiKey, pollfishParams);
}
```

<br/>

## 5. Handling Android or iOS specific cases

###  5.1 If you are targeting Android ![alt text](https://storage.googleapis.com/pollfish-images/android-icon.png)

### Android Back Event

Since Pollfish uses Android back button to close its panel if open, if you want to replicate this behavior you should capture  back button event and call Pollfish.ShouldQuit(); to inform the library and act accordingly.

```csharp
public void Update ()
{        
	/* handling Android back event */	

	if (Input.GetKeyDown (KeyCode.Escape)) {

		Pollfish.ShouldQuit();

	}
}
```

<br/>

### AndroidManifest file

We have included an AndroidManifest.xml file that will work for most of user cases However if you need to include your own AndroidManifest file remember to add the following lines:

```xml
<meta-data android:name="unityplayer.ForwardNativeEventsToDalvik" android:value="true" />
```

within your Activity <activity></activity> that holds the following intent filters:

```xml
<intent-filter>
  <action android:name="android.intent.action.MAIN" />
  <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

This line enable touch events to pass through Pollfish SDK.

Finally, Pollfish requires Internet permission in order to work, so please do not forget to add the following line if you do not already have it.

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

<br/>

### Using Proguard

If you use proguard with your app, please insert the following lines in the proguard configuration file under the unityLibrary module:

```
-keep class com.pollfish.** { *; }
-keep class com.pollfish_unity.** { *; }
-dontwarn com.pollfish.**
```

<br/>

###  5.2 If you are targeting iOS ![alt text](https://storage.googleapis.com/pollfish-images/ios-icon.png)

### Distributing your app to AppStore

Pollfish uses Advertising Identifier (IDFA) for survey distribution (if permission granted) and therefore when submitting your app to the App you should select the following options as seen in the image below:  

![](/homeassets/images/documentation/idfa_2.jpg)

<br/>

## Optional Section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys. All these steps are optional.

<br/>

## 6. Implement Pollfish Event Listeners

<br/>

### 6.1. Get notified when a Pollfish survey is received

You can be notified when a Pollfish survey is received. With this notification, you can also get informed about the type of survey that was received, money to be earned if survey gets completed, shown in USD cents and other info around the survey such as LOI and IR.

<br/>

> **Note:** If Pollfish is initialized in offerwall mode then the event parameter will be `null`, otherwise it will include info around the received survey.

<br/>

```csharp
Pollfish.SurveyReceivedEvent += SurveyReceived;

public void SurveyReceived(SurveyInfo surveyInfo)
{
  if (surveyInfo == null)
  {
    Debug.Log("PollfishDemo: Survey Offerwall received");
  }
  else
  {
    Debug.Log("PollfishDemo: Survey was completed - " + surveyInfo.ToString());
  }
}
```

<br/>

### 6.2. Get notified when a Pollfish survey is completed

You can be notified when a user completed a survey. With this notification, you can also get informed about the type of survey, money earned from that survey in USD cents and other info around the survey such as LOI and IR.

```csharp
Pollfish.SurveyCompletedEvent += SurveyCompleted;

public void SurveyCompleted(SurveyInfo surveyInfo)
{
  Debug.Log("PollfishDemo: Survey was Completed - " + surveyInfo.ToString());
}
```

<br/>

### 6.3. Get notified when a user is not eligible for a Pollfish survey

You can be notified when a user is not eligible for a Pollfish survey. In market research monetization, users can get screened out while completing a survey beucase they are not relevant with the audience that the market researcher was looking for. In that case the user not eligible notification will fire and the publisher will make no money from that survey. The user not eligible notification will fire after the surveyReceived event, when the user starts completing the survey.

```csharp
Pollfish.UserNotEligibleEvent += UserNotEligible;

public void UserNotEligible()
	{
		Debug.Log("PollfishDemo: User not eligible");
	}
```

<br/>

### 6.4. Get notified when a Pollfish survey is not available

You can be notified when a Pollfish survey is not available.

```csharp
Pollfish.SurveyNotAvailableEvent += SurveyNotAvailable;

public void SurveyNotAvailable()
{
  Debug.Log("PollfishDemo: Survey not available");
}
```

<br/>

### 6.5. Get notified when a user has rejected a Pollfish survey

You can be notified when a user has rejected a Pollfish survey.

```csharp
Pollfish.UserRejectedSurveyEvent += UserRejectedSurvey;

public void UserRejectedSurvey()
{
  Debug.Log("PollfishDemo: User rejected survey");
}
```

<br/>

### 6.6. Get notified when a Pollfish survey panel has opened

You can register and get notified when a Pollfish survey panel has opened. Publishers usually use this notification to pause a game until the pollfish panel is closed again.

```csharp
Pollfish.SurveyOpenedEvent += SurveyOpened;

public void SurveyOpened()
{
  Debug.Log("PollfishDemo: Survey was opened");
}
```

<br/>

### 6.7. Get notified when a Pollfish survey panel has closed

You can register and get notified when a Pollfish survey panel has closed. Publishers usually use this notification to resume a game that they have previously paused when the Pollfish panel was opened.

```csharp
Pollfish.SurveyClosedEvent += SurveyClosed;

public void SurveyClosed()
{
  Debug.Log("PollfishDemo: Survey was closed");
}
```

### Unsubsribe from Pollfish Event Listeners

Please make sure you unsubscribe from Pollfish Event Listeners, preferably on the scene destruction to avoid duplicated events.

```csharp
public void OnDisable()
{
  Pollfish.SurveyCompletedEvent -= SurveyCompleted;
  Pollfish.SurveyOpenedEvent -= SurveyOpened;
  Pollfish.SurveyClosedEvent -= SurveyClosed;
  Pollfish.SurveyReceivedEvent -= SurveyReceived;
  Pollfish.SurveyNotAvailableEvent -= SurveyNotAvailable;
  Pollfish.UserNotEligibleEvent -= UserNotEligible;
  Pollfish.UserRejectedSurveyEvent -= UserRejectedSurvey;
}
```

<br/>

## 7. Manually show/hide Pollfish panel

You can manually hide and show Pollfish by calling the functions below, after initialization.

```csharp
Pollfish.show();
```

```csharp
Pollfish.hide();
```

<br/>

## 8. Check if Pollfish Surveys are available on your device

After you initialize Pollfish and a survey is received you can check at any time if the survey is available at the device by calling the following function.

```csharp
bool isPresent = Pollfish.isPollfishPresent():
```

<br/>

## 9. Check if Pollfish Panel is open

You can check at any time if the survey panel is open by calling the following function.

```csharp
bool isOpen = Pollfish.isPollfishPanelOpen();
```

<br/>

## 10\.  Update your Privacy Policy

Add the following paragraph to your App's Privacy Policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Publishers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user's device data (including Advertising ID, Device ID, other available electronic identifiers and further response meta-data is automatically sent, via our app, to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully the Pollfish respondent terms located at [https://www.pollfish.com/terms/respondent](https://www.pollfish.com/terms/respondent). These data will be associated with your answers to the questionnaires whenever Pollfish sends such questionnaires to eligible users. Pollfish may share such data with third parties, clients and business partners, for commercial purposes. By downloading the application, you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by visiting the following link [https://www.pollfish.com/respondent/opt-out](https://www.pollfish.com/respondent/opt-out). We once more invite you to check the Pollfish respondent's terms of use, if you wish to have more detailed view of the way Pollfish works and with whom Pollfish may further share your data."*  

---

### At this point you are ready to publish your app with Pollfish! 

> **Note:** Remember to turn your app in release mode prior publishing to a relevant app store

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>

<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://help.pollfish.com/en/collections/24867-faq-publishers">FAQ page</a>

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

In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys [here](https://www.pollfish.com/docs/demographic-surveys).

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 7.2 to skip or shorten Pollfish Demographic surveys.

<br/>

### 11\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>

<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.

<br/>

## More Info

You can read more info on how the Native Pollfish SDKs work on Android and iOS at the following links:

<br/>

[Pollfish Android SDK Integration Guide](https://pollfish.com/docs/android)

[Pollfish iOS SDK Integration Guide](https://pollfish.com/docs/ios)