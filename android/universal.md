<div class="changelog changelog-4.1.0">
v4.1.0

- added new init function with developer mode param
- added track and respect of Google Advertising Id
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
**This SDK should be used for distribution in the Google Play Store.**

## Quick Guide of Universal SDK

1. Download Pollfish jar or aar file and add to your project
2. Import Pollfish classes
3. Add permissions to AndroidManifest.xml
4. Call the init function to activate Pollfish
5. Set to Release mode and release in Store
6. Update your privacy policy

Pollfish Android SDK works with Android 10 (2.3.3) and above.  

Read the Handle Orientations section below, to handle the orientations in your app properly.  

**Note: Be careful to turn the debuggable parameter in AndroidManifest.xml to false when you release your app in the relevant store! (or just delete it)**  

### Developer Vs Release Mode

You can use Pollfish either in Developer or in Release mode.  

*   Developer mode is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
*   Release mode is the mode to be used for a released app in any app store(start receiving paid surveys).

If you **do not set the debuggable parameter** in your AndroidManifest.xml file Pollfish runs in developer mode by default. It will turn to Release mode automatically when you sign your apk with a release key.  

If you use the debuggable parameter in your AndroidManifest.xml  

```xml
<application android:debuggable="true" android:label="@string/app_name"> 
```

then you can set the different modes.  

<span class="debuggable">android:debuggable</span>

*   true: Debug mode
*   false: Release mode

**Note: Be carefull to turn the debuggable parameter to false when you release your app in the relevant store!!**  

## Steps Analytically

### 1\. Obtain a Developer Account and download Pollfish SDK

Register at [www.pollfish.com](//www.pollfish.com) and download Pollfish Android SDK.

### 2\. Add new app in Pollfish panel and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com) and add a new app at Pollfish panel in section My Apps and copy the given API key for this app to use later in your init function in your app.

## Integrate Google Play services (optional)

### 3\. Add Google Play services to your project (optional)

Applications that integrate Pollfish SDK can optionally include the Google Play services library when possible, to achieve better targeting. Further details regarding integration with the Google Play services library can be found [here](//developer.android.com/google/play-services/setup.html).  

*** Be careful - Pollfish does not work with Google Play services for Froyo**

## Integrate Pollfish SDK

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
    compile project(':pollfish')
}
```

b) or retrieve Pollfish through jcenter() with gradle by adding the following line in your project build.gradle (not the top level one, the one under 'app') add the following (in the dependencies section):  

```
dependencies {
  compile 'com.pollfish:pollfish:4.1.0:universalRelease@aar'
}
```

### 5. Import Pollfish classes

Import Pollfish classes with the following lines at the top of your Activity’s class file:

```java
import com.pollfish.main.PollFish;
import com.pollfish.constants.Position;
```

### 6\. Add permissions to AndroidManifest.xml

You should also add the following lines in your AndroidManifest.xml  

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```

Pollfish uses these permissions to track and send the survey responses.  

## Initialize Pollfish

### init Vs customInit

*   init function is the standard way of using Pollfish in your apps. Using init function enables controlling the behavior of Pollfish in an app from Pollfish panel.
*   customInit function ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates. Both init and customInit functions have the same arguments.

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

**Note: If your app calls setContentView() function more than once in your Activity lifecycle you should call Pollfish.init() or Pollfish.customInit() respectively just after each setContentView to use Pollfish properly.**  

#### Both init and customInit functions take the following parameters:

1.  <span class="params">act:</span> - The current activity where the Pollfish is initialized
2.  <span class="params">YOUR_API_KEY:</span> - Your API Key (from step 2)
3.  <span class="params">pos:</span> - The Position where you wish to place the Pollfish indicator. There are four different options {Position.TOP_LEFT, Position.BOTTOM_LEFT, Position.MIDDLE_LEFT, Position.TOP_RIGHT, Position.BOTTOM_RIGHT, Position.MIDDLE_RIGHT}
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

**7.1 Use Pollfish listeners without the need of implementing them in the Activity**

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

**7.2 Passing user view layout in the init function**

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
**7.3 Passing custom parameter for server to server postback calls**

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function within the SDK and receive it back with Server to Server, survey completed postback call you can use:

```
PollFish.init(Activity act, String YOUR_API_KEY, Position pos, int padding, String request_uuid);
```

## Update your Privacy Policy

### 8\. Add the following paragraph to your app's privacy policy

“Survey Serving Technology  

This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone) is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.  

APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”

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
-libraryjars libs/pollfish.jar // not necessary if you are using Android Studio or .aar library
-keep class com.pollfish.** { *; }
```

where pollfish.jar is the latest pollfish jar you use in your app and is placed in your libs folder.  

**Note:  

- Using Proguard with Pollfish requires setting your Project Build Target to Android 5.0 (API 21)!  
- Include all Google Play services necessary Proguard code as described [here](//developer.android.com/google/play-services/setup.html#Proguard) (if you use them in your project).**  

If you do not include Google Play services in your project, add the following code in your Proguard file:  


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

