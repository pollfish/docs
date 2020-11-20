<div class="changelog" data-version="5.6.1">
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

*   Unity 4.6.8 +
*   iOS 9.0 +
*   Android 16 +

Please set minimum version of your project accordingly.

> **Note:** Pollfish does not work on Editor, so please do try only on mobile devices
<br/>

> **Note:** Pollfish iOS SDK utilizes Apple's Advertising ID (IDFA) to identify and retarget users with Pollfish surveys. As of iOS 14 you should initialize Pollfish Unity plugin in iOS only if the relevant IDFA permission was granted by the user

<br/><br/>

## Steps Analytically
<br/>
### 1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](//www.pollfish.com/login/publisher)
<br/><br/>
### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click **"Add a new app"** on Pollfish Developer Dashboard in section **"My Apps"**. Copy then the given API key for this app, in order to use later on, when initializing Pollfish within your code.

> **Note:** If your app supports both Android and iOS it would be better to create 2 different apps on the dashboard and use different API keys for each platform in your Unity code

<br/>
### 3\. Import Pollfish in your project

Download Pollfish Unity Plugin from the website. In Pollfish Unity Plugin zip file you will find a **.unitypackage** file. You can use this file to easily import plugin’s necessary files.

### Import Pollfish unity package

*   Open your Unity project and right click on your Assets folder in your Project area or select Assets from the menu and then choose **Import Package**, then **Custom Package** and finally select **PollfishUnityPlugin.unitypackage**

    ![](https://storage.googleapis.com/pollfish_production/doc_images/import_package.png)
*   If you want to exlude demo scene please uncheck **Assets/Plugins/Pollfish/demo** folder. Have in mind that in demo folder you will find **PollfishDemo.cs file** that demonstrates Pollfish Unity Plugin usage within a scene.
*   Review the package files and then select Import. If you are targeting only Android platform for example you can uncheck the iOS folder and vice versa.

### Check/uncheck files to import
<br/>
Imported files will be listed in the following directories:

![alt text](https://storage.googleapis.com/pollfish_production/doc_images/import_un.png)

- **Assets/Editor** – Files to help with initial setup

<div style="margin-left: 40px;">

**If you target iOS** ![alt text](https://storage.googleapis.com/pollfish-images/ios-icon.png)

* **PollfishBuildPostprocessor.cs** IS used to automatically add Pollfish necessary frameworks in your XCode project. If you do not want to have to link each time the necessary frameworks in your XCode project you can deselect them during importing.

</div>

- **Assets/ExternalDependencyManager** – Files to help with Goolge Play Services Setup
<div style="margin-left: 40px;">

**If you target Android** ![alt text](https://storage.googleapis.com/pollfish-images/android-icon.png)

* **ExternalDependencyManager** folder contains files to allow automatically add Google Play Services in your Android project from Unity menu.

> **Note:** Please have in mind that in order to use Pollfish you have to include Google Play Services in your Unity project. You can easily do that by selecting **Assets –> External Dependency Manager -> Android Resolver -> Resolve**. If you do not have Google Play Services you can install them through Android SDK Manager.

![alt text](https://storage.googleapis.com/pollfish_production/doc_images/resolve1.png)

or

![alt text](https://storage.googleapis.com/pollfish_production/doc_images/resolve2.png)

</div>

You can customize the seetings of Android Resolver. By selecting **Assets –> External Dependency Manager -> Android Resolver -> Settings**. Be sure to unselect **Patch AndroidManifest.xml**

![alt text](https://storage.googleapis.com/pollfish_production/doc_images/settings_resolver.png)


| **Note:** If you do not want to use ExternalDepencyManager you need to manually add the following dependencies to your project in order for Pollfish to wrok properly:

```  
    implementation 'com.google.android.gms:play-services-ads-identifier:16.0.0'
    implementation 'com.google.android.gms:play-services-base:16.0.1'
```

- **Assets/Plugins/Android** – Android Pollfish libraries and resources

- **Assets/Plugins/iOS** – Pollfish framework and bridge files.

- **Assets/Plugins/Pollfish** – Pollfish C# bridge files that allow communication between Unity and Java for Android and Unity and Objective-C for iOS.

- **Assets/Plugins/Pollfish/demo** – A simple scene that demonstrates Pollfish plugin integration
<br/><br/><br/>



### 4. Initializing Pollfish

You should use a MonoBehaviour object for your scene that will enable interaction with Pollfish Unity plugin. Pollfish should be initialized when an app starts or resumes (this way you will always receive new surveys when available).

### Pollfish API Key

In order to initialize Pollfish, you need an API Key as described in step 2

**1\. apiKey** (string)- Your API Key. This is the key that allows you to use Pollfish in your app. You can find it on Pollfish website after your registration, when you create an app in “My apps” section in the panel.  

```
Pollfish.PollfishInitFunction(apiKey, pollfishParams);
```

### Pollfish PollfishParams object

In order to initialize Pollfish you need to create a PollfishParams object:

```
Pollfish.PollfishParams pollfishParams = new Pollfish.PollfishParams();
  
pollfishParams.OfferwallMode(offerwallMode);
pollfishParams.IndicatorPadding(indPadding);
pollfishParams.ReleaseMode(releaseMode);
pollfishParams.RewardMode(rewardMode);
pollfishParams.IndicatorPosition((int)pollfishPosition);
pollfishParams.RequestUUID(requestUUID);
pollfishParams.UserAttributes(userAttributes);
```

PollfishParams can be initialized with the following calls:

**1\. IndicatorPosition(PollfishPosition pollfishPosition)** - Sets the Position where you wish to place Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png)

Also this setting sets from which side of the screen you would like Pollfish survey panel to slide in.

<span style="text-decoration: underline">There are six different options available: </span> 

*   **Position.TOP_LEFT**  
*   **Position.TOP_RIGHT**  
*   **Position.BOTTOM_LEFT**  
*   **Position.BOTTOM_RIGHT**  
*   **Position.MIDDLE_LEFT** 
*   **Position.MIDDLE_RIGHT**  

**2\. IndicatorPadding(int indPadding)** - The padding from the top or bottom of the screen according to PollfishPosition of the indicator (small icon) specified before (0 is the default value)  

> **Note:** if used in MIDDLE position, padding is calculating from the top

**3\. ReleaseMode(bool releaseMode)** – Debug or Release mode  

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).  
*   **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

> **Note:** Be careful to set release mode parameter to true prior releasing to Google Play or AppStore!  

4\. **RewardMode(bool rewardMode)** – Initializes Pollfish in reward mode if set to true. By default this is set to false.

**true Vs false**

*   **true** -  ignores Pollfish panel behavior from Pollfish Developer Dashboard. It always skips showing Pollfish indicator (small Pollfish icons) and hides Pollfish survey panel view from users. This method is aimed to be used when app developers want to incentivize first somehow their users. 
*   **false** - is the standard way of using Pollfish in your apps. This option enables controlling behavior (intrusiveness) of Pollfish panel in an app from Pollfish Developer Dashboard.

5\. **OfferwallMode(bool offerwallMode)** – Enables offerwall mode. If not set, one single survey is shown each time.

6\. **RequestUUID(string requestUUID)** – Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

7\. **UserAttributes(Dictionary<string, string> userAttributes)** – Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and also achieve a better fill rate and higher priced surveys.

| **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default

An example of how you can pass user demographics can be found below:

```

Dictionary<string, string> userAttributes = new Dictionary<string, string> ();
		
userAttributes.Add ("gender", "1");
userAttributes.Add ("year_of_birth", "1974");
userAttributes.Add ("marital_status", "2");
userAttributes.Add ("parental", "3");
userAttributes.Add ("education", "1");
userAttributes.Add ("employment", "1");
userAttributes.Add ("career", "2");
userAttributes.Add ("race", "3");
userAttributes.Add ("income", "1");

Pollfish.PollfishParams pollfishParams = new Pollfish.PollfishParams();

pollfishParams.UserAttributes(userAttributes);
		
```
You can check values mapping for demographic surveys in the following [section](https://www.pollfish.com/docs/demographic-surveys)

<br/>

Below you can see an example of the init function. Remember to set your API key for each platform prior calling init:

```

private string apiKey;
	
private Position pollfishPosition = Position.MIDDLE_LEFT;

private bool releaseMode = true;
private bool rewardMode = false;
private int indPadding = 10;
private int offerwallMode = false;

public void OnEnable()
{
  #if UNITY_ANDROID
  
  apiKey = "ANDROID_API_KEY";
  
  #elif UNITY_IPHONE
  
  apiKey = "IOS_API_KEY";
  
  #endif

  Pollfish.PollfishParams pollfishParams = new Pollfish.PollfishParams();

  pollfishParams.OfferwallMode(offerwallMode);
  pollfishParams.IndicatorPadding(indPadding);
  pollfishParams.ReleaseMode(releaseMode);
  pollfishParams.RewardMode(rewardMode);
  pollfishParams.IndicatorPosition((int)pollfishPosition);
		
  Pollfish.PollfishInitFunction(apiKey, pollfishParams);
}
```

<br/>

### 5. Handling Android or iOS specific cases

###  5.1 If you are targeting Android ![alt text](https://storage.googleapis.com/pollfish-images/android-icon.png)

### Android Back Event

Since Pollfish uses Android back button to close its panel if open, if you want to replicate this behavior you should capture  back button event and call Pollfish.ShouldQuit(); to inform the library and act accordingly.

```
public void Update ()
{        
	/* handling Android back event */	

	if (Input.GetKeyDown (KeyCode.Escape)) {

		Pollfish.ShouldQuit();
	}
}
```

### AndroidManifest file

We have included an AndroidManifest.xml file that will work for most of user cases However if you need to include your own AndroidManifest file remember to add the following lines:

```
<meta-data android:name="unityplayer.ForwardNativeEventsToDalvik" android:value="true" />
```

within your Activity <activity></activity> that holds the following intent filters:

```
<intent-filter>
  <action android:name="android.intent.action.MAIN" />
  <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

This line enable touch events to pass through Pollfish SDK.

Finally, Pollfish requires Internet permission in order to work, so please do not forget to add the following line if you do not already have it.

```
<uses-permission android:name="android.permission.INTERNET"/>
```


### Using Proguard

If you use proguard with your app, please insert the following lines in your proguard configuration file:

```
-libraryjars libs/pollfish_unity_bridge.jar

-keep class com.pollfish.** { *; }
-keep class com.pollfish_unity.** { *; }
-dontwarn com.pollfish.**
```

where **pollfish_unity_bridge.jar** is the bridge jar between Pollfish and Unity that are placed in your Assets folder.

> **Note:** Using Proguard with Pollfish requires setting your Project Build Target to Android 4.2.2 (API 17) or above!**

<br/>
###  5.2 If you are targeting iOS ![alt text](https://storage.googleapis.com/pollfish-images/ios-icon.png)

### Distributing your app to AppStore

Pollfish uses Advertising Identifier (IDFA) for survey distribution and therefore when submitting your app to the App you should select the following options as seen in the image below:  

![](/homeassets/images/documentation/idfa_2.jpg)

<br/>

### 6\.  Update your Privacy Policy

Add the following paragraph to your App's Privacy Policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Publishers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user's device data (including Advertising ID, Device ID, other available electronic identifiers and further response meta-data is automatically sent, via our app, to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully the Pollfish respondent terms located at [https://www.pollfish.com/terms/respondent](https://www.pollfish.com/terms/respondent). These data will be associated with your answers to the questionnaires whenever Pollfish sends such questionnaires to eligible users. Pollfish may share such data with third parties, clients and business partners, for commercial purposes. By downloading the application, you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by visiting the following link [https://www.pollfish.com/respondent/opt-out](https://www.pollfish.com/respondent/opt-out). We once more invite you to check the Pollfish respondent's terms of use, if you wish to have more detailed view of the way Pollfish works and with whom Pollfish may further share your data."*  

<br/><br/>

---

### At this point you are ready to publish your app with Pollfish! 

> **Note:** Remember to turn your app in release mode prior publishing to a relevant app store

<br/><br/><br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://help.pollfish.com/en/collections/24867-faq-publishers">FAQ page</a>
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


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 7.2 to skip or shorten Pollfish Demographic surveys.

<br/>

### 7\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>
<br/>
<br/>
