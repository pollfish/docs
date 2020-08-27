<div class="changelog" data-version="5.3.1">	
v.5.3.1

- Added a modulemap for Swift interoperability
	
	
v.5.3.0

- Added support for iOS 14. Pollfish SDK utilizes the IDFA and therefore it should initialized in iOS 14 only when the IDFA tracking permission is granted by the user.
	
v.5.2.5

- Added functionality if overlay views are not attached to top view controller, re-attach

v.5.2.4

- Fixed overlay visibilty in modular views in iOS<13

v.5.2.3

- Ensure the Pollfish overlay view is always on top

v.5.2.2

- Added backwards compatibility support for XCode 10.x

v.5.2.1

- Added isPollfishPanelOpen public interface

v.5.2.0

- Fixed issues around panel visibility and concurrency
- Added support for new demographics (spoken languages, organization role, organization number of employees)

v.5.1.0

- Removed deprecated UIWebView functions

v.5.0.0

- Created new expandable interface initWithAPIKey(...) with a configuration PollfishParams object
- Removed old init interfaces
- Removed deprecated interface setAttributes
- Removed customMode and introduced rewardMode option
- Added support for offerwall mode
- Added option to pass a container view to rendered Pollfish overlay
- Removed automatic re-init feature for device orientation
- Added support for exiting faulty mediation surveys
	
v4.5.1

- Fixed bug with user locale

v4.5.0

- Added support for retrieving survey info in callbacks (CPA, IR, LOI, Survey Class)

v4.4.0

- Added support for iOS 12
- New iOS minimum is 9.0
- Added dependency on WebKit.framework
- Added the ability to render surveys from Mediation within the app
- Added notification for user rejecting a survey
- Improved performance
- Fixed bugs


v4.3.5

- Added ability to test survey formats in debug mode

v4.3.4

- Deprecated destroy function
- Added dynamic caching
- Drastically decreased sdk size
- Updated Pollfish indicator
- Improved performance
- Fixed memory leaks
- XCode 9 support (required)

v4.2.4

- Fixed bitcode issue

v4.2.3

- Added support for sending user attributes during init
- Deprecated setAttributeDictionary function
- Fixed bug for multiple notifications and url encoding
- Fixed isPollfishPresent bug

v4.2.2

- Fixed bug on survey view

v4.2.1

- ATS compliance
- improved performance

v4.2.0

- Fixed bitcode issue
- New API functions to support beacon and location relevant surveys 
- Added support for new type of questions in surveys, including video surveys
- Added new framework dependency (SystemConfiguration.framework)

v4.1.2

- Fixed ARM64 issue


v4.1.1

- support Bitcode
- support Xcode 7

v4.1.0

- Fixed bug on orientation changes
- Converted lib to ARC

v4.0.3

- Fixed bug in init function with Request UUID in release mode

v4.0.2

- Weak link of AdSupport framework
- Added init function with option to pass a custom param and receive it on server-to-server callback
- Added UserAttributesDictionary class for passing attributes around user
- Added various bug fixes and optimizations

v4.0.1

- Added support of circle questions
- Added various bug fixes and optimizations

v4.0.0

- Added various bug fixes and optimizations
</div>

## Quick Guide

1.  Download Pollfish iOS SDK and unzip it
2.  Import pollfish.framework to your project
3.  Import AdSupport.framework, SystemConfiguration.framework, WebKit.framework and CoreTelephony.framework to your project
4.  Call init function of Pollfish when a view is loaded or in the App’s Delegate
5.  Set to **Release mode** and release in AppStore
6.  Update your privacy policy
7.  Request your account to get verified from Pollfish Dashboard

**or** 

Through CocoaPods:
---

1.  Add a Podfile with Pollfish framework as a pod reference:

```
platform :ios, '9.0'
pod 'Pollfish'
```

You can find latest Pollfish iOS SDK version on CocoaPods [here](https://cocoapods.org/pods/Pollfish)  

2. Run **pod install** on the command line to install  Pollfish cocoapod.
3. Call init function of Pollfish in the App’s Delegate
4. Set to **Release mode** and release in AppStore
5. Update your privacy policy
6. Request your account to get verified from Pollfish Dashboard
<br/>
> **Requirements:** Pollfish framework works with iOS version 9.0+ and XCode9+.  

<br/><br/>

#### Important note on iOS 14 upcoming release

Apple announced a new [transparency framework](https://developer.apple.com/documentation/apptrackingtransparency) that requires changes to iOS apps with the release of iOS 14. Pollfish iOS SDK utilizes Apple's Advertising ID (IDFA) to identify and retarget users with Pollfish surveys. Therefore Pollfish iOS SDK should only be initialized after the relevant tracking permission is granted by the users. You can see an example in code on how to do that in Pollfish Sample Project code [here](https://github.com/pollfish/ios-sdk-pollfish/blob/master/SampleProjectSwift/SampleProjectSwift/FirstViewController.swift)

To continue using Pollfish surveys in your app you’ll need to make the following changes prior to the release of iOS 14:

1. Install the latest Pollfish iOS SDK (version 5.3.0 or later)

2. Add the AppTrackingTransparency permission request to your iOS apps and ask your users to grant access to the IDFA

3. Initialize Pollfish only after the AppTrackingTransparency permission is granted

All of these steps are required for your apps to continue monetizing with Pollfish surveys on iOS 14. 

<br/><br/>

## Steps Analytically

### 1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](//www.pollfish.com/login/publisher)

### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.


### 3\. Add Pollfish framework to your project

Download Pollfish iOS SDK from the website and then in Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.  

The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane).  

**Note: The framework is a folder and you should add the whole folder into your project.**

### 4\. Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework
- SystemConfiguration.framework 
- WebKit.framework (added in Pollfish v4.4.0)

**Note: If your deployment target is less than iOS 7.0, change the AdSupport.framework from Required to Optional.**

<br/>

### or skip steps 3\. and 4\. and go through CocoaPods

Add a Podfile with Pollfish framework as a pod reference:

```
platform :ios, '9.0'
pod 'Pollfish'
```

You can find latest Pollfish iOS SDK version on CocoaPods [here](https://cocoapods.org/pods/Pollfish)  

Run **pod install** on the command line to install  Pollfish cocoapod.

<br/>


### 5\. Embedding Pollfish into your code

<br/>

### 5.1 If you are using Pollfish in Objective C, import Pollfish header

You have to include Pollfish library headers in any file that you will use Pollfish.  

```
#import <Pollfish/Pollfish.h>
```

### or if you are using Pollfish in a Swift project just import the Module

```
import Pollfish
```
<br/>

### 5.2 Initialize Pollfish

A good place to call Pollfish init function is in the application’s delegate applicationDidBecomeActive method. This way it is ensured that Pollfish surveys will be refreshed each time the application will become active. (another placement could be in the viewDidLoad or viewWillAppear methods of a ViewController).

| **Note:** Init function affects the view hierarchy of the app. Therefore it shoud be called from the main thread that created the view hierarchy.

In order to initialize, you need the API key of your app (step 2 above) and also an instance of PollfishParams. PollfishParams has several params that affect the behaviour of Pollfish survey panel.

Below you can see an example on how you can initialize Pollfish with the help of PollfishParams onject:

<span style="text-decoration: underline">Objective-C:</span>
 
```
- (void)applicationDidBecomeActive:(UIApplication *)application 
{
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {
        
        pollfishParams.indicatorPosition=PollFishPositionMiddleRight;
        pollfishParams.indicatorPadding=10;
        pollfishParams.releaseMode= false;
        pollfishParams.offerwallMode= false;
        pollfishParams.rewardMode=false;
        pollfishParams.requestUUID=@"USER_ID";
    }];
    
    [Pollfish initWithAPIKey:@"YOUR_API_KEY" andParams:pollfishParams];
}
```

<span style="text-decoration: underline">Swift:</span>

```
func applicationDidBecomeActive(application: UIApplication) {

  	let pollfishParams = PollfishParams ()
        
        pollfishParams.indicatorPosition=Int32(PollfishPosition.PollFishPositionMiddleRight.rawValue);
        pollfishParams.indicatorPadding=10;
        pollfishParams.releaseMode = false;
        pollfishParams.offerwallMode = false;
        pollfishParams.requestUUID="USER_ID";
        
        Pollfish.initWithAPIKey("YOUR_API_KEY", andParams: pollfishParams);
}
```
<br/>

### 5.2.1 PollfishParams available options (optional)

You can set several params to control the behaviour of Pollfish survey panel within your app wih the use of PollfishParams instance. Below you can see all the available options. 
<br/><br/>
| **Note:** All the params are optional, however you should at least use the **releaseMode** setting to turn your integration in release mode prior uploading to AppStore 
<br/>

No | Description
------------ | -------------
5.2.1 | **.indicatorPosition(PollfishPosition (int))**  <br/> Sets the Position where you wish to place the Pollfish indicator
5.2.2 | **.requestUUID(NSString \*)**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
5.2.3 | **.indicatorPadding(int)** <br/> Sets the padding from the top or the bottom of the view, according to the Position of Pollfish indicator
5.2.4 | **.pollfishViewContainer(UIView \*)**  <br/> Sets a view container that Pollfish surveys will be rendered above it
5.2.5 | **.releaseMode(BOOL)**  <br/> Sets Pollfish SDK to Developer or Release mode
5.2.6 | **.rewardMode(BOOL)**  <br/> Initializes Pollfish in reward mode
5.2.7 | **.surveyFormat(NSString \*)**  <br/> Explicitly requests a specific survey format
5.2.8 | **.offerwallModel(BOOL)**  <br/> Sets Pollfish to offerwall mode
5.2.9 | **.userAttributes(NSMutableDictionary \*)**  <br/> Provides user attributes upfront during initialization

<br/>
#### **5.2.1 .indicatorPosition (PollfishPosition (int))**
This setting sets the Position where you wish to place Pollfish indicator  ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png) Pollfish indicator is shown only if Pollfish is used in a non rewarded mode.

<span style="text-decoration: underline">There are six different options available: </span> 

*   **PollFishPositionBottomLeft**  
*   **PollFishPositionBottomRight**  
*   **PollFishPositionTopLeft**  
*   **PollFishPositionTopRight**  
*   **PollFishPositionMiddleLeft** 
*   **PollFishPositionMiddleRight**  

If you do not set explicity a position for Pollfish indicator, it will appear by default at **PollFishPositionMiddleRight**
<br/><br/>
Below you can see an example on how you can set Pollfish indicator to slide from the top right middle of the screen:
<br/><br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.indicatorPosition=PollFishPositionMiddleRight;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
        
        pollfishParams.indicatorPosition=Int32(PollfishPosition.PollFishPositionMiddleRight.rawValue);
```
<br/>
indicatorPosition param affects also from which side the survey panel will slide-in (Right or Left).
<br/>

#### **5.2.2 .requestUUID (NSString \*)**

Sets a unique id to identify a user and be passed through server-to-server callbacks. You can read more on how to retrieve this param through the callbacks <a href="https://www.pollfish.com/docs/s2s">here</a>.
<br/><br/>
Below you can see an example on how you can pass a requestUUID during initialization:
<br/><br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.requestUUID=@"USER_ID";
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
        
        pollfishParams.requestUUID="USER_ID";
```
<br/>
#### **5.2.3 .indicatorPadding (int)**

Sets padding from the top or the bottom of the screen according to the Position of the Pollfish indicator. Below you can see an example on how to add padding of 50 from the bottom of the screen, prior rendering Pollfish indicator.
<br/><br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.indicatorPadding=50;
	pollfishParams.indicatorPosition=PollFishPositionBottomRight;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
        
        pollfishParams.indicatorPadding=50;
	pollfishParams.indicatorPosition=Int32(PollfishPosition.PollFishPositionBottomRight.rawValue);
```
<br/>
| **Note:** if used in MIDDLE position, padding is calculating from top.**  
<br/>
#### **5.2.4 .pollfishViewContainer (UIView \*)**

Sets a UIView container where Pollfish surveys will be rendered above it. If this param is not set, the SDK will traverse the view hierarchy of the app and render Pollfish surveys on the top view of the root view controller. 

Preferrably you should let the SDK handle the view hierarchy on its own.
<br/><br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.pollfishViewContainer=self.view;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
        
        pollfishParams.pollfishViewContainer=self.view;
```
<br/>
#### **5.2.5 .releaseMode (BOOL)**

Sets Pollfish SDK to Developer or Release mode. If you do not set this param it will turn the SDK to Developer mode by default in order for the developer to be able to test with test surveys.

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing - always returns a survey).  
*   **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

| **Note:** Be careful to set releaseMode parameter to true prior releasing to AppStore!  
<br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.releaseMode=true;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
        
        pollfishParams.releaseMode=true;
```
<br/>
#### **5.2.6 .rewardMode (BOOL)**

Initializes Pollfish in reward mode. This means that Pollfish Indicator will not be shown and Pollfish survey panel will be automatically hidden until the publisher explicitly calls Pollfish show function. This behaviour enables the option for the publisher, to show a custom prompt to incentivize the user to participate to the survey.

If not set, the default value is false and Pollfish indicator is shown.
<br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.rewardMode=true;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
        
        pollfishParams.rewardMode=true;
```
<br/>
You can read more on how you can use the rewardMode to incentivize users to participate to surveys in the following <a href="https://www.pollfish.com/docs/rewarded-surveys">link</a>.
<br/>
#### **5.2.7 .surveyFormat (NSString \*)**

Explicitly requests a specific survey format for testing purposes.

| **Note:** This param is ignored when offerwall mode is true 

If you want to test Pollfish different available Survey Formats you can  request a specific survey format during initialization

There are four different options available: 

* **SurveyFormatBasic**
* **SurveyFormatPlayful**
* **SurveyFormatRandom**
* **SurveyFormatThirdParty**

Below you can see an example on how you can explicitly request to test Pollfish Plaful Survey Format in debug mode:
<br/><br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.surveyFormat=SurveyFormatBasic;
	pollfishParams.releaseMode=false;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
        
        pollfishParams.surveyFormat=SurveyFormatBasic;
	pollfishParams.releaseMode=false;
```
<br/>

#### **5.2.8 .offerwallModel (BOOL)**

Enables Pollfish in offerwall mode. If not specified Pollfish is shown as one survey at a time.

Below you can see an example on how you can intialize Pollfish in offerwall mode in an incentivized integration:
<br/><br/>
<span style="text-decoration: underline">Objective-C:</span>
```
    PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
        pollfishParams.offerwallModel=true;
	pollfishParams.rewardMode=true;
	pollfishParams.releaseMode=false;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
	let pollfishParams = PollfishParams ()
	
	pollfishParams.offerwallModel=true;
	pollfishParams.rewardMode=true;
	pollfishParams.releaseMode=false;
```
<br/>
#### **5.2.9 .userAttributes(NSMutableDictionary \*)**

Passing user attributes to skip or shorten Pollfish Demographic surveys.

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and archieve better fill rate and higher priced surveys.

| **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default.

an example of how you can create and pass a user attributes dictionary during initialization can be the following below:
<br/><br/>
<span style="text-decoration: underline">Objective-C:</span>

```
UserAttributesDictionary *userAttributesDictionary = [[UserAttributesDictionary alloc] init];
    
    [userAttributesDictionary setGender: GENDER(MALE)];
    [userAttributesDictionary setRace:RACE(WHITE)];
    [userAttributesDictionary setYearOfBirth:YEAR_OF_BIRTH(_1984)];
    [userAttributesDictionary setMaritalStatus:MARITAL_STATUS(MARRIED)];
    [userAttributesDictionary setParentalStatus:PARENTAL_STATUS(THREE)];
    [userAttributesDictionary setEducation:EDUCATION_LEVEL(UNIVERSITY)];
    [userAttributesDictionary setEmployment:EMPLOYMENT_STATUS(EMPLOYED_FOR_WAGES)];
    [userAttributesDictionary setCareer:CAREER(TELECOMMUNICATIONS)];
    [userAttributesDictionary setIncome:INCOME(MIDDLE_I)];
    
PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {        
	pollfishParams.userAttributes=userAttributesDictionary;
    }];
```
<span style="text-decoration: underline">Swift:</span>
```
    let userAttributesDictionary:UserAttributesDictionary = [:]
    
    /*included in Demographic Surveys*/
    userAttributesDictionary.setGender(GENDER(MALE));
    userAttributesDictionary.setRace(RACE(WHITE));
    userAttributesDictionary.setYearOfBirth(YEAR_OF_BIRTH(_1984));
    userAttributesDictionary.setMaritalStatus(MARITAL_STATUS(MARRIED));
    userAttributesDictionary.setParentalStatus(PARENTAL_STATUS(THREE));
    userAttributesDictionary.setEducation(EDUCATION_LEVEL(UNIVERSITY));
    userAttributesDictionary.setEmployment(EMPLOYMENT_STATUS(EMPLOYED_FOR_WAGES));
    userAttributesDictionary.setCareer(CAREER(TELECOMMUNICATIONS));
    userAttributesDictionary.setIncome(INCOME(MIDDLE_I));
    
    let pollfishParams = PollfishParams ()
	
    pollfishParams.userAttributes=userAttributesDictionary;
    
```


<br/>
**At this point you are ready to go live! Turn your app to Release mode by setting releaseMode:true and submit your app to AppStore.**
<br/><br/>
### 6\. Distributing your app to AppStore

Pollfish uses Advertising Identifier (IDFA) for survey distribution and therefore when submitting your app to the App you should select the following options as seen in the image below:  

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/idfa_3.png"/>

<br/>

### 7\.  Update your Privacy Policy

Add the following paragraph to your app's privacy policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*  

*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”*

<br/><br/>

---
<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>
<br/><br/><br/>

| **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process that users need to go through, in order to join the platform. If a paid survey is available at that point of time, the demographic questions will be inserted at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this type of targeting.


<br/>

<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>
<br/>


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 9 - "Passing user attributes to skip or shorten Pollfish Demographic surveys" and skip or shorten this way, Pollfish Demographic surveys.



<br/>

### 8\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>
<br/>


## Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour like listening and acting on different  notifications. All the steps below are optional.
<br/>
<br/>

### 9\. Handling orientation changes (optional)

Pollfish SDK does not handle by default different orientation changes. If your app supports more than one orientations you should register and get notified when a device is roated and re-init Pollfish.

For example:

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(appRotated) name:UIDeviceOrientationDidChangeNotification object:nil];
```
```
-(void) appRotated{
    // Pollfish re-init
}
```
<span style="text-decoration: underline">Swift:</span>
 
```
NotificationCenter.default.addObserver(forName: UIDevice.orientationDidChangeNotification,
                                               object: nil,
                                               queue: nil,
                                               using:appRotated)
```
```
func appRotated(_ notification:Notification){
    // Pollfish re-init
}
```
<br/>
### 10\. Manually show or hide Pollfish (optional)

You can manually hide and show Pollfish from your various UIVIewControllers. by calling anywhere after initialization:  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish show];
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.show()
```

or  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish hide];
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.hide()
```


For example:  

<span style="text-decoration: underline">Objective-C:</span>

```
// MyViewController1
- (void)viewWillAppear:(BOOL)animated
{
    // ...
    [Pollfish hide];
}

// MyViewController2
- (void)viewWillAppear:(BOOL)animated
{
    // ...
    [Pollfish show];
}
```

<span style="text-decoration: underline">Swift:</span>

```
// MyViewController1
override func viewWillAppear(animated: Bool) 
{
    super.viewWillAppear(animated)
  
    // ...
    Pollfish.hide()
}

// MyViewController2
override func viewWillAppear(animated: Bool) 
{
    super.viewWillAppear(animated)
    
    // ...
    Pollfish.hide()
}
```
<br/>

### 11\. Update user location (optional)

You can update user’s location anytime after initialization to get better fill rate on surveys by calling the following:  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish updateLocationWith:(CLocation *) location];
```

<span style="text-decoration: underline">Swift:</span>

```
 Pollfish.updateLocationWith(location: CLLocation!);
```
<br/>

### 12\. Send beacon information (optional)

You can send beacon information if available anytime after initialization to get to be eligible for receiveing beacon surveys by calling the following:  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish sendBeaconInfo:(CLBeacon *)beacon];
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.sendBeaconInfo(beacon: CLBeacon!);
```
<br/>

### 13\.Implement Pollfish event listeners (optional)

> **Note:** Pollfish listeners/notifications fire in an asynchronous way. Having said that it's possible that you receive them while being in a background thread and not the main UI thread. If you want to make any prompts or custom changes on the view level when you receive those notifications, please be sure to make them on the main UI thread

### 14.1 Get notified when a survey is received


You can be notified when a survey is received via the iOS Notification Center. Note that the observer should be already registered when a survey is received in order to run the selector.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishReceived:) name:@"PollfishSurveyReceived" object:nil];
```

```
- (void)pollfishReceived:(NSNotification *)notification
{
    int surveyPrice = [[[notification userInfo] valueForKey:@"survey_cpa"] intValue];
    int surveyIR = [[[notification userInfo] valueForKey:@"survey_ir"] intValue];
    int surveyLOI = [[[notification userInfo] valueForKey:@"survey_loi"] intValue];
    
    NSString *surveyClass =[[notification userInfo] valueForKey:@"survey_class"];
    
    NSString *rewardName = [[notification userInfo] valueForKey:@"reward_name"];
    int rewardValue = [[[notification userInfo] valueForKey:@"reward_value"] intValue];
    
    NSLog(@"Pollfish: Survey Received - SurveyPrice:%d andSurveyIR: %d andSurveyLOI:%d andSurveyClass:%@ andRewardName:%@ andRewardValue:%d", surveyPrice,surveyIR, surveyLOI, surveyClass, rewardName, rewardValue);
}
```

<span style="text-decoration: underline">Swift:</span>

```
NotificationCenter.default.addObserver(forName: NSNotification.Name(rawValue: "PollfishSurveyReceived"),
                                               object: nil,
                                               queue: nil,
                                               using:pollfishReceived)
```

```
func pollfishReceived(_ notification:Notification) {
        
        if let userInfo : [AnyHashable: Any] = (notification.userInfo) {
      
            let surveyPrice = userInfo["survey_cpa"]
            let surveyIR =  userInfo["survey_ir"]
            let surveyLOI =  userInfo["survey_loi"]
            let surveyClass =  userInfo["survey_class"]
            
            let rewardName = userInfo["reward_name"]
            let rewardValue = userInfo["reward_value"]
            
            print("Pollfish Survey  Received - SurveyPrice: \(String(describing: surveyPrice)) andSurveyIR: \(String(describing: surveyIR)) andSurveyLOI: \(String(describing: surveyLOI)) andSurveyClass: \(String(describing: surveyClass)) andRewardName: \(String(describing: rewardName)) andRewardValue:\(String(describing: rewardValue))")

        }else{         
            print("Pollfish Survey Received")
	}
}
```


As you may see in the example above you can get informed for the following values by listening and reading the relevant notification object: 

| **Note:** This notification object, when offerwall mode is enabled, it returns an empty userInfo object. It just notifies that surveys are available within the offerwall.

- **survey_cpa** : money to be earned from survey received in US dollar cents (estimated based on daily exchange currency)
- **survey_ir** : the current estimation for the survey incidence rate as an integer number in the range 0-100. This param is optional and will have as default the value -1 if it was not set and the IR was not computed reliably.
- **survey_loi** : the expected time in minutes that it takes to complete the survey. This param is optional and will have as default the value -1 if it was not set and the LOI wan not computed reliably.
- **survey_class** :  information about the survey network and type* 
- **reward_name** :  a virtual reward name as specified on Developer Dashboard* 
- **reward_vale** :  a virtual reward value as caluclated via a given echange rate on Developer Dashboard.* 

* The syntax for survey_class values is:

```
survey_class: provider["/"type]
provider: "Pollfish" | "Toluna" | "Cint" | "Lucid" | "InnovateMR" | "SaySo" | "P2Sample"
type: "Basic" | "Playful" | "ThirdParty" | "Demographics" | "Internal"
```

that is a network name followed by an optional slash and survey type.

The provider is the network that provides the survey. The syntax rule has all the networks currently supported by Pollfish.

The type is that of the survey as described in the network's documentation. The exception is the type "Demographics" which
is always used to identify surveys whose purpose is to collect demographic data for the users.

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

<br/>
### 14.2 Get notified when a survey is completed

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishCompleted:) name:@"PollfishSurveyCompleted" object:nil];
```

```
- (void)pollfishCompleted:(NSNotification *)notification
{
    int surveyPrice = [[[notification userInfo] valueForKey:@"survey_cpa"] intValue];
    int surveyIR = [[[notification userInfo] valueForKey:@"survey_ir"] intValue];
    int surveyLOI = [[[notification userInfo] valueForKey:@"survey_loi"] intValue];
    
    NSString *surveyClass =[[notification userInfo] valueForKey:@"survey_class"];
    
    NSString *rewardName = [[notification userInfo] valueForKey:@"reward_name"];
    int rewardValue = [[[notification userInfo] valueForKey:@"reward_value"] intValue];
    
    
    NSLog(@"Pollfish: Survey Completed - SurveyPrice:%d andSurveyIR: %d andSurveyLOI:%d andSurveyClass:%@ andRewardName:%@ andRewardValue:%d", surveyPrice,surveyIR, surveyLOI, surveyClass, rewardName, rewardValue);
}
```
<span style="text-decoration: underline">Swift:</span>

```
NotificationCenter.default.addObserver(forName: NSNotification.Name(rawValue: "PollfishSurveyCompleted"),
                                               object: nil,
                                               queue: nil,
                                               using:pollfishCompleted)
```

```
func pollfishCompleted(_ notification:Notification) {

   if let userInfo : [AnyHashable: Any] = (notification.userInfo) {
            
            let surveyPrice = userInfo["survey_cpa"]
            let surveyIR =  userInfo["survey_ir"]
            let surveyLOI =  userInfo["survey_loi"]
            let surveyClass =  userInfo["survey_class"]
            
            let rewardName = userInfo["reward_name"]
            let rewardValue = userInfo["reward_value"]
            
            print("Pollfish Survey  Completed - SurveyPrice: \(String(describing: surveyPrice)) andSurveyIR: \(String(describing: surveyIR)) andSurveyLOI: \(String(describing: surveyLOI)) andSurveyClass: \(String(describing: surveyClass)) andRewardName: \(String(describing: rewardName)) andRewardValue:\(String(describing: rewardValue))")

        }else{
            
            print("Pollfish Survey Completed")
        }
}
```


Similarly to survey received notification, upon completion you can get informed on the following values around the completed survey

- **survey_cpa** : money to be earned from survey received in US dollar cents (estimated based on daily exchange currency)
- **survey_ir** : the current estimation for the survey incidence rate as an integer number in the range 0-100. This param is optional and will have as default the value -1 if it was not set and the IR was not computed reliably.
- **survey_loi** : the expected time in minutes that it takes to complete the survey. This param is optional and will have as default the value -1 if it was not set and the LOI wan not computed reliably.
- **survey_class** :  information about the survey network and type* 
- **reward_name** :  a virtual reward name as specified on Developer Dashboard* 
- **reward_vale** :  a virtual reward value as caluclated via a given echange rate on Developer Dashboard.* 
<br/>
### 14.3 Get notified when a user is not eligible for a Pollfish survey


You can be notified when a user is not eligible for a Pollfish survey after accepting to take one, via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishUsernotEligible) name:@"PollfishUserNotEligible" object:nil];
```

```
- (void)pollfishUsernotEligible
{
    NSLog(@"Pollfish User Not Eligible");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NotificationCenter.default.addObserver(forName: NSNotification.Name(rawValue: "PollfishUserNotEligible"),
                                               object: nil,
                                               queue: nil,
                                               using:pollfishUsernotEligible)
```

```
func pollfishUsernotEligible(_ notification:Notification) 
{
     print("Pollfish User Not Eligible")
}
```

<br/>
### 14.4 Get notified when no survey is available


You can be notified when a survey is not available for a user via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishNotAvailable) name:@"PollfishSurveyNotAvailable" object:nil];
```

```
- (void) surveyNotAvailable
{
    NSLog(@"Pollfish Survey Not Available!");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NotificationCenter.default.addObserver(forName: NSNotification.Name(rawValue: "PollfishSurveyNotAvailable"),
                                               object: nil,
                                               queue: nil,
                                               using:pollfishNotAvailable)
```

```
func pollfishNotAvailable(_ notification:Notification) 
{
     print("Pollfish Survey Not Available!")
}
```

<br/>
### 14.5 Get notified when Pollfish panel has opened


You can be notified when a user opens Pollfish survey panel via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishOpened) name:@"PollfishOpened" object:nil];
```

```
- (void)pollfishOpened
{
    NSLog(@"Pollfish is opened!");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NotificationCenter.default.addObserver(forName: NSNotification.Name(rawValue: "PollfishOpened"),
                                               object: nil,
                                               queue: nil,
                                               using:pollfishOpened)
```

```
func pollfishOpened(_ notification:Notification)
{
     print("Pollfish is opened!")
}
```

<br/>
### 14.6 Get notified when Pollfish panel has closed


You can be notified when a user closes Pollfish survey panel via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishClosed) name:@"PollfishClosed" object:nil];
```

```
- (void)pollfishClosed
{
    NSLog(@"Pollfish is closed!");
} 
```

<span style="text-decoration: underline">Swift:</span>

```
NotificationCenter.default.addObserver(forName: NSNotification.Name(rawValue: "PollfishClosed"),
                                               object: nil,
                                               queue: nil,
                                               using:pollfishClosed)
```

```
func pollfishClosed(_ notification:Notification)
{
     print("Pollfish is closed!")
}
```

<br/>

### 14.7 Get notified when a user rejected a survey (added in Pollfish v4.4.0)


You can be notified when a user rejected a survey via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishUserRejectedSurvey) name:@"PollfishUserRejectedSurvey" object:nil];
```

```
- (void)pollfishUserRejectedSurvey
{
    NSLog(@"Pollfish User Rejected Survey");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NotificationCenter.default.addObserver(forName: NSNotification.Name(rawValue: "PollfishUserRejectedSurvey"),
                                               object: nil,
                                               queue: nil,
                                               using:pollfishUserRejectedSurvey)
```

```
func pollfishUserRejectedSurvey(_ notification:Notification)
{
     print("Pollfish User Rejected Survey")
}
```

<br/>

### 15\. Check if Pollfish survey is still available on your device (optional)

It happens that time had past since you initialized Pollfish and a survey is received. If you want to check if survey is still avaialble on your device and has not expired you can check by calling:

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish isPollfishPresent]
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.isPollfishPresent()
```

<br/>




