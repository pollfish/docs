<div class="changelog" data-version="4.3.7">
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
*   iOS 7.0 +
*   Android 2.3.3 (10) +

Please set minimum version of your project accordingly.



> **Note:** There is an [issue](https://issuetracker.unity3d.com/issues/regression-android-banner-ads-are-invisible-but-clickable) with Unity 5.6 which affected Pollfish Unity Plugin, resulting to Pollfish surveys not being rendered on top of Unity's scene. That issue was fixed with [5.6.1p4 patch](https://unity3d.com/ru/unity/qa/patch-releases). If you are using a version of Unity that is still affected by that bug you can use this [version](https://storage.googleapis.com/pollfish_production/sdk/Unity/Pollfish%20Unity%20Plugin%20v4.3.4.zip) of Pollfish Unity Plugin. If you want to learn more on what happened in that bug behind the scened you can read the following [article](https://android.jlelse.eu/unity-and-android-connecting-the-dots-6368b31e86c5).


> **Note:** Pollfish does not work on Editor, so please do try only on mobile devices


<br/><br/>

## Steps Analytically
<br/>
### 1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](//www.pollfish.com/login/publisher)
<br/><br/>
### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click **"Add a new app"** on Pollfish Developer Dashboard in section **"My Apps"**. Copy then the given API key for this app, in order to use later on, when initializing Pollfish within your code.

> **Note:** If your app supports both Android and iOS it would be better to create 2 different apps on the dashboard and use different API keys for each platform in your Unity code

<br/><br/>
### 3\. Import Pollfish in your project

Download Pollfish Unity Plugin from the website. In Pollfish Unity Plugin zip file you will find a **.unitypackage** file. You can use this file to easily import plugin’s necessary files.

### Import Pollfish unity package

*   Open your Unity project and right click on your Assets folder in your Project area or select Assets from the menu and then choose **Import Package**, then **Custom Package** and finally select **PollfishUnityPugin.unitypackage**

    ![](/homeassets/images/documentation/unity/unity1.png)
*   If you want to exlude demo scene please uncheck **Assets/Plugins/Pollfish/demo** folder. Have in mind that in demo folder you will find **PollfishDemo.cs file** that demonstrates Pollfish Unity Plugin usage within a scene.
*   Review the package files and then select Import. If you are targeting only Android platform for example you can uncheck the iOS folder and vice versa.

### Check/uncheck files to import
<br/>
Imported files will be listed in the following directories:

![alt text](https://storage.googleapis.com/pollfish-images/pakcage_contents.png)

- **Assets/Editor** – Files to help with initial setup

<div style="margin-left: 40px;">

**If you target iOS** ![alt text](https://storage.googleapis.com/pollfish-images/ios-icon.png)

* **mod_pbproj.pyc, PostprocessBuildPlayer and PostprocessBuildPlayer_Pollfish and PollfishBuildPostprocessor.cs** are used to automatically add Pollfish necessary frameworks in your XCode project (if frameworks  show up in red color in your XCode project, ignore that and build). If you do not want to have to link each time the necessary frameworks in your XCode project you can deselect them during importing.

> **Note:** Be careful to replace your previous project when you build for iOS otherwise frameworks will be added more than once if you choose to append.

</div>

- **Assets/PlayServicesResolver** – Files to help with Goolge Play Services Setup
<div style="margin-left: 40px;">

**If you target Android** ![alt text](https://storage.googleapis.com/pollfish-images/android-icon.png)

* **PlayServicesResolver** folder contains files to allow automatically add Google Play Services in your Android project from Unity menu.

> **Note:** Please have in mind that in order to use Pollfish you have to include Google Play Services in your Unity project. You can easily do that by selecting **Assets –> Play Services Resolver -> Android Resolver -> Resolve Client Jars**. If you do not have Google Play Services you can install them through Android SDK Manager.

![alt text](https://storage.googleapis.com/pollfish-images/android_resolver.png)

or

![alt text](https://storage.googleapis.com/pollfish-images/new_unity_menu.png)

</div>

- **Assets/Plugins/Android** – Android Pollfish libraries and resources

- **Assets/Plugins/iOS** – Pollfish framework and bridge files.

- **Assets/Plugins/Pollfish** – Pollfish C# bridge files that allow communication between Unity and Java for Android and Unity and Objective-C for iOS.

- **Assets/Plugins/Pollfish/demo** – A simple scene that demonstrates Pollfish plugin integration
<br/><br/><br/>



### 4. Initializing Pollfish

You should use a MonoBehaviour object for your scene that will enable interaction with Pollfish Unity plugin. Pollfish should be initialized when an app starts or resumes.

```
void PollfishInitFunction(int pollfishPosition, int indPadding, string apiKey, bool debugMode, bool customMode);
```

### Pollfish init function takes the following parameters:

**1\. pollfishPosition** (PollfishPosition) - Sets Position where you wish to place  Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png)

<span style="text-decoration: underline">There are six different options available: </span> 

*   **Position.TOP_LEFT**  
*   **Position.TOP_RIGHT**  
*   **Position.BOTTOM_LEFT**  
*   **Position.BOTTOM_RIGHT**  
*   **Position.MIDDLE_LEFT** 
*   **Position.MIDDLE_RIGHT**  

**2\. indPadding** (int) - The padding from top or bottom of the screen according to PollfishPosition of the indicator (small red rectangle) specified before (0 is the default value)  

> **Note:** if used in MIDDLE position, padding is calculating from top.**  

**3\. apiKey** (string)- Your API Key. This is the key that allows you to use Pollfish in your app. You can find it on Pollfish website after your registration, when you create an app in “My apps” section in the panel.  

**4\. debugMode** (bool) – Debug or Release mode  

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).  
*   **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

> **Note:** Be careful to set andDebuggable parameter to false prior releasing to Google Play or AppStore!  

5\. **customMode** (bool) – Initializes Pollfish in custom mode if set to true. By default this is set to false.

**true Vs false**

*   **true** -  ignores Pollfish panel behavior from Pollfish Developer Dashboard. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish panel view to app users. This method is usually used when app developers want to incentivize first somehow their users. 
*   **false** - is the standard way of using Pollfish in your apps. This option enables controlling behavior (intrusiveness) of Pollfish panel in an app from Pollfish Developer Dashboard.

![alt text](https://pollfish.zendesk.com/hc/en-us/article_attachments/202124442/Screen_Shot_2015-10-13_at_11.56.10_AM.png)

<br/><br/>

Below you can see an example of the init function. Remember to set your API key for each platform prior calling init:

```

private string appDeveloperKey;
	
private Position pollfishPosition = Position.MIDDLE_LEFT;

private bool debugMode = true;
private bool customMode = false;
private int indPadding = 10;


public void onEnable()
{
  #if UNITY_ANDROID
  
  apiKey = "ANDROID_API_KEY";
  
  #elif UNITY_IPHONE
  
  apiKey = "IOS_API_KEY";
  
  #endif
  
  Pollfish.PollfishInitFunction((int) pollfishPosition, indPadding, apiKey, debugMode, customMode);

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

Add the following paragraph to your app's privacy policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone) is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*  

*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”*

<br/><br/>

---

### At this point you are ready to publish your app with Pollfish! 

> **Note:** Remember to turn your app in release mode prior publishing to a relevant app store

<br/><br/><br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>
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

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 7.2 to skip or shorten Pollfish Demographic surveys.

<br/>

### 7\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>
<br/>
<br/>

### 8\. Other init methods (optional)

#### 8.1 Passing custom parameter for server to server postback calls

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function and receive it back with Server to Server, survey completed postback call you can use:  

```
void PollfishInitWithRequestUUID(int position, int padding, string developerKey, bool debuggable, bool customMode, string request_uuid);

```
<br/>

#### 8.2 Passing user attributes to skip or shorten Pollfish Demographic surveys

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and also achieve a better fill rate and higher priced surveys.

| **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default


```
void PollfishInitWithUserAttributes(int position, int padding, string developerKey, bool debuggable, bool customMode, string request_uuid, Dictionary<string,string> attrDict);

```
for example:

```
// Send user demographic attributes to shorten or skip demographic surveys

Dictionary<string, string> dict = new Dictionary<string, string> ();

//used in demographic surveys
dict.Add ("gender", "1");
dict.Add ("year_of_birth", "1974");
dict.Add ("marital_status", "2");
dict.Add ("parental", "3");
dict.Add ("education", "1");
dict.Add ("employment", "1");
dict.Add ("career", "2");
dict.Add ("race", "3");
dict.Add ("income", "1");

//general user attributes
dict.Add ("email", "user_email@gmail.com");
dict.Add ("google_id", "USER_GOOGLE");
dict.Add ("linkedin_id", "USER_LINKEDIN");
dict.Add ("twitter_id", "USER_TWITTER");
dict.Add ("facebook_id", "USER_FB");
dict.Add ("phone", "USER_PHONE");
dict.Add ("name", "USER_NAME");
dict.Add ("surname", "USER_SURNAME");

Pollfish.PollfishInitFunction ((int)pollfishPosition, indPadding, apiKey, debugMode, customMode, requestUUID,dict);

```
You can check values mapping for demographic surveys in the following [section](https://www.pollfish.com/docs/demographic-surveys)
