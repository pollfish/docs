<div class="changelog changelog-4.1.0">
v4.1.0

- Support of manual set of devMode for android by ignoring key of signing
- Respect and submit of Google Advertising Id
v4.0.0

- Initial Release
- Support for Lollipop
</div>

**Obtain a Developer Account and download Pollfish Unity Plugin**

Register at [www.pollfish.com](//www.pollfish.com) and download Pollfish Unity Plugin.

**Add app (one for iOS and one for Android) in Pollfish panel and copy the given API Keys**

Login at [www.pollfish.com](//www.pollfish.com) and add two new apps (iOS and Android if you support both platforms) at Pollfish panel in section My Apps and copy the given API key for each app to use later in your init function in Unity.

## Initial Setup

In Pollfish Unity plugin zip file you will find a unitypackage file for easy import of plugin’s necessary files.

### To import Pollfish unity package:

*   Open your Unity project and right click on your Assets folder in your Project area or select Assets from the menu and then choose Import Package, then Custom Package and finally select PollfishUnityPugin. unitypackage.  

    ![](/img/documentation/unity/unity1.png)
*   If you want to exlude demo scene please uncheck Assets/Plugins/Pollfish/demo folder. Have in mind that in demo folder you will find PollfishDemo.cs file that demonstrates Pollfish Unity Plugin usage within a scene.
*   Review the package files and then select Import. If you are targeting only Android platform for example you can uncheck the iOS folder and vice versa.

### Imported Files will be listed in the following directories:

**Assets/Editor** – Files to help with initial setup

![](/img/documentation/unity/unity2.png)

#### iOS

*mod_pbproj,pyc, PostprocessBuildPlayer and PostprocessBuildPlayer_Pollfish are used to automatically add Pollfish necessary frameworks in your XCode project (frameworks will show up in red color in your XCode project, ignore that and build). If you do not want to have to link each time the necessary frameworks in your XCode project then you should leave the files as it is in Editor folder, otherwise you can deselect them.

![](/img/documentation/unity/unity3.png)

Be careful to replace your previous project when you build for iOS otherwise frameworks will be added more than once if you choose to append.

#### Android

*PollfishAndroidSetupUI.cs is a script file that allows to automatically add Google Play Services in your Android project from Unity menu.

Please have in mind that in order to use Pollfish you have to include Google Play Services in your Unity project. You can do that easily do that by selecting File and then Pollfish – Setup Android dependencies. If you do not have Google Play Services you can install them through Android SDK Manager.

**Assets/Plugins/Android** – Android Pollfish libraries and resources

**Assets/Plugins/iOS** – Pollfish framework and bridge files.

**Assets/Plugins/Pollfish** – Pollfish C# bridge files that allow communication between Unity and Java for Android and Unity and Objective-C for iOS.

**Assets/Plugins/Pollfish/demo** – A simple scene that demonstrates Pollfish plugin integration

### Requirements

Have in mind that Pollfish works with Unity 4.3+ and :

*   iOS 6.0 +
*   Android 2.3.3 (10) +

Please set minimum versions of your project accordingly.

### Sample Project

In order to have a look on a simple integration of Pollfish in a unity project have a look in Assets/Plugins/Pollfish/demo folder. You can run the scene there and see how Pollfish will be rendered through your apps.

![](/img/documentation/unity/unity4.png)

However we suggest that you follow this tutorial in order to understand better the integration steps you have to follow to properly use Pollfish in your project.

### Initializing Pollfish

You should use a MonoBehaviour object for your scene that will enable interaction with Pollfish plugin. (See example PollfishBinding.cs in Assets/Plugins/Pollfish folder)

Set your API key for each platform prior calling init:

```
public void onEnable()
{
  #if UNITY_ANDROID
  
  appDeveloperKey = "ANDROID_API_KEY";
  
  #elif UNITY_IPHONE
  
  appDeveloperKey = "IOS_API_KEY";
  
  #endif
  
  Pollfish.PollfishInitFunction ((int)pollfishPosition, padding, appDeveloperKey, debugMode, customMode);
}
```

You should initialize Pollfish when apps starts or resumes.

```
Pollfish.PollfishInitFunction ((int)pollfishPosition, padding, appDeveloperKey, debugMode, customMode);
```

Pollfish init function takes the following parameters:

*   **string appDeveloperKey** – your app developer key (iOS and Android)
*   **Position pollfishPosition** - The Position where you wish to place the Pollfish indicator. There are six different options {Position.TOP_LEFT, Position.BOTTOM_LEFT, Position.MIDDLE_LEFT, Position.TOP_RIGHT, Position.BOTTOM_RIGHT, Position.MIDDLE_RIGHT}
*   **bool debugMode** – Debug or Release mode

    You can use Pollfish either in Debug or in Release mode.

    -Debug/Developer mode is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).

    -Release mode is the mode to be used for a released app in AppStore or Google Play (start receiving paid surveys).

*   **bool customMode** – use Pollfish in custom mode.

    customMode false or true.

    customMode false is the standard way of using Pollfish in your apps. Using customMode false enables controlling the behavior of Pollfish in an app from Pollfish panel. customMode true function ignores Pollfish behavior from Pollfish web panel. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish view to app users. customMode true is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates.

*   **int padding** - The padding from top or bottom according to Position of the indicator specified before (0 is the default value – |*if used in MIDDLE position, padding is calculating from top).

### App Lifecycle handling (optional)

To init Pollfish when app resumes you can call:

```
void OnApplicationPause (bool pause)
{
  if (pause) {
    // we are in background
    ispaused = true;
  } else {
    // we are in foreground again.
    ispaused=false;                        

    #if UNITY_IPHONE 
            
    /* you can use this on Android too, but test since low end devices may freeze */
    Pollfish.PollfishInitFunction ((int)pollfishPosition, padding, appDeveloperKey, debugMode, customMode);

    #endif            
  
  }
}
```

*Calling Pollfish init on other times on Android may cause UI freezing on low end devices.

### Manually call show and hide (optional)

You can manually show or hide Pollfish by calling anywhere after initialization of Pollfish:

```
Pollfish.ShowPollfish ();
```

Or

```
Pollfish.HidePollfish ();
```


### Listening to Pollfish events (optional)

If you want to register to listen for Pollfish events you can add PollfishEventListener.cs to your scene object and listen for the relevant functions to fire. If you want to listen only to specific listeners choose from them and add them to your MonoBehaviour object in a similar way as in PollfishEventListener.cs

Generally, in order to listen to Pollfish events you have to explicitly listen for them:

```
public void OnEnable()
{
  Pollfish.surveyCompletedEvent += surveyCompleted;
  Pollfish.surveyOpenedEvent += surveyOpened;
  Pollfish.surveyClosedEvent += surveyClosed;
  Pollfish.surveyReceivedEvent += surveyReceived;
  Pollfish.surveyNotAvailableEvent += surveyNotAvailable;
  Pollfish.userNotEligibleEvent += userNotEligible;
        
  #if UNITY_ANDROID

  /* events for back button android */

  Pollfish.shouldQuitEvent += shouldQuit;
  Pollfish.shouldNotQuitEvent += shouldNotQuit;

  #endif
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
        
  #if UNITY_ANDROID

  /* events for back button android */

  Pollfish.shouldQuitEvent -= shouldQuit;
  Pollfish.shouldNotQuitEvent -= shouldNotQuit;

  #endif
}
```

On the left side you can see the event you are registering with, and on the right side the function that will be fired when the event occurs.

In order to inform Android and iOS to which object to send the unity messages when an event happens we have to add the following code in Awake function:

```
void Awake()
{
  // Tell plugin which gameobject to send messages too

  Pollfish.SetEventObjectPollfish(this.gameObject.name);
}
```

### Android Back Event

Since Pollfish uses Android back button to close its panel if open, if you want to replicate this behavior you should capture the back button event and call Pollfish.ShouldQuit (); to inform the library and act accordingly.

```
public void Update ()
{        
    /* handling Android back event */    
  if (Input.GetKeyDown (KeyCode.Escape)) {
                
    Pollfish.ShouldQuit ();
    
  }
}
```

This function will fire any of the following listeners that you should prior register in order to listen for the following events in the same way as described before:

```
#if UNITY_ANDROID

public void shouldQuit()
{
  Debug.Log("PollfishEventListener: shouldQuit()");

  Application.Quit ();

}

public void shouldNotQuit()
{
  Debug.Log("PollfishEventListener: shouldNotQuit()");
}

#endif
```

shouldNotQuit() listener informs you that Pollfish has handled the Pollfish back event (Pollfish panel was open and the event closed it) and you should not quit the app or take any other action upon it.

### Android AndroidManifest file

We have included an AndroidManifest.xml file that will work for most of user cases However if you need to include your own AndroidManifest file remember to add the following lines:

```
<meta-data android:name="com.google.android.gms.version"
  android:value="@integer/google_play_services_version" />
```

that are required by Google Play Services within the <application> tags and also to add the following line

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

### Pausing and Resuming a scene when user takes a survey (optional)

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

### Set custom user attributes (optional)

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

### Android Obfuscation (Using Proguard when exporting)

If you use proguard with your app, please insert the following line in your proguard configuration file:

```
-libraryjars libs/pollfish.jar
-libraryjars libs/pollfish_unity_android_bridge.jar

-keep class com.pollfish.** { *; }
-keep class com.pollfish_unity.** { *; }
```

where pollfish.jar is the latest pollfish jar you use in your app and pollfish_unity_android_bridge.jar is the bridge jar between Pollfish and Unit that are placed in your Assets folder.

**Note:**

**- Using Proguard with Pollfish requires setting your Project Build Target to Android 4.2.2 (API 17) or above!**

**- Include all Google Play services necessary code as described [here](http://developer.android.com/google/play-services/setup.html#Proguard).**

