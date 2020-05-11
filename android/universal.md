<div class="changelog" data-version="5.4.1">
v5.4.1	

- Updated functionality of rendering Pollfish overlay panel above complex Activity and Fragments hirarchies

v5.4.0	

- Removed updated restricted non-SDK interface list usages, as described [here](https://developer.android.com/distribute/best-practices/develop/restrictions-non-sdk-interfaces?authuser=1)

v5.3.3
	
- Added option to fire both Pollfish Closed local notifications (if provided both through ParamsBuilder and implemented by the Activity)

v5.3.2
	
- Exposed functionality to render overlay on top of a new Activity
	
v5.3.0
	
- Exposed a new public interface showOnTopOfActivity

v5.2.0
	
- Fixed issues with view hierarchy on multiple activities

v5.1.0
	
- Fixed conflicts with other ad SDKs

v5.0.2
	
- Removed installed apps functionality

v5.0.0
	
- Added offerwall support
- Removed deprecated init interfaces
- Removed deprecated interfaces PollfishSurveyReceivedListener,PollfishSurveyCompletedListener
- Deprecated customMode and introduced rewardMode
- Added support for exiting faulty mediation surveys
- Changed minimum SDK to 16

v4.5.0
	
- Moved away from Jar format in SDKs
- Fixed localisation issues
- Added new interfaces PollfishReceivedSurveyListener,PollfishCompletedSurveyListener to expose survey info (CPA, LOI, IR, Survey Class)
- Deprecated old interfaces PollfishSurveyReceivedListener,PollfishSurveyCompletedListener

v4.4.0
	
- Added the ability to render surveys from Mediation within the app
- Added notification for user rejecting a survey
- Improved performance
- Fixed bugs

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

> **Note:** Do not use this SDK for distribution on Google Play Store!

## Quick Guide of Universal SDK

1. Register as a publisher at Pollfish, create an App and copy app's API key
2. Download Pollfish aar file and import to your project
3. Import Pollfish classes
4. Add permissions to AndroidManifest.xml
5. Call Pollfish initialization function in onResume() of your Activity to activate Pollfish
6. Update your privacy policy
7. Set to **Release mode** and publish your app at any app store
8. Request your account to get verified from Pollfish Dashboard

> **Requirements:** Pollfish Android SDK works with Android 16 and above.  

<br/><br/><br/><br/>
## Steps Analytically

### 1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on when initializing Pollfish within your code.

### 3. Add Pollfish jar or aar library to your project

Download Pollfish Android SDK or reference it through jCenter().

#### **Download Pollfish Android SDK**

Import Pollfish **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project add select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish aar file. Right click again on your project and in Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

#### **Retrieve Pollfish Android SDK through jCenter()**

Retrieve Pollfish through **jCenter()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```
dependencies {
  implementation 'com.pollfish:pollfish:5.4.0:universalRelease@aar'
}
```

### 4. Import Pollfish classes

Import Pollfish classes with the following lines at the top of your Activity’s class file:

```java
import com.pollfish.main.PollFish;
import com.pollfish.main.PollFish.ParamsBuilder;
import com.pollfish.constants.Position;
```

### 5. Add permissions to AndroidManifest.xml

#### 5.1 Add access to internet permission

You should add the following line in your AndroidManifest.xml  

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```

#### 5.2 Add support for cleartext http traffic

If you are looking to use Pollfish mediation surveys from all the providers, in order to avoid any faulty behaviour on new Android devices we would advice that you allow cleartext http traffic. To achieve that you need to create a new file named **network_security_config.xml** under **res/xml** and add the following inside:

```
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true">
        <trust-anchors>
            <certificates src="system" />
        </trust-anchors>
    </base-config>
</network-security-config>
```

add in your Androidmanifest.xml reference the file above in the **android:networkSecurityConfig** tag as below:

```
 <application
        android:networkSecurityConfig="@xml/network_security_config">
```

### 6. Initialize Pollfish

Now you can easily initialize Pollfish. In order to initialize you will need to create an instance of ParamsBuilder. ParamsBuilder has only one mandatory parameter which is the API key of your app (step 2 above). 

| **Note:** In section 9 you can see several other optional params that you can pass to ParamsBuilder instance in order to configure Pollfish behaviour during initialization.


```java
ParamsBuilder paramsBuilder = new ParamsBuilder(String "YOUR_API_KEY").build();
```
Once you have created ParamsBuilder instance, you can call Pollfish initWith() in **onResume()** function of your Activity ( just after super.onResume() ) and you are ready to go.

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


| **Note:** If your app calls setContentView() function more than once in your Activity lifecycle you should call Pollfish.initWith() or just after each setContentView in order to use Pollfish properly.**  
<br/>

### 7\.  Update your Privacy Policy

Add the following paragraph to your app's privacy policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*  

*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”*

<br/>

| **Note:** It's important that you include this disclosure both in the privacy policy posted on Google Play but also in the privacy policy included in your app, as described in [Google's Developer Privacy Policy](https://play.google.com/about/privacy-security/personal-sensitive/)  


<br/><br/>

**At this point you are ready to go live! Sign your app with a release key or explicitly set .releaseMode(true) - (section 9.5) in your ParamsBuilder and publish to any Android app store**

---
<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>
<br/><br/><br/>

| **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process users need to go through in order to join the platform. If a paid survey is available at that point of time, the demographic questions will be inserted at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this type of targeting.

<br/>

<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>
<br/>


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents  and also Survey Type. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 8.13 - and skip or shorten this way, Pollfish Demographic surveys.

<br/>
### 8\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>


<br/>
<br/>


## Optional section


In this section we will list several options that can be used to control Pollfish surveys behaviour. For example how to listen to several events that happen during the lifetime of a survey, or how to receive more targeted (high-paid) surveys. All these steps are optional.


### 9. ParamsBuilder available options (optional)

As we have seen in section 6, ParamsBuilder instance requires only one mandatory param, the API key of the app that you acquired at step 2. 

```java
ParamsBuilder paramsBuilder = new ParamsBuilder(String "YOUR_API_KEY").build();
```

However you can set several other params to control the behaviour of Pollfish surveys within your app or register to several notifications.
<br/>
Below you can see all the available options of ParamsBuilder instance. All these functions can be called in any order consequently prior calling build() to ParamsBuilder instance.
<br/>

No | Description
------------ | -------------
9.1 | **.indicatorPosition(int position)**  <br/> Sets the Position where you wish to place the Pollfish indicator (small red rectangle)
9.2 | **.requestUUID(String requestUUID)**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
9.3 | **.indicatorPadding(int padding)**  <br/> Sets padding (in dp) from top or bottom according to the Position of the indicator
9.4 | **.userLayout(ViewGroup userLayout)**  <br/> Sets User View layout that Pollfish surveys will be rendered above it
9.5 | **.releaseMode(boolean releaseMode)**  <br/> Sets Pollfish SDK to Developer or Release mode
9.6 | [DEPRECATED-use 9.18] **.customMode(boolean customMode)**  <br/> Initializes Pollfish in custom mode
9.7 | [DEPRECATED-use 9.16] **.pollfishSurveyReceivedListener(PollfishSurveyReceivedListener pollfishSurveyReceivedListener)**  <br/> Sets a notification listener when Pollfish Survey is received
9.8 | **.pollfishSurveyNotAvailableListener(PollfishSurveyNotAvailableListener pollfishSurveyNotAvailableListener)**  <br/> Sets a notification listener when Pollfish Survey is not available
9.9 | DEPRECATED-use 9.17] **.pollfishSurveyCompletedListener(PollfishSurveyCompletedListener pollfishSurveyCompletedListener)**  <br/> Sets a notification listener when Pollfish Survey is completed
9.10 | **.pollfishUserNotEligibleListener(PollfishUserNotEligibleListener pollfishUserNotEligibleListener)**  <br/> Sets a notification listener when a user is not eligible for a Pollfish survey
9.11 | **.pollfishUserRejectedSurveyListener(PollfishUserRejectedSurveyListener pollfishUserRejectedSurveyListener)**  <br/> Sets a notification listener when a user rejects a survey
9.12 | **.pollfishOpenedListener(PollfishOpenedListener pollfishOpenedListener)**  <br/> Sets a notification listener when Pollfish Survey panel is opened
9.13 | **.pollfishClosedListener(PollfishClosedListener pollfishClosedListener)**  <br/> Sets a notification listener when Pollfish Survey panel is closed
9.14 | **.userProperties(UserProperties userProperties)**  <br/> Send user attributes to skip or shorten Pollfish demographic surveys
9.15 | **.surveyFormat(SurveyFormat surveyFormat)**  <br/> Requests a specific survey format (only in debug mode)
9.16 | **.pollfishReceivedSurveyListener(PollfishReceivedSurveyListener pollfishReceivedSurveyListener)**  <br/> Sets a notification listener when Pollfish Survey is received
9.17 | **.pollfishCompletedSurveyListener(PollfishCompletedSurveyListener pollfishCompletedSurveyListener)**  <br/> Sets a notification listener when Pollfish Survey is completed
9.18 | **.rewardMode(boolean rewardMode)**  <br/> Initializes Pollfish in reward mode
9.19 | **.offerWallMode(boolean offerWallMode)**  <br/> Sets Pollfish to offerwall mode.


<br/>
#### **9.1 .indicatorPosition(int position)**
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
This choice affects also from which side the survey panel will slide-in.
<br/>
#### **9.2 .requestUUID(String requestUUID)**

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
#### **9.3 .indicatorPadding(int padding)**

Sets padding (in dp) of Pollfish indicator, from top or bottom of the screen according to the specified Position of the indicator as described before in point 9.1. Default value is 5. If Position of Pollfish indicator is MIDDLE, padding is calculated from the top of the middle of the screen.
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
#### **9.4 .userLayout(ViewGroup userLayout)**

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
#### **9.5 .releaseMode(boolean releaseMode)**

Sets Pollfish SDK to Developer or Release mode
<br/><br/>
**Developer Vs Release Mode**

You can use Pollfish either in Developer or in Release mode.  

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish runs in developer mode by default (when you sign your apk with a debug key). It will turn to Release mode automatically when you sign your apk with a release key.

However you can explicity request Pollfish SDK to run in release or developer mode by setting mode through ParamsBuilder instance during initialization. If you explicity request release mode or not through ParamsBuilder, the type of the signing key is ignored and does not affect Pollfish mode any more.
<br/>

Below you can see an example on how you can turn your app in Release mode explicitly:

```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.releaseMode(true)
					.build();
```
<br/>
#### **9.6 .customMode(boolean customMode)**  [DEPRECATED-use 9.18]

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
This mode should be used if you want to incentivize users to participate to surveys. We have a detailed guide on how to implement the rewarded approach <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a>
<br/>
#### **9.7 .pollfishReceivedSurveyListener(PollfishReceivedSurveyListener pollfishReceivedSurveyListener)** [DEPRECATED-use 9.16]

Sets a notification listener when a Pollfish Survey is received. With this notification, the publisher can also get informed about the type of survey (Playful or not) that was received and money to be earned if survey is completed, shown in USD cents.

Below you can see an example of how you can register and listen within your code to Pollfish survey received notification through ParamsBuilder instance:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishReceivedSurveyListener(new PollfishReceivedSurveyListener() {
    @Override
    public void onPollfishSurveyReceived(SurveyInfo surveyInfo)
    {
    	Log.d(TAG, "Pollfish :: CPA: " + surveyInfo.getSurveyCPA()
                + " SurveyClass: " + surveyInfo.getSurveyClass()
		+ " LOI: " + surveyInfo.getSurveyLOI()
		+ " IR: " + surveyInfo.getSurveyIR()
		+ " Reward Name: " + surveyInfo.getRewardName()
		+ " Reward Value: " + surveyInfo.getRewardValue());
	}
    })
	.build();
```
<br/>
| **Note:** In offerwall mode, SurveyInfo object should be empty. In that case the notification informs that surveys are available in the offerwall
<br/>
#### **9.8 .pollfishSurveyNotAvailableListener(PollfishSurveyNotAvailableListener  pollfishSurveyNotAvailableListener)**

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
#### **9.9 .pollfishCompletedSurveyListener(PollfishCompletedSurveyListener pollfishCompletedSurveyListener)** [DEPRECATED-use 9.17]

Sets a notification listener when a Pollfish Survey is completed. With this notification, the publisher can also get informed about the type of survey (Playful or not) that was completed and money earned from that survey in USD cents.

Below you can see an example of how you can register and listen within your code to Pollfish survey completed notification through ParamsBuilder instance:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishCompletedSurveyListener(new PollfishCompletedSurveyListener() {
    @Override
    public void onPollfishSurveyCompleted(SurveyInfo surveyInfo)
    {
    	Log.d(TAG, "Pollfish :: CPA: " + surveyInfo.getSurveyCPA()
                + " SurveyClass: " + surveyInfo.getSurveyClass()
		+ " LOI: " + surveyInfo.getSurveyLOI()
		+ " IR: " + surveyInfo.getSurveyIR()
		+ " Reward Name: " + surveyInfo.getRewardName()
		+ " Reward Value: " + surveyInfo.getRewardValue());
    }
    })
	.build();
```
<br/>
#### **9.10 .pollfishUserNotEligibleListener(PollfishUserNotEligibleListener pollfishUserNotEligibleListener)**

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
#### **9.11 .pollfishUserRejectedSurveyListener(PollfishUserRejectedSurveyListener pollfishUserRejectedSurveyListener)**

Sets a notification listener when a user rejects a survey. If a user decides to reject a survey this notification will be fired and publisher will make no money from that survey. 

Below you can see an example of how you can register and listen within your code to Pollfish user rejected survey notification:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishUserRejectedSurveyListener(new PollfishUserRejectedSurveyListener() {
    	@Override
    	public void onUserRejectedSurvey(){}
    	})
	.build();
```
<br/>
#### **9.12 .pollfishOpenedListener(PollfishOpenedListener pollfishOpenedListener)**

Sets a notification listener for when Pollfish survey panel is opened. Publishers usually use this notification to pause a game until Pollfish panel is closed again.

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
#### **9.13 .pollfishClosedListener(PollfishClosedListener pollfishClosedListener)**

Sets a notification listener for when Pollfish survey panel is closed. Publishers usually use this notification to resume a game that they have previously paused when Pollfish panel opened.

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
#### **9.14 .userProperties(UserProperties userProperties)**

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
		      .setNumberOfEmployees(NumberOfEmployees.GREATER_THAN_FIVE_THOUSANDS)
                      .setSpokenLanguages(SpokenLanguages.FRENCH)
                      .setOrganizationRole(OrganizationRole.C_LEVEL_EXECUTIVE)
                      .setCustomAttributes("MY_PARAM", "MY_VALUE");
			    
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.userProperties(userProperties)
	.build();
```
<br/>
A detailed list of all the required demographics can be found at the following [link](https://www.pollfish.com/docs/demographic-surveys)

#### **9.15 .surveyFormat(SurveyFormat surveyFormat)**

Explicitly requests a specific survey format.

There are four different options available: 

- SurveyFormat.BASIC 
- SurveyFormat.PLAYFUL
- SurveyFormat.THIRD_PARTY
- SurveyFormat.RANDOM


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
#### **9.16 .pollfishReceivedSurveyListener(PollfishReceivedSurveyListener pollfishReceivedSurveyListener)**

Sets a notification listener when a Pollfish Survey is received. 

With this notification the publisher can get informed through the SurveyInfo object returned, about the:

- **surveyCPA** : money to be earned from survey received in US dollar cents (estimated based on daily exchange currency)
- **surveyIR** : the current estimation for the survey incidence rate as an integer number in the range 0-100. This param is optional and will have as default the value -1 if it was not set and the IR was not computed reliably.
- **surveyLOI** : the expected time in minutes that it takes to complete the survey. This param is optional and will have as default the value -1 if it was not set and the LOI wan not computed reliably.
- **surveyClass** :  information about the survey network and type* 
- **rewardName** :  information about the reward name as specified on Publishers Dashboard* 
- **rewardValue** :  information about the reward value as calculated based on exhange rate specified on Publishers Dashboard* 

The syntax for surveyClass values is:

```
provider["/"type]
provider: "Pollfish" | "Toluna" | "Cint" | "Lucid" | "InnovateMR" | "SaySo" | "P2Sample"
type: "Basic" | "Playful" | "ThirdParty" | "Demographics" | "Internal"

example: Pollfish/Playful
```

network name followed by an optional slash and survey type.

The provider is the network that provides the survey. The syntax rule has all the networks currently supported by Pollfish. The type reffers to different types of surveys provided by a network.

The whole set of values currently supported are:

| Value              | Description
|:------------------|:----------------
| **Pollfish**           | Pollfish Basic survey
| **Pollfish/Basic**           |  Pollfish Basic survey (another name)
| **Pollfish/Playful**         | Pollfish Playful survey 
| **Pollfish/ThirdParty**         | Pollfish 3rd party survey
| **Pollfish/Demographics**         | Pollfish Demographic survey
| **Pollfish/Internal**         | Pollfish internal survey created by the publisher
| **Toluna**         | Toluna survey   
| **Cint**         | Cint survey   
| **InnovateMR**         | InnovateMR survey   
| **SaySo**       | SaySo survey   
| **P2Sample**       | P2Sample survey

When a new mediation network enters the Pollfish network the appropriate values will be added.

Below you can see an example of how you can register and listen within your code to Pollfish survey received notification through ParamsBuilder instance:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY").pollfishReceivedSurveyListener(new PollfishReceivedSurveyListener() {
  @Override
  public void onPollfishSurveyReceived(SurveyInfo surveyInfo) {
        Log.d(TAG, "Pollfish :: CPA: " + surveyInfo.getSurveyCPA()
                + " SurveyClass: " + surveyInfo.getSurveyClass()
		+ " LOI: " + surveyInfo.getSurveyLOI()
		+ " IR: " + surveyInfo.getSurveyIR());
    }
  }).build();
```
<br/>

**9.17 .pollfishCompletedSurveyListener(PollfishCompletedSurveyListener pollfishCompletedSurveyListener)**

Sets a notification listener when a Pollfish Survey is completed. With this notification, publisher can also get informed through the SurveyInfo object returned about the money earned in USD cents, the survey class, IR and LOI of the survey.

Below you can see an example of how you can register and listen within your code to Pollfish survey completed notification through ParamsBuilder instance:
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
	.pollfishCompletedSurveyListener(new PollfishCompletedSurveyListener() {
    @Override
    public void onPollfishSurveyCompleted(SurveyInfo surveyInfo)
    {}
    })
	.build();
```
<br/>

**9.18 .rewardMode(boolean rewardMode)**

Initializes Pollfish in reward mode if set to true. By default this is set to false.

**true Vs false**

*   **true** -  ignores Pollfish panel behavior from Pollfish Developer Dashboard. It always skips showing Pollfish indicator (small Pollfish icons) and hides Pollfish survey panel view from users. This method is aimed to be used when app developers want to incentivize first somehow their users. 
*   **false** - is the standard way of using Pollfish in your apps. This option enables controlling behavior (intrusiveness) of Pollfish panel in an app from Pollfish Developer Dashboard.
<br/>

Below you can see an example of setting Pollfish to reward mode with ParamsBuilder object:  
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.rewardMode(true)
					.build();
```

<br/>
This mode should be used if you want to incentivize users to participate to surveys. We have a detailed guide on how to implement the rewarded approach <a href="https://www.pollfish.com/docs/rewarded-surveys/">here</a>
<br/>

**9.19 .offerWallMode(boolean offerWallMode)**

Enables offerwall mode. If not set, one single survey is shown each time.
<br/>
Below you can see an example of setting Pollfish to offerwall mode with ParamsBuilder object:  
<br/>
```java
ParamsBuilder paramsBuilder = new ParamsBuilder("YOUR_API_KEY")
					.offerWallMode(true)
					.rewardMode(true)
					.build();
```


<br/>
<br/>
### 10. Handling orientation changes (optional)

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
### 11. Implement Pollfish event listeners through your Activity (optional)

#### **11.1. Get notified when a Pollfish survey is received**

You can be notified when a Pollfish survey is received. With this notification publisher can also get informed about the type of survey that was received, money to be earned if survey gets completed, shown in USD cents and other info around the survey such as LOI and IR.

 Just import:  

```java
import com.pollfish.interfaces.PollfishReceivedSurveyListener; 
```

and make your Activity implement PollfishReceivedSurveyListener, for example:

```java
public class MyActivity extends Activity implements PollfishReceivedSurveyListener
```

and Override onPollfishSurveyReceived() function: 

```java
@Override
public void onPollfishSurveyReceived(SurveyInfo surveyInfo) {
	Log.d(TAG, "Pollfish :: CPA: " + surveyInfo.getSurveyCPA()
                + " SurveyClass: " + surveyInfo.getSurveyClass()
		+ " LOI: " + surveyInfo.getSurveyLOI()
		+ " IR: " + surveyInfo.getSurveyIR()
		+ " Reward Name: " + surveyInfo.getRewardName()
		+ " Reward Value: " + surveyInfo.getRewardValue());
}
```
<br/>
| **Note:** In offerwall mode, SurveyInfo object should be empty. In that case the notification informs that surveys are available in the offerwall
<br/>
#### **11.2. Get notified when a Pollfish survey is not available**

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
#### **11.3. Get notified when a Pollfish survey is completed**

You can be notified when a user completed a survey. With this notification, publisher can also get informed about the type of survey, money earned from that survey in USD cents and other info around the survey such as LOI and IR.

Just import:  

```java
import com.pollfish.interfaces.PollfishCompletedSurveyListener;
```

and make your Activity implement SurveyCompletedListener,for example: 

```java
public class MyActivity extends Activity implements PollfishCompletedSurveyListener 
```

and Override  onPollfishSurveyCompleted() function:

```java
@Override
public void onPollfishSurveyCompleted(SurveyInfo surveyInfo) {

	Log.d(TAG, "Pollfish :: CPA: " + surveyInfo.getSurveyCPA()
                + " SurveyClass: " + surveyInfo.getSurveyClass()
		+ " LOI: " + surveyInfo.getSurveyLOI()
		+ " IR: " + surveyInfo.getSurveyIR()
		+ " Reward Name: " + surveyInfo.getRewardName()
		+ " Reward Value: " + surveyInfo.getRewardValue());
}
```
<br/>
#### **11.4. Get notified when a user is not eligible for a Pollfish survey**

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
#### **11.5. Get notified when Pollfish Survey panel has opened**

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
#### **11.6. Get notified when Pollfish Survey panel has closed**

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
### 12. Other actions (optional)

#### **12.1. Manually show or hide Pollfish in an Activity**

You can manually show or hide Pollfish indicator or survey panel by calling anywhere in your activity after the initialization line:  

```java
PollFish.show();
```

or  

```java
PollFish.hide();
```

#### **12.2. Check if Pollfish survey is still available on your device**

It happens that time had past since you initialized Pollfish and a survey is received. If you want to check is survey is still avaialble on your device and has not expired you can check by calling:

```java
PollFish.isPollfishPresent();
```
<br/><br/>
### 13. Proguard (optional)

If you use proguard with your app, please insert the following line in your proguard configuration file:  

```java
-dontwarn com.pollfish.**
-keep class com.pollfish.** { *; }
```

| **Note:** Using Proguard with Pollfish requires setting your Project Build Target to Android 5.0 (API 21)!

If you do not include Google Play services in your project, add the following code in your Proguard file:  

```java
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
<br/><br/>
### 14. Highly targeted surveys (optional)

If you wish to receive highly targeted surveys in your app and increase your chances for a higher revenue you can include any or all of the following permissions in your AndroidManifest.xml file:  

```java
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

If you want to be eligible for beacon based surveys for your app you can include the following permsissionsin your AndroidManifest.xml file:  

```java
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```
<br/><br/>
### 15\. Server-to-server callbacks on survey completion (optional)

If you want to reward your users for completing a survey it is common practise to verify this through server to server callbacks in order to introduce an enhanced security layer to your system. You can easily add your postback  url on your app's page on Pollfish Developer Dashboard. You can read more on how to set server to server callbacks <a href="https://www.pollfish.com/docs/s2s">here</a>. 


