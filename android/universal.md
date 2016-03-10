<div class="changelog" data-version="4.2.0">
v4.2.0

- new init function structure
- new builder pattern approach on init function
- added support for beacon surveys
- added video, rating, slider, open ended, open ended numerical and description questions support
- deprecated old init methods
- improved performance, bug fixes

v4.1.0

- added new init function with developer mode param
- added track and respect of Google Advertising Id
- 
v4.0.3

- added UserProperties object for passing attributes around user.
- added init function with option to pass user view layout as param
- added init function with option to pass a custom param and receive it on server-to-server callback
- Added various bug fixes and optimizations

v4.0.2

- When called manually, show/hide Pollfish on main UI thread
- fixed bugs on layout resize on orientation changes when android:configChanges="screenSize"
- Added various bug fixes and optimizations

v4.0.1

- Added various bug fixes and optimizations

v4.0.0

- Fixed issue with support for Gingerbread 2.3
- Support for Lollipop

</div>

> **Note:** Do not use this SDK for distribution on Google Play Store!

## Quick Guide of Universal SDK

1. Download Pollfish jar or aar file and import to your project
2. Import Pollfish classes
3. Add permissions to AndroidManifest.xml
4. Call init function to activate Pollfish
5. Set to **Release mode** and release in any app store
6. Update your privacy policy

Pollfish Android SDK works with Android 10 (2.3.3) and above.  

<br/><br/><br/><br/>
## Steps Analytically

### 1. Obtain a Developer Account and download Pollfish SDK

Register at [www.pollfish.com](//www.pollfish.com/login/publisher) and download Pollfish Android SDK.

### 2. Add new app in Pollfish panel and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and add a new app at Pollfish panel in section My Apps and copy the given API key for this app to use later in your init function in your app.

### 3. Integrate Google Play Services to your project

Applications that integrate Pollfish SDK are required to include the Google Play services library. Further details regarding integration with the Google Play services library can be found [here](//developer.android.com/google/play-services/setup.html).

Pollfish SDK uses only a subset of Google Play Services library so if you want you can only include this subset in your project. 

If you are using Google Play Services 8.3.* and less you can use:

```java
dependencies {
	 compile 'com.google.android.gms:play-services-ads:8.3.0'
}
```
otherwise since Google Play Services 8.4.* you can use only Google Play Services Base Client library. For example:

```java
dependencies {
	 compile 'com.google.android.gms:play-services-base:8.4.0'
}
```

### 4\. Add Pollfish jar or aar library to your project

**+jar: +**  

Add Pollfish jar to your project libraries  

or  

**+aar:+**  

Add Pollfish .aar file to your project.  

If you are using Android Studio  

a) right click on your project add select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate pollfish.aar file.  

Then in your project build.gradle (not the top level one, the one under 'app') add the following (in the dependencies section):  

```java
dependencies {
    compile project(':pollfish-universal-4.2.0')
}
```

b) or retrieve Pollfish through **jcenter()** with gradle by adding the following line in your project build.gradle (not the top level one, the one under 'app') add the following (in the dependencies section):  

```
dependencies {
  compile 'com.pollfish:pollfish:4.1.0:universalRelease@aar'
}
```

### 5. Import Pollfish classes

Import Pollfish classes with the following lines at the top of your Activity’s class file:

```java
import com.pollfish.main.PollFish;
import com.pollfish.main.PollFish.ParamsBuilder;
import com.pollfish.constants.Position;
```

### 6. Add permissions to AndroidManifest.xml

You should also add the following lines in your AndroidManifest.xml  

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```

Pollfish uses these permissions to track and send the survey responses.  

### 7. Initialize Pollfish

After you link your project to Google Play Services you can easily initialize Pollfish. In order to initialize you will need to create an instance of ParamsBuilder. ParamsBuilder has only one mandatory parameter which is the API key of your app (step 2 above). In section 7.1 we will see several other params that we can pass to ParamsBuilder instance in order to configure Pollfish behaviour during initialization.


```java
ParamsBuilder paramsBuilder = new ParamsBuilder(String "YOUR_API_KEY").build();
```
Once you created ParamsBuilder instance then you can call Pollfish initWith() in **onResume()** function of your Activity ( just after super.onResume() ) and you are ready to go.

```java
PollFish.initWith(Activity activity, ParamsBuilder paramsBuilder);
```

Below you can see an example:

```java
@Override
public void onResume() {
    super.onResume();
 
    PollFish.initWith(this, new ParamsBuilder("YOUR_API_KEY").build());
}
```


**Note: If your app calls setContentView() function more than once in your Activity lifecycle you should call Pollfish.init() or Pollfish.customInit() respectively just after each setContentView to use Pollfish properly.**  
<br/>

### 8\.  Update your Privacy Policy

Add the following paragraph to your app's privacy policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone) is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*  

*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”*

<br/><br/>

> **You are ready to go live! Sign your app with a release key and publish to any app store**

---

<br/><br/><br/><br/>

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys.


#### 9. ParamsBuilder available options (optional)

As we have seen in previous section ParamsBuilder instance requires only one mandatory param, the API key of the app. 

```java
ParamsBuilder paramsBuilder = new ParamsBuilder(String "YOUR_API_KEY").build();
```

However we can set several other params to control the behaviour of Pollfish surveys within your app or register to several notifications.
<br/>
Below you can see all the available options of ParamsBuilder instance"
<br/>

No | Description
------------ | -------------
9.1 | **.indicatorPosition(int position)**  <br/> Sets the Position where you wish to place the Pollfish indicator (small red rectangle).
9.2 | **.requestUUID(String requestUUID)**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
9.3 | **.indicatorPadding(int padding)**  <br/> Sets padding (in dp) from top or bottom according to Position of the indicator
9.4 | **.userLayout(ViewGroup userLayout)**  <br/> Sets User View layout that Pollfish surveys will be rendered above it
9.5 | **.releaseMode(boolean releaseMode)**  <br/> Sets Pollfish SDK to Developer or Release mode
9.6 | **.customMode(boolean customMode)**  <br/> Initializes Pollfish in custom mode
9.7 | **.pollfishSurveyReceivedListener(PollfishSurveyReceivedListener pollfishSurveyReceivedListener)**  <br/> Sets a notification listener when Pollfish Survey is received
8 | **.pollfishSurveyNotAvailableListener(PollfishSurveyNotAvailableListener pollfishSurveyNotAvailableListener)**  <br/> Sets a notification listener when Pollfish Survey is not available
9.8 | **.pollfishSurveyCompletedListener(PollfishSurveyCompletedListener pollfishSurveyCompletedListener)**  <br/> Sets a notification listener when Pollfish Survey is completed
9.10 | **.pollfishUserNotEligibleListener(PollfishUserNotEligibleListener pollfishUserNotEligibleListener)**  <br/> Sets a notification listener when a user is not eligible for a Pollfish survey
9.11 | **.pollfishOpenedListener(PollfishOpenedListener pollfishOpenedListener)**  <br/> Sets a notification listener when Pollfish Survey panel is opened
9.12 | **.pollfishClosedListener(PollfishClosedListener pollfishClosedListener)**  <br/> Sets a notification listener when Pollfish Survey panel is closed

<br/>
<br/>
#### 9.1 .indicatorPosition(int position)
Sets Position where you wish to place  Pollfish indicator. There are six different options available: 

- Position.TOP_LEFT 
- Position.BOTTOM_LEFT
- Position.MIDDLE_LEFT
- Position.TOP_RIGHT
- Position.BOTTOM_RIGHT (default)
- Position.MIDDLE_RIGHT

If you do not set explicity a position for Pollfish indicator, it will appear by default at Position.BOTTOM_RIGHT
<br/>
Below you can see an example on how we can set Pollfish inticator to slide from top right corner of the screen:

```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.indicatorPosition(Position.TOP_RIGHT)
					.build();
```

<br/>
#### 9.2 .requestUUID(String requestUUID)

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object.

![alt text](https://pollfish.zendesk.com/hc/en-us/article_attachments/201860351/Screen_Shot_2015-08-19_at_1.30.21_PM.png)
<br/>
Here is an example of setting a requestUUID:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.requestUUID("YOUR_UUID")
					.build();
```

#### 9.3 .indicatorPadding(int padding)

Sets padding (in dp) of Pollfish indicator, from top or bottom according to Position of the indicator as specified before 
Default value is 5. If Position of Pollfish indicator is MIDDLE, padding is calculated from the top.
<br/>
Here is an example of setting a padding of Pollfish indicator to be 35dp from the top of the screen:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.indicatorPosition(Position.TOP_RIGHT)
					.indicatorPadding(35)
					.build();
```

#### 9.4 .userLayout(ViewGroup userLayout)

Sets user's View layout that Pollfish surveys will be rendered above it. If Pollfish regular init function affects the UI of your app by creating flings or any other issues you can try passing a view layout of your app that can be used to render above Pollfish 
<br/>
Here is an example of how a user can pass a view on his own through ParamsBuilder instance during initialization.
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.userLayout((ViewGroup) getWindow().getDecorView())
					.build();
```
#### 9.5 .releaseMode(boolean releaseMode)

Sets Pollfish SDK to Developer or Release mode
<br/><br/>
**Developer Vs Release Mode**

You can use Pollfish either in Developer or in Release mode.  

*   **Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store(start receiving paid surveys).

Pollfish runs in developer mode by default (when you sign your apk with a debug key). It will turn to Release mode automatically when you sign your apk with a release key.

However you can explicity request Pollfish SDK to run in release or developer mode by setting mode through ParamsBuilder instance during initialization.
<br/>

Below you can see an example on how you can turn your app in Release mode explicitly:

```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.releaseMode(true)
					.build();
```

#### 9.6 .customMode(boolean customMode)**  <br/> Initializes Pollfish in custom mode





### init Vs customInit

*   init function is the standard way of using Pollfish in your apps. Using init function enables controlling the behavior of Pollfish in an app from Pollfish panel.
*   customInit function ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates. 

Both init and customInit functions have the same arguments.

**Note: do not use both init and customInit in the same activity.**  

### 7\. Call init or customInit function to activate Pollfish

Add the init or customInit statement of Pollfish in the onResume() function of your activity (just after super.onResume()) and you are ready to go.  

```
PollFish.init(Activity act, String YOUR_API_KEY, Position pos, int padding);
```

or

```
PollFish.customInit(Activity act, String YOUR_API_KEY, Position pos, int padding);
```

The init or custom Init methods enable Pollfish surveys through your app.  


#### Both init and customInit functions take the following parameters:

1.  <span class="params">act:</span> - The current activity where the Pollfish is initialized
2.  <span class="params">YOUR_API_KEY:</span> - Your API Key (from step 2)
3.  <span class="params">pos:</span> - The Position where you wish to place the Pollfish indicator. There are six different options {Position.TOP_LEFT, Position.BOTTOM_LEFT, Position.MIDDLE_LEFT, Position.TOP_RIGHT, Position.BOTTOM_RIGHT, Position.MIDDLE_RIGHT}
4.  <span class="params">padding:</span> - The padding (in dp) from top or bottom according to Position of the indicator specified before (0 is the default value – |*if used in MIDDLE position, padding is calculating from top).

Below you can see an example of the init function:  

```
@Override
public void onResume() {
    super.onResume();
    PollFish.init(this, "your_api_key_here", Position.BOTTOM_LEFT, 5);
}
```

or

```
@Override
public void onResume() {
    super.onResume();
    PollFish.customInit(this, "your_api_key_here", Position.BOTTOM_LEFT, 5);
}
```

### Other init methods (optional)

**7.1 Init method with Pollfish listeners without the need of implementing them in the Activity**

You can use Pollfish alternative init and custom init functions that include Pollfish listeners within the initialization function.

```
PollFish.init(Activity act, String YOUR_API_KEY, Position p, int indPadding, 
  PollfishSurveyReceivedListener pollfishSurveyReceivedListener, 
  PollfishSurveyNotAvailableListener pollfishSurveyNotAvailableListener, 
  PollfishSurveyCompletedListener pollfishSurveyCompletedListener, 
  PollfishOpenedListener pollfishOpenedListener, 
  PollfishClosedListener pollfishClosedListener, 
  PollfishUserNotEligibleListener pollfishUserNotEligibleListener);
```

for example:

```
PollFish.init(this,"your_api_key", Position.BOTTOM_RIGHT, 5, 
  null, null ,new PollfishSurveyCompletedListener() {
  
    @Override
    public void onPollfishSurveyCompleted(boolean playfulSurvey, int surveyPrice) {
      
      Log.d("Pollfish", "Pollfish survey completed - Playful survey: " + playfulSurveys + " with price: " + surveyPrice);

    }
      
  },null,null,null,null)e
```

**7.2 Init method with option of passing user view layout in the init function**

If Pollfish regular init function affects your UI by creating flings or any other issues you can try passing your view's layout in the init function.

```
PollFish.init(Activity act, String YOUR_API_KEY, Position pos, int padding, ViewGroup userLayout);
```

for example:

```
@Override
public void onResume() {
    super.onResume();
    PollFish.init(this, "your_api_key_here", Position.BOTTOM_LEFT, 5, (ViewGroup) getWindow().getDecorView());
}
```
**7.3 Init method for passing custom parameter for server to server postback calls**

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function within the SDK and receive it back with Server to Server, survey completed postback call you can use:

```java
PollFish.init(Activity act, String YOUR_API_KEY, Position pos, int padding, ViewGroup userLayout, String request_uuid);
```
where userLayout is the view you would like ot show Pollfish as described in 7.2. You should pass null if you would like the SDK to handle it on its own.



## Handling orientation changes (optional)

### 9\. Handle Orientations

If your app supports both orientations and **your activities are recreated** on each orientation change **you should not do anything more**.  

If your app **does not recreate the activity** on change orientation  

e.g you may have in your manifest file, AndroidManifest.xml, the following lines if targeting prior Android 3.2:  

```
<activity android:name=".MyActivity" android:configChanges="keyboardHidden|orientation"> 
```

or beginning with Android 3.2

```
<activity android:name=".MyActivity" android:configChanges="keyboardHidden|orientation|screenSize">
```

If any of the above is true you should override the **onConfigurationChanged** method and initialize Pollfish again

```
@Override
public void onConfigurationChanged(Configuration newConfig) {

    super.onConfigurationChanged(newConfig);

    PollFish.init(this, "your_api_key_here", Position.BOTTOM_LEFT, 50);

}
```

## Implement Pollfish event listeners

### 10\. Get notified when a Pollfish survey is received (optional)

You can be notified when a Pollfish survey is received. Just import:  

```
import com.pollfish.interfaces.PollfishSurveyReceivedListener; 
```

and make your Activity implement PollfishSurveyReceivedListener, e.g 

```
public class MyActivity extends Activity implements PollfishSurveyReceivedListener
```

and Override the onPollfishSurveyReceived() function. You can also get informed about the type of survey (playful or not) that was received and its price shown in USD (estimated based on daily exchange currency).  

```
@Override
public void onPollfishSurveyReceived(boolean playfulSurveys, int surveyPrice) {

  Log.d("Pollfish", "Pollfish survey received - Playful survey: " + playfulSurveys + " with price: " + surveyPrice);

}
```

### 11\. Get notified when no Pollfish survey is available (optional)

You can be notified when no Pollfish survey is available. Just import:  

```
import com.pollfish.interfaces.PollfishSurveyNotAvailableListener;
```

and Override the onPollfishSurveyNotAvailable () function  

```
@Override
public void onPollfishSurveyNotAvailable() {
  Log.d("Pollfish", "Survey not available!");
}
```

### 12\. Get notified when Pollfish Survey is completed (optional)

You can be notified when a user completed a survey. Just import:  

```
import com.pollfish.interfaces.PollfishSurveyCompletedListener;
```

and make your Activity implement SurveyCompletedListener, e.g  

```
public class MyActivity extends Activity implements PollfishSurveyCompletedListener 
```

and Override the onPollfishSurveyCompleted() function. You can also get informed about the type of survey (playful or not) that was completed and its price shown in USD (estimated based on daily exchange currency).  

```
@Override
public void onPollfishSurveyCompleted(boolean playfulSurveys , int surveyPrice) {

  Log.d("Pollfish", "Pollfish survey completed - Playful survey: " + playfulSurveys + " with price: " + surveyPrice);

}
```

### 13\. Get notified when a user is not eligible for a Pollfish survey (optional)

You can be notified when a user is not eligible for a Pollfish survey after accepting to take it. Just import:  

```
import com.pollfish.interfaces.PollfishUserNotEligibleListener;
```

and make your Activity implement PollfishUserNotEligibleListener, e.g  

```
public class MyActivity extends Activity implements PollfishUserNotEligibleListener
```

and Override the onUserNotEligible() function 

```
@Override
public void onUserNotEligible() {
	Log.d("Pollfish", "onUserNotEligible()");

}
```

### 14\. Get notified when Pollfish Survey is opened (optional)

You can be notified when a Pollfish survey is opened. Just import:  

```
import com.pollfish.interfaces.PollfishOpenedListener; 
```

and make your Activity implement PollfishOpenedListener, e.g  

```
public class MyActivity extends Activity implements PollfishOpenedListener
```

and Override the onPollfishOpened() function  

```
@Override
public void onPollfishOpened () {

    Log.d("Pollfish", "Survey opened!");
}
```


### 15\. Get notified when Pollfish Survey is closed (optional)

You can be notified when a Pollfish survey is closed. Just import:  

```
import com.pollfish.interfaces.PollfishClosedListener;
```

and make your Activity implement PollfishClosedListener, e.g  

```
public class MyActivity extends Activity implements PollfishClosedListener
```

and Override the onPollfishClosed() function  

```
@Override
public void onPollfishClosed () {

    Log.d("Pollfish", "Survey closed!");
}
```

*** Usually used in game apps to resume the game**

## Other actions

### 16\. Manually show or hide Pollfish in an Activity (optional)

You can manually show or hide Pollfish indicator or panel by calling anywhere in your activity after the initialization line:  

```
PollFish.show();
```

or  

```
PollFish.hide();
```

### 17\. Proguard (optional)

If you use proguard with your app, please insert the following line in your proguard configuration file:  

```
-libraryjars libs/pollfish.jar // not necessary if using Android Studio or .aar library
-keep class com.pollfish.** { *; }
```

where pollfish.jar is the latest pollfish jar you use in your app and is placed in your libs folder.  

**Note:**  

**- Using Proguard with Pollfish requires setting your Project Build Target to Android 5.0 (API 21)!**  
**- Include all Google Play services necessary Proguard code as described [here](//developer.android.com/google/play-services/setup.html#Proguard) (if you use them in your project).**  

If you do not include Google Play services in your project, add the following code in your Proguard file:  

```
-keep class com.google.android.gms.** { *; }
-dontwarn com.google.android.gms.**
 
-keep class * extends java.util.ListResourceBundle {
    protected Object[][] getContents();
}
 
-keep public class com.google.android.gms.common.internal.safeparcel.SafeParcelable {
    public static final *** NULL;
}
 
-keepnames @com.google.android.gms.common.annotation.KeepName class *
-keepclassmembernames class * {
    @com.google.android.gms.common.annotation.KeepName *;
}
 
-keepnames class * implements android.os.Parcelable {
    public static final ** CREATOR;
}
```

### 18\. Highly targeted surveys (optional)

If you wish to receive highly targeted surveys in your app and increase your chances for a higher revenue you can include any or all of the following permissions in your AndroidManifest.xml file:  

```
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```


### 19\. Set user attributes (optional)

You can set attributes that you receive from your app regarding a user in order to receive a better fill rate and higher priced surveys.  

Just import:  

```
import com.pollfish.constants.UserProperties;
```

and set any of the attributes like below. Please remember to call this only after calling the init function.  

```
UserProperties userProperties = new UserProperties();

userProperties.setGender(Gender.MALE).setAge(Age._34).setMaritalStatus(MarritalStatus.SINGLE);
userProperties.setAgeGroup(AgeGroup._55_64);
userProperties.setFacebookId("facebookId");
userProperties.setTwitterId("twitterId");
userProperties.setCustomParams("PARAM_KEY","PARAM_VALUE");

PollFish.setAttributesMap(userProperties);
```

