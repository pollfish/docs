<div class="changelog" data-version="4.3.5">
v4.3.5
	
- added ability to test survey formats in debug mode

v4.3.4
	
- drastically decreased sdk footprint
- improved performance
- fixed crashing issues on open ended questions
- fixed memory leaks issue
- updated Pollfish indicators

v4.3.3

- added support for sending user attributes during init
- deprecated setCustomAttributes

v4.3.2

- bug fixes

v4.3.1

- improved support and optimizations for third-party survey providers
- fixed bug with google play services

v4.3.0

- added support for third-party survey providers

v4.2.1

- fixed shrinkResources bug

v4.2.0

- new init function structure
- new pattern approach on init function
- added support for beacon surveys
- added video, rating, slider, open ended, open ended numerical and description questions support
- deprecated old init methods
- improved performance, bug fixes

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

</br></br>
## Quick Guide of Google Play SDK

1. Register as a publisher at Pollfish, create an App and copy app's API key
2. Download Pollfish jar or aar file and import to your project
3. Import Google Play Services to your project
4. Import Pollfish classes
5. Add permissions to AndroidManifest.xml
6. Call Pollfish initialization function in onResume() of your Activity to activate Pollfish
7. Update your privacy policy
8. Set to **Release mode** and publish your app at any app store
9. Request your account to get verified from Pollfish Dashboard

> **Requirements:** Pollfish Android SDK works with Android 10 (2.3.3) and above.  

<br/><br/>
## Steps Analytically

### 1. Obtain a Developer Account

Register at [www.pollfish.com](//www.pollfish.com/login/publisher)

### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard in section "My Apps". Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

### 3. Integrate Google Play Services to your project

Applications that integrate Pollfish SDK are required to include  Google Play Services library. Further details regarding integration with the Google Play services library can be found [here](//developer.android.com/google/play-services/setup.html).

If you are using gradle you can easily add in your dependencies:

```java
dependencies {
	 compile 'com.google.android.gms:play-services:11.0.2'
}
```

Have in mind that Pollfish SDK uses only a subset of Google Play Services library so if you want you can only include this subset in your project. 

If you are using Google Play Services 8.3.* and less you can use:

```java
dependencies {
	 compile 'com.google.android.gms:play-services-ads:8.3.0'
}
```
otherwise since Google Play Services 8.4.* you can use only Google Play Services Base Client library. For example:

```java
dependencies {
	 compile 'com.google.android.gms:play-services-base:11.0.2'
}
```

> **Note:** If you cannot see surveys even in developer mode, please do check your logs to see if this is related your current version of Google Play Services  

</br>

### 4\. Add Pollfish jar or aar library to your project

Download Pollfish Android SDK or reference it through jCenter().

#### **Download Pollfish Android SDK**

Add Pollfish **.JAR** or **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project add select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate pollfish jar or aar file. Right click again on your project and in Module Dependencies tab choose to add pollfish module that you recently added, as a dependency.

**OR**

#### **Retrieve Pollfish Android SDK through jCenter()**

Retrieve Pollfish through **jCenter()** with gradle by adding the following line in your project build.gradle (not the top level one, the one under 'app') in  dependencies section:  

```
dependencies {
  compile 'com.pollfish:pollfish:+:googleplayRelease@aar'
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
```

Pollfish uses these permissions to track and send survey responses to Pollfish servers.  

### 7. Initialize Pollfish

After you link your project to Google Play Services you can easily initialize Pollfish. In order to initialize you will need to create an instance of ParamsBuilder. ParamsBuilder has only one mandatory parameter which is the API key of your app (step 2 above). 

| **Note:** In section 9 you can see several other optional params that you can pass to ParamsBuilder instance in order to configure Pollfish behaviour during initialization.


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


| **Note:** If your app calls setContentView() function more than once in your Activity lifecycle you should call Pollfish.init() or Pollfish.customInit() respectively just after each setContentView to use Pollfish properly.**  
<br/>

### 8\.  Update your Privacy Policy


Add the following paragraph to your app's privacy policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone) is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*  

*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”*

<br/>

| **Note:** It's important that you include this disclosure both in the privacy policy posted on Google Play but also in the privacy policy included in your app as described in [Google's Developer Privacy Policy](https://play.google.com/about/privacy-security/personal-sensitive/)  


<br/><br/>

**At this point you are ready to go live! Sign your app with a release key or explicitly set .releaseMode(true) - (section 9.5) in your ParamsBuilder and publish to any Android app store**

---
<br/>
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


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 9.13 - and skip or shorten this way, Pollfish Demographic surveys.



<br/>

### 9\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>

<br/>

<br/>

## Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys. All these steps are optional.


### 10. ParamsBuilder available options (optional)

As we have seen in section 7, ParamsBuilder instance requires only one mandatory param, the API key of the app that you acquired at step 2. 

```java
ParamsBuilder paramsBuilder = new ParamsBuilder(String "YOUR_API_KEY").build();
```

However you can set several other params to control the behaviour of Pollfish surveys within your app or register to several notifications.
<br/>
Below you can see all the available options of ParamsBuilder instance. All these functions can be called in any order consequently prior calling build() to ParamsBuilder instance.
<br/>

No | Description
------------ | -------------
10.1 | **.indicatorPosition(int position)**  <br/> Sets the Position where you wish to place the Pollfish indicator
10.2 | **.requestUUID(String requestUUID)**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
10.3 | **.indicatorPadding(int padding)**  <br/> Sets padding (in dp) from top or bottom according to Position of the indicator
10.4 | **.userLayout(ViewGroup userLayout)**  <br/> Sets User View layout that Pollfish surveys will be rendered above it
10.5 | **.releaseMode(boolean releaseMode)**  <br/> Sets Pollfish SDK to Developer or Release mode
10.6 | **.customMode(boolean customMode)**  <br/> Initializes Pollfish in custom mode
10.7 | **.pollfishSurveyReceivedListener(PollfishSurveyReceivedListener pollfishSurveyReceivedListener)**  <br/> Sets a notification listener when Pollfish Survey is received
10.8 | **.pollfishSurveyNotAvailableListener(PollfishSurveyNotAvailableListener pollfishSurveyNotAvailableListener)**  <br/> Sets a notification listener when Pollfish Survey is not available
10.9 | **.pollfishSurveyCompletedListener(PollfishSurveyCompletedListener pollfishSurveyCompletedListener)**  <br/> Sets a notification listener when Pollfish Survey is completed
10.10 | **.pollfishUserNotEligibleListener(PollfishUserNotEligibleListener pollfishUserNotEligibleListener)**  <br/> Sets a notification listener when a user is not eligible for a Pollfish survey
10.11 | **.pollfishOpenedListener(PollfishOpenedListener pollfishOpenedListener)**  <br/> Sets a notification listener when Pollfish Survey panel is opened
10.12 | **.pollfishClosedListener(PollfishClosedListener pollfishClosedListener)**  <br/> Sets a notification listener when Pollfish Survey panel is closed
10.13 | **.userProperties(UserProperties userProperties)**  <br/> Send user attributes to skip or shorten Pollfish demographic surveys
10.14 | **.surveyFormat(SurveyFormat surveyFormat)**  <br/> Requests a specific survey format (only in debug mode)
<br/>
#### **10.1 .indicatorPosition(int position)**
Sets Position where you wish to place  Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png)

There are six different options available: 

- Position.TOP_LEFT 
- Position.BOTTOM_LEFT
- Position.MIDDLE_LEFT
- Position.TOP_RIGHT
- Position.BOTTOM_RIGHT (default)
- Position.MIDDLE_RIGHT

If you do not set explicity a position for Pollfish indicator, it will appear by default at Position.BOTTOM_RIGHT
<br/><br/>
Below you can see an example on how you can set Pollfish indicator to slide from top right corner of the screen:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.indicatorPosition(Position.TOP_RIGHT)
					.build();
```
<br/>
#### **10.2 .requestUUID(String requestUUID)**

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

![alt text](https://pollfish.zendesk.com/hc/en-us/article_attachments/201860351/Screen_Shot_2015-08-19_at_1.30.21_PM.png)
<br/><br/>
Here is an example of setting a requestUUID:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.requestUUID("YOUR_UUID")
					.build();
```
<br/>
#### **10.3 .indicatorPadding(int padding)**

Sets padding (in dp) of Pollfish indicator, from top or bottom of the screen according to the specified Position of the indicator as described before in 10.1. Default value is 5. If Position of Pollfish indicator is MIDDLE, padding is calculated from the top of the middle of the screen.
<br/><br/>
Here is an example of setting padding of Pollfish indicator to be 35dp from the top of the screen:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.indicatorPosition(Position.TOP_RIGHT)
					.indicatorPadding(35)
					.build();
```
<br/>
#### **10.4 .userLayout(ViewGroup userLayout)**

Sets user's View layout that Pollfish surveys will be rendered above it. If Pollfish regular init function affects the UI of your app by creating flings or any other issues you can try passing a view layout of your app that can be used to render above Pollfish surveys
<br/><br/>
Here is an example of how a user can pass a view of his Activity through ParamsBuilder instance during initialization.
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.userLayout((ViewGroup) getWindow().getDecorView())
					.build();
```
<br/>
#### **10.5 .releaseMode(boolean releaseMode)**

Sets Pollfish SDK to Developer or Release mode
<br/><br/>
**Developer Vs Release Mode**

You can use Pollfish either in Developer or in Release mode.  

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish runs in developer mode by default (when you sign your apk with a debug key). It will turn to Release mode automatically when you sign your apk with a release key.

However you can explicity request Pollfish SDK to run in release or developer mode by setting mode through ParamsBuilder instance during initialization. If you explicity request release mode or not through ParamsBuilder, type of signing key is ignored and does not affect Pollfish mode any more.
<br/>

Below you can see an example on how you can turn your app in Release mode explicitly:

```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.releaseMode(true)
					.build();
```
<br/>
#### **10.6 .customMode(boolean customMode)**  

Initializes Pollfish in custom mode if set to true. By default this is set to false.

**true Vs false**

*   **true** -  ignores Pollfish panel behavior from Pollfish Developer Dashboard. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish panel view to app users. This method is usually used when app developers want to incentivize first somehow their users. 
*   **false** - is the standard way of using Pollfish in your apps. This option enables controlling behavior (intrusiveness) of Pollfish panel in an app from Pollfish Developer Dashboard.

![alt text](https://storage.googleapis.com/pollfish_production/multimedia/dashboard_1.png)
<br/><br/>

Below you can see an example of setting Pollfish to custom mode with ParamsBuilder object:  
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.customMode(true)
					.build();
```

<br/>
#### **10.7 .pollfishSurveyReceivedListener(PollfishSurveyReceivedListener pollfishSurveyReceivedListener)**

Sets a notification listener when a Pollfish Survey is received. With this notification publisher can also get informed about the type of survey (Playful or not) that was received and money to be earned if survey is completed, shown in USD cents.

Below you can see an example of how you can register and listen within your code to Pollfish survey received notification through ParamsBuilder instance:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishSurveyReceivedListener(new PollfishSurveyReceivedListener() {
    @Override
    public void onPollfishSurveyReceived(final boolean playfulSurvey, final int surveyPrice)
    {}
    })
	.build();
```
<br/>
#### **10.8 .pollfishSurveyNotAvailableListener(PollfishSurveyNotAvailableListener  pollfishSurveyNotAvailableListener)**

Sets a notification listener when a Pollfish Survey is not available after initialization.

Below you can see an example of how you can register and listen within your code to Pollfish survey not available notification through ParamsBuilder instance:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishSurveyNotAvailableListener(new PollfishSurveyNotAvailableListener() {
    @Override
    public void onPollfishSurveyNotAvailable(){}
    })
	.build();
```
<br/>
#### **10.9 .pollfishSurveyCompletedListener(PollfishSurveyCompletedListener pollfishSurveyCompletedListener)**

Sets a notification listener when a Pollfish Survey is completed. With this notification, publisher can also get informed about the type of survey (Playful or not) that was completed and money earned from that survey in USD cents.

Below you can see an example of how you can register and listen within your code to Pollfish survey completed notification through ParamsBuilder instance:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishSurveyCompletedListener(new PollfishSurveyCompletedListener() {
    @Override
    public void onPollfishSurveyCompleted(final boolean playfulSurvey, final int surveyPrice)
    {}
    })
	.build();
```
<br/>
#### **10.10 .pollfishUserNotEligibleListener(PollfishUserNotEligibleListener pollfishUserNotEligibleListener)**

Sets a notification listener when a user is not eligible for a Pollfish survey. If a user is not eligible for a survey this notification will be fired and publisher will make no money from that survey. User not eligible notification will fire after survey received when user starts completing the survey.

Below you can see an example of how you can register and listen within your code to Pollfish user not eligible notification:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishUserNotEligibleListener(new PollfishUserNotEligibleListener() {
    	@Override
    	public void onUserNotEligible(){}
    	})
	.build();
```
<br/>
#### **10.11 .pollfishOpenedListener(PollfishOpenedListener pollfishOpenedListener)**

Sets a notification listener Pollfish survey panel is opened. Publishers usually use this notification to pause a game until Pollfish panel is closed again.

Below you can see an example of how you can register and listen within your code to Pollfish panel opened notification:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishOpenedListener(new PollfishOpenedListener() {
    	@Override
    	public void onPollfishOpened(){}
    	})
	.build();
```
<br/>
#### **10.12 .pollfishClosedListener(PollfishClosedListener pollfishClosedListener)**

Sets a notification listener Pollfish survey panel is closed. Publishers usually use this notification to resume a game that they have previously paused when Pollfish panel opened.

Below you can see an example of how you can register and listen within your code to Pollfish panel closed notification:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishClosedListener(new PollfishClosedListener() {
    	@Override
    	public void onPollfishClosed(){}
    	})
	.build();
```
<br/>
#### **10.13 .userProperties(UserProperties userProperties)**

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and also achieve a better fill rate and higher priced surveys.

| **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default

Below you can see an example of how you can pass user properties during initialization.

Just import:  

```
import com.pollfish.constants.UserProperties;
```
and specify any user information you know upfront:

```java

UserProperties userProperties = new UserProperties()
                      /*included in Demographic Surveys*/      		
		      .setGender(Gender.MALE)
                      .setYearOfBirth(YearOfBirth._1984)
                      .setMaritalStatus(MaritalStatus.SINGLE)
                      .setParentalStatus(ParentalStatus.ZERO)
                      .setEducation(EducationLevel.UNIVERSITY)
                      .setEmployment(EmploymentStatus.EMPLOYED_FOR_WAGES)
                      .setCareer(Career.TELECOMMUNICATIONS)
                      .setRace(Race.WHITE)
                      .setIncome(Income.MIDDLE_I)
		       /*other user attributes*/
                      .setEmail("user_email@test.com")
                      .setFacebookId("USER_FB")
                      .setGoogleId("USER_GOOGLE")
                      .setTwitterId("USER_TWITTER")
                      .setLinkedInId("USER_LINKEDIN")
                      .setPhone("USER_PHONE")
                      .setName("USER_NAME")
                      .setSurname("USER_SURNAME")
                      .setCustomAttributes("MY_PARAM", "MY_VALUE");
			    
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.userProperties(userProperties)
	.build();
```
<br/>
#### **10.4 .surveyFormat(SurveyFormat surveyFormat)**

Explicitly requests a specific survey format.

| **Note:** You can request and receive a specific survey format only in debug mode


There are four different options available: 

- SurveyFormat.BASIC 
- SurveyFormat.PLAYFUL
- SurveyFormat.THIRD_PARTY
- SurveyFormat.RANDOM

<br/>
Here is an example of how a user can explicitly request a specific survey format during initialization.

Just import:
<br/>
```java
import com.pollfish.constants.SurveyFormat;
```
and specify the survey format you would like to receive in order to test:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.surveyFormat(SurveyFormat.PLAYFUL)
					.build();
```
<br/>
<br/>
<br/>
### 11. Handling orientation changes (optional)

If your app supports both orientations and **your Activities are recreated** on each orientation change **you should not do anything more**.  

If your app **does not recreate the Activity** on change orientation: 

e.g you may have in your AndroidManifest.xml file, the following lines if targeting prior Android 3.2:  

```java
<activity android:name=".MyActivity" android:configChanges="keyboardHidden|orientation"> 
```

or beginning with Android 3.2:

```java
<activity android:name=".MyActivity" android:configChanges="keyboardHidden|orientation|screenSize">
```

If any of the above is true you should override the **onConfigurationChanged** method and initialize Pollfish again

```java
@Override
public void onConfigurationChanged(Configuration newConfig) {
	super.onConfigurationChanged(newConfig);
	
    	PollFish.initWith(this, new ParamsBuilder("YOUR_API_KEY").build());
}
```
<br/>
<br/>
### 12. Implement Pollfish event listeners through your Activity (optional)

#### **12.1. Get notified when a Pollfish survey is received**

You can be notified when a Pollfish survey is received. With this notification publisher can also get informed about the type of survey (Playful or not) that was received and money to be earned if survey is completed, shown in USD cents.

 Just import:  

```java
import com.pollfish.interfaces.PollfishSurveyReceivedListener; 
```

and make your Activity implement PollfishSurveyReceivedListener, for example:

```java
public class MyActivity extends Activity implements PollfishSurveyReceivedListener
```

and Override onPollfishSurveyReceived() function: 

```java
@Override
public void onPollfishSurveyReceived(boolean playfulSurveys, int surveyPrice) {
  Log.d("Pollfish", "Pollfish survey received - Playful survey: " + playfulSurveys + " with price: " + surveyPrice);
}
```
<br/>
#### **12.2. Get notified when a Pollfish survey is not available**

You can be notified when Pollfish survey is not available. 

Just import:  

```java
import com.pollfish.interfaces.PollfishSurveyNotAvailableListener;
```

and Override onPollfishSurveyNotAvailable() function:  

```java
@Override
public void onPollfishSurveyNotAvailable() {
  Log.d("Pollfish", "Survey not available!");
}
```
<br/>
#### **12.3. Get notified when a Pollfish survey is completed**

You can be notified when a user completed a survey. With this notification, publisher can also get informed about the type of survey (Playful or not) that was completed and money earned from that survey in USD cents.

Just import:  

```java
import com.pollfish.interfaces.PollfishSurveyCompletedListener;
```

and make your Activity implement SurveyCompletedListener,for example: 

```java
public class MyActivity extends Activity implements PollfishSurveyCompletedListener 
```

and Override  onPollfishSurveyCompleted() function:

```java
@Override
public void onPollfishSurveyCompleted(boolean playfulSurveys , int surveyPrice) {
  Log.d("Pollfish", "Pollfish survey completed - Playful survey: " + playfulSurveys + " with price: " + surveyPrice);

}
```
<br/>
#### **12.4. Get notified when a user is not eligible for a Pollfish survey**

You can be notified when a user is not eligible for a Pollfish survey. If a user is not eligible for a survey, this notification will be fired and publisher will make no money from that survey. User not eligible notification will fire after survey received when user starts completing the survey.

Just import:  

```java
import com.pollfish.interfaces.PollfishUserNotEligibleListener;
```

and make your Activity implement PollfishUserNotEligibleListener, e.g  

```java
public class MyActivity extends Activity implements PollfishUserNotEligibleListener
```

and Override the onUserNotEligible() function 

```java
@Override
public void onUserNotEligible() {
	Log.d("Pollfish", "onUserNotEligible()");

}
```
<br/>
#### **12.5. Get notified when Pollfish Survey panel has opened**

You can be notified when a Pollfish survey panel has opened. Publishers usually use this notification to pause a game until Pollfish panel is closed again.

Just import:  

```java
import com.pollfish.interfaces.PollfishOpenedListener; 
```

and make your Activity implement PollfishOpenedListener, e.g  

```java
public class MyActivity extends Activity implements PollfishOpenedListener
```

and Override the onPollfishOpened() function  

```java
@Override
public void onPollfishOpened () {
    Log.d("Pollfish", "Survey opened!");
}
```
<br/>
#### **12.6. Get notified when Pollfish Survey panel has closed**

You can be notified when a Pollfish survey panel has closed. Publishers usually use this notification to resume a game that they have previously paused when Pollfish panel opened.

Just import:  

```java
import com.pollfish.interfaces.PollfishClosedListener;
```

and make your Activity implement PollfishClosedListener, e.g  

```java
public class MyActivity extends Activity implements PollfishClosedListener
```

and Override the onPollfishClosed() function  

```java
@Override
public void onPollfishClosed () {
    Log.d("Pollfish", "Survey closed!");
}
```


<br/>
### 13. Other actions (optional)

#### **13.1. Manually show or hide Pollfish in an Activity**

You can manually show or hide Pollfish indicator or survey panel by calling anywhere in your activity after the initialization line:  

```java
PollFish.show();
```

or  

```java
PollFish.hide();
```

#### **13.2. Check if Pollfish survey is still available on your device**

It happens that time had past since you initialized Pollfish and a survey is received. If you want to check if survey is still avaialble on your device and has not expired you can check by calling:

```java
PollFish.isPollfishPresent();
```
<br/><br/>
### 14. Proguard (optional)

If you use proguard with your app, please insert the following line in your proguard configuration file:  

```java
-libraryjars libs/pollfish-googleplay-4.3.4.jar // not necessary if using Android Studio or .aar library
-dontwarn com.pollfish.**
-keep class com.pollfish.** { *; }
```

where pollfish-googleplay-4.3.4.jar is the latest pollfish jar you use in your app and is placed in your libs folder (if you used Pollfish jar file).

| **Note:** Using Proguard with Pollfish requires setting your Project Build Target to Android 5.0 (API 21)!
<br/><br/>
### 15. Highly targeted surveys (optional)

If you wish to receive highly targeted surveys in your app and increase your chances for a higher revenue you can include any or all of the following permissions in your AndroidManifest.xml file:  

```java
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

If you want to be eligible for beacon based surveys for your app you can include the following permsissions in your AndroidManifest.xml file:  

```java
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```
<br/><br/>
### 16\. Server-to-server callbacks on survey completion (optional)

If you want to reward your users for completing a survey it is common practise to verify this through server to server callbacks in order to introduce an enhanced security layer to your system. You can easily add your postback  url on your app's page on Pollfish Developer Dashboard. You can read more on how to set server to server callbacks in our FAQ page <a href="https://pollfish.zendesk.com/hc/en-us/articles/204106261">here</a>. 



