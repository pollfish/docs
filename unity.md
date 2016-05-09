<div class="changelog" data-version="4.2.0">
v4.2.0

- New updated iOS and Android SDKs
- Added video, rating, slider, open ended, open ended numerical and description questions support
- Improved performance, bug fixes

v4.1.0

- Support of manual set of devMode for android by ignoring key of signing
- Respect and submit of Google Advertising Id

v4.0.0

- Initial Release
- Support for Lollipop
</div>
<br/><br/>

## Steps Analytically

### 1. Obtain a Developer Account

Register at [www.pollfish.com](//www.pollfish.com/login/publisher)
<br/>
### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click **"Add a new app"** on Pollfish Developer Dashboard in section **"My Apps"**. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

> **Note:** If your app supports both Android and iOS it would be better to create 2 different apps on the dashboard and use different API keys for each platform in your Unity code
<br/>
### 3\. Import Pollfish in your project

Download Pollfish Unity Plugin from the website. In Pollfish Unity Plugin zip file you will find a unitypackage file. You can use this file to easily import plugin’s necessary files.

### Import Pollfish unity package

*   Open your Unity project and right click on your Assets folder in your Project area or select Assets from the menu and then choose **Import Package**, then **Custom Package** and finally select **PollfishUnityPugin.unitypackage**

    ![](/homeassets/images/documentation/unity/unity1.png)
*   If you want to exlude demo scene please uncheck **Assets/Plugins/Pollfish/demo** folder. Have in mind that in demo folder you will find **PollfishDemo.cs file** that demonstrates Pollfish Unity Plugin usage within a scene.
*   Review the package files and then select Import. If you are targeting only Android platform for example you can uncheck the iOS folder and vice versa.

### Check/uncheck files to be imported

Imported Files will be listed in the following directories:

**Assets/Editor** – Files to help with initial setup

![](https://storage.googleapis.com/pollfish-images/PollfishUnityPlugin.png)

### If you target iOS ![alt text](https://storage.googleapis.com/pollfish-images/ios-icon.png)

* **mod_pbproj.pyc, PostprocessBuildPlayer and PostprocessBuildPlayer_Pollfish and PollfishBuildPostprocessor.cs** are used to automatically add Pollfish necessary frameworks in your XCode project (if frameworks  show up in red color in your XCode project, ignore that and build). If you do not want to have to link each time the necessary frameworks in your XCode project you can deselect them during importing.

> **Note:** Be careful to replace your previous project when you build for iOS otherwise frameworks will be added more than once if you choose to append.

### If you target Android ![alt text](https://storage.googleapis.com/pollfish-images/android-icon.png)


* **PollfishAndroidSetupUI.cs** is a script file that allows to automatically add Google Play Services in your Android project from Unity menu.

> **Note:** Please have in mind that in order to use Pollfish you have to include Google Play Services in your Unity project. You can do that easily do that by selecting **File** and then **Pollfish – Setup Android dependencies**. If you do not have Google Play Services you can install them through Android SDK Manager.

![alt text](https://storage.googleapis.com/pollfish-images/android_dep.png)

**Assets/Plugins/Android** – Android Pollfish libraries and resources

**Assets/Plugins/iOS** – Pollfish framework and bridge files.

**Assets/Plugins/Pollfish** – Pollfish C# bridge files that allow communication between Unity and Java for Android and Unity and Objective-C for iOS.

**Assets/Plugins/Pollfish/demo** – A simple scene that demonstrates Pollfish plugin integration
<br/><br/><br/>


#### **Requirements**

Have in mind that Pollfish works with Unity 4.3+ and :

*   iOS 7.0 +
*   Android 2.3.3 (10) +

Please set minimum versions of your project accordingly.

> **Note:** Pollfish does not work on Editor
<br/><br/><br/>


### 4. Initializing Pollfish

You should use a MonoBehaviour object for your scene that will enable interaction with Pollfish Unity plugin. Pollfish should be initialized when an app starts or resumes.

```
void PollfishInitFunction(int pollfishPosition, int indPadding, string apiKey, bool debugMode, bool customMode);
```

### Pollfish init function takes the following parameters:

**1\. pollfishPosition** (PollfishPosition) - Sets Position where you wish to place  Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish-images/indicator.png)

<span style="text-decoration: underline">There are six different options available: </span> 

*   **Position.TOP_LEFT**  
*   **Position.TOP_RIGHT**  
*   **Position.BOTTOM_LEFT**  
*   **Position.BOTTOM_RIGHT**  
*   **Position.MIDDLE_LEFT** 
*   **Position.MIDDLE_RIGHT**  

**2\. indPadding** (int) - The padding from top or bottom of the screen according to PollfishPosition of the indicator (small red rectangle) specified before (0 is the default value)  

> **Note:** if used in MIDDLE position, padding is calculating from top.**  

**3\. apiKey** (NSString *)- Your API Key. This is the key that allows you to use Pollfish in your app. You can find it on Pollfish website after your registration, when you create an app in “My apps” section in the panel.  

**4\. debugMode (BOOL)** – Debug or Release mode  

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).  
*   **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

> **Note:** Be careful to set andDebuggable parameter to false prior releasing to AppStore!  

5\. **customMode** (BOOL) – Initializes Pollfish in custom mode if set to true. By default this is set to false.

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
  
  Pollfish.PollfishInitFunction((int) pollfishPosition, indPadding, apiKey, bool debugMode, bool customMode);

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

Also Pollfish requires Internet permission so please do not forget to add the following line if you do not already have it.

```
<uses-permission android:name="android.permission.INTERNET"/>
```


### Using Proguard

If you use proguard with your app, please insert the following line in your proguard configuration file:

```
-libraryjars libs/pollfish_unity_android_bridge.jar

-keep class com.pollfish.** { *; }
-keep class com.pollfish_unity.** { *; }
-dontwarn com.pollfish.**
```

where **pollfish_unity_android_bridge.jar** is the bridge jar between Pollfish and Unity that are placed in your Assets folder.

**Note:**

**- Using Proguard with Pollfish requires setting your Project Build Target to Android 4.2.2 (API 17) or above!**

**- Include all Google Play services necessary code as described [here](http://developer.android.com/google/play-services/setup.html#Proguard).**
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
<br/>
<img style="margin: 0 auto; display: block;" src="https://pollfish.files.wordpress.com/2016/03/basic_survey.gif"/>
<br/>

If you have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>
<br/><br/><br/><br/>

## Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys. All these steps are optional.
<br/>
<br/>
### 7\. Other init methods (optional)

#### Passing custom parameter for server to server postback calls

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function within the plugin and receive it back with Server to Server, survey completed postback call you can use:  

```
void PollfishInitFunction(int pollfishPosition, int indPadding, string apiKey, bool debugMode, bool customMode, string request_uuid);
```

<br/>
### 8. Adjusting Pollfish with app lifecycle events (optional)

It would be a good practise to init Pollfish when app resumes in order to check if a new survey is available for the user.

```
void OnApplicationPause (bool pause)
{
  if (pause) {
    // we are in background
    ispaused = true;
  } else {
    // we are in foreground again.
    ispaused=false;                        
       
    /* you can use this on Android too, but test since low end devices may freeze */
    Pollfish.PollfishInitFunction ((int)pollfishPosition, indPadding, apiKey, debugMode, customMode);
  }
}
```
<br/>
### 9\. Manually show or hide Pollfish (optional)

You can manually show or hide Pollfish anytime, by calling anywhere after initialization:  

```
Pollfish.ShowPollfish ();
```

Or

```
Pollfish.HidePollfish ();
```
<br/>

### 10. Listening to Pollfish events (optional)

If you want to register to listen for Pollfish events you can add **PollfishEventListener.cs** to your scene object and listen for the relevant functions to fire. If you want to listen only to specific listeners choose from them and add them to your MonoBehaviour object in a similar way as in PollfishEventListener.cs

Generally, in order to listen to Pollfish events you have to explicitly listen for them:

```
/* register to listen to Pollfish events */

public void OnEnable()
{
  Pollfish.surveyCompletedEvent += surveyCompleted;
  Pollfish.surveyOpenedEvent += surveyOpened;
  Pollfish.surveyClosedEvent += surveyClosed;
  Pollfish.surveyReceivedEvent += surveyReceived;
  Pollfish.surveyNotAvailableEvent += surveyNotAvailable;
  Pollfish.userNotEligibleEvent += userNotEligible;
}

/* unregister from Pollfish events */

public void OnDisable()
{
  Pollfish.surveyCompletedEvent -= surveyCompleted;
  Pollfish.surveyOpenedEvent -= surveyOpened;
  Pollfish.surveyClosedEvent -= surveyClosed;
  Pollfish.surveyReceivedEvent -= surveyReceived;
  Pollfish.surveyNotAvailableEvent -= surveyNotAvailable;
  Pollfish.userNotEligibleEvent -= userNotEligible;
    
  #endif
}
```

On the left side you can see the event you are registering to listen to, and on the right side the function that will be fired when the event occurs.

In order to inform Android and iOS to which object to send the unity messages when an event happens we have to add the following code in Awake function:

```
void Awake()
{
  // Tell plugin which gameobject to send messages too

  Pollfish.SetEventObjectPollfish(this.gameObject.name);
}
```
<br/>
### 11. Pausing and Resuming a scene when user takes a survey (optional)

It is good practice to pause your scene when a user is taking a survey and resume when he is done. To do this we pause our scene when Pollfish panel opens and we resume when Pollfish panel closes.

```
private bool ispaused = false ; 

public void Update () {
    
  if (!ispaused) {
    Time.timeScale = 1;

  } else if (ispaused) {
    Time.timeScale = 0;        
  }
}    

public void surveyOpened()
{
  ispaused = true; // pause scene 
}
    
public void surveyClosed()
{
  ispaused = false; // resume scene 
}
```
<br/>
### 12. Set custom user attributes (optional)

You can set custom attributes that you receive from your app regarding a user in order to receive a better fill rate on surveys by calling the following:  

```
Pollfish.SetAttributesPollfish(Dictionary<string,string> dict);
```

For example:

```
Dictionary<string, string> dict = new Dictionary<string, string>();
 
dict.Add("FacebookID", "1234");
dict.Add("TwitterID", "10sde");
 
Pollfish.SetAttributesPollfish(dict);
```

<br/>
### 13\. Check if Pollfish survey is still available on your device (optional)

It happens that time had past since you initialized Pollfish and a survey is received. If you want to check is survey is still avaialble on your device and has not expired you can check by calling:

```
Pollfish.IsPollfishPresent();
```



<br/><br/><br/>


### Sample Project

In order to have a look on a simple integration of Pollfish in a unity project have a look in **Assets/Plugins/Pollfish/demo** folder. You can run the scene there and see how Pollfish will be rendered through your apps.

![](/homeassets/images/documentation/unity/unity4.png)

In sample project you can see both standard and rewarded integration from Pollfish in case you want to use Pollfish for rewarding users with some sort of virtual currency. However we suggest that you follow this tutorial in order to understand better the integration steps you have to follow to properly use Pollfish in your project.







