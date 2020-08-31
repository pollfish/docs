<div class="changelog" data-version="5.3.1.1">
v.5.3.1.1

- Updated with Pollfish iOS SDK 5.3.1

v.5.2.5.2

- Updated User Not Eligible listener behaviour

v.5.2.5.1

- Updated with Pollfish iOS SDK 5.2.5

v.5.2.4.1

- Updated with Pollfish iOS SDK 5.2.4

v.5.2.3.1

- Updated with Pollfish iOS SDK 5.2.3
- Updated User Rejection listener behaviour

v.5.2.2.1

- Updated with Pollfish iOS SDK 5.2.2

v.5.2.1.1

- Updated with Pollfish iOS SDK 5.2.1

v.5.1.0.2

- Initial release

</div>

This guide is for publishers looking to use AdMob mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

##### Prerequisites

iOS 9.0 or later

</br>

#### Important note on iOS 14 upcoming release

Apple announced a new [transparency framework](https://developer.apple.com/documentation/apptrackingtransparency) that requires changes to iOS apps with the release of iOS 14. Pollfish iOS SDK utilizes Apple's Advertising ID (IDFA) to identify and retarget users with Pollfish surveys. Therefore Pollfish iOS SDK should only be initialized after the relevant tracking permission is granted by the users. You can see an example in code on how to do that in Pollfish Sample Project code [here](https://github.com/pollfish/ios-sdk-pollfish/blob/master/SampleProjectSwift/SampleProjectSwift/FirstViewController.swift)

To continue using Pollfish surveys in your app you’ll need to make the following changes prior to the release of iOS 14:

1. Install the latest Pollfish iOS SDK (version 5.3.0 or later)

2. Add the AppTrackingTransparency permission request to your iOS apps and ask your users to grant access to the IDFA

3. Initialize Pollfish ONLY after the AppTrackingTransparency permission is granted

All of these steps are required for your apps to continue monetizing with Pollfish surveys on iOS 14. 

<br/><br/>

Below you can find a step by step guide on how to incorporate Pollfish surveys with AdMob mediation:

### Step 1: Implement AdMob Rewarded Ads in your app 

If you have not implemented [Rewarded Ads](https://developers.google.com/admob/ios/rewarded-ads) in your app yet, you can follow the documentation Implement as described by AdMob. 

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

First you need to sign in to your [AdMob account](https://apps.admob.com/). In your app you can click on **Ad Units** and then **ADD AD UNITS** and select **Rewarded** Ads

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/ad_unit_ios.png"/>
<br/>


In the configuration of the Ad Unit popup you can specify a name for your rewarded placement and then a name for the reward and a value. If you want to apply the same reward to the user no matter which ad network is served, check the **Apply to all networks in Mediation Groups** box.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/rewarded_ad_unit_ios.png"/>
<br/>

If you don't apply this setting, the Pollfish adapter will provide a dynamic value as you specified it on your Pollfish Dashboard, in the App Settings area, based on the actual price of each survey completed.


### Step 2: Configure Mediation Settings for your AdMob Rewarded Ad unit

You need to add Pollfish to the mediation configuration for your Rewarded Ad unit. 

Log in to your AdMob account. On the left side menu, click on the **Mediation** and then in **Mediation Groups** Tab. If you already have an existing Mediation Group you will need to modify it (click on the name of the Mediation Group and press **Edit**).

if you do not have a Mediation Group yet, click to create one with **CREATE MEDIATION GROUP**.

In the Ad Format drop down menu select **Rewarded** and for platform **iOS**


<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/created_ios.png"/>
<br/>

and then you can name the Mediation Group if you do not have one already. Next, set the mediation group status to **Enabled**

Afterwards you should click **ADD AD UNITS** and associate the Mediation group with an existing AdMob Rewarded Ad unit.

You should now see the ad units card populated with the ad units you selected, as shown below:

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/ad_units_ios.png"/>
<br/>
You then have to add Pollfish Network to the Mediationn Waterfall of the group. Click on **ADD CUSTOM EVENT**

You can add a name to differentiate Pollfish Network from your other ad sources (for example Pollfish Netowrk) and an estimated eCPM. Pollfish surveys average eCPMs, range betweenn $70-$80.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/custom_event_aa.png"/>
<br/>

You can then configure Pollfish ad unit by adding the class name of Pollfish AdMob Mediation Adapter

**Class Name:** GADMediationAdapterPollfish<br/>
**Parameter:** JSON with Pollfish SDK configuration prams (optional)

Users can pass a **JSON string** to provide the necessary params for Pollfish SDK to work (similarly they can pass those params as described in Step 5. 

No | Key | Type
------------ | -------------| -------------
2.1 | **api_key**  <br/> Sets Pollfish SDK API key as provided by Pollfish | String
2.2 | **release_mode**  <br/> Sets Pollfish SDK to Developer or Release mode | Bool
2.3 | **request_uuid**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks | String

Example:

```
{"api_key":"Pollfish API Key", "release_mode":true, "request_uuid":"My user id"}
```

> **Note:** Pollfish SDK works by default in production mode. If you would like to test with test surveys you should use release_mode false or explicitly request that in code as described in Step 5.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/pollfish_ios_mediation.png"/>
<br/>


### Step 3: Set Up Pollfish

#### 3.1\. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

#### 3.2\. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

#### 3.3\.  Add Pollfish framework to your project

Download Pollfish iOS SDK from the website and then in Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.  

The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane).  

**Note: The framework is a folder and you should add the whole folder into your project.**

#### 3.4\. Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework
- SystemConfiguration.framework 
- WebKit.framework (added in Pollfish v4.4.0)

**Note: If your deployment target is less than iOS 7.0, change the AdSupport.framework from Required to Optional.**

<br/>

#### or skip steps 3.3 and 3.4 and go through CocoaPods

Add a Podfile with Pollfish framework as a pod reference:

```
platform :ios, '9.0'
pod 'Pollfish'
```

You can find latest Pollfish iOS SDK version on CocoaPods [here](https://cocoapods.org/pods/Pollfish)  

Run **pod install** on the command line to install  Pollfish cocoapod.

<br/>

### Step 4: Add Pollfish AdMob Adapter to your project

Download Pollfish iOS AdMob Adapter framework and then in Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.

**OR**

#### **Retrieve Pollfish AdMob Adapter through CocoaPods**

Add a Podfile with Pollfish framework as a pod reference:

```
pod 'PollfishAdMobAdapter'
```
You can find latest Pollfish iOS SDK version on CocoaPods here

Run pod install on the command line to install Pollfish cocoapod.


### Step 5: Use and control Pollfish AdMob Adapter in your Rewarded Ad Unit 

Pollfish AdMob Adapter provides different options that you can use to control the behaviour of Pollfish SDK.

<br/>
Below you can see all the available options of **GADPollfishRewardedNetworkExtras** instance that is used to configure the behaviour of Pollfish SDK.

<br/>

No | Description
------------ | -------------
5.1 | **.pollfishAPIKey**  <br/> Sets Pollfish SDK API key as provided by Pollfish
5.2 | **.requestUUID**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
5.3 | **.releaseMode**  <br/> Sets Pollfish SDK to Developer or Release mode


#### 5.1 .pollfishAPIKey

Pollfish API Key as provided by Pollfish on  [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign up to the platform.  If you have already specified Pollfish API Key on AdMob's UI, this param will be ignored.

#### 5.2 .requestUUID

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

#### 5.3 .releaseMode

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish AdMob Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

Below you can see an example on how you can use GADPollfishRewardedNetworkExtras to pass info to Pollfish AdMob Adapter:
```
#import <PollfishAdMobAdapter/GADPollfishRewardedNetworkExtras.h>
```
</br>
```
GADRequest *request = [GADRequest request];
    
GADPollfishRewardedNetworkExtras *pollfishNetworkExtras = [[GADPollfishRewardedNetworkExtras alloc] init];
    
pollfishNetworkExtras.pollfishAPIKey = @"POLLFISH_API_KEY";
pollfishNetworkExtras.releaseMode = false;
pollfishNetworkExtras.requestUUID = @"YOUR_USER_ID";
    
[request registerAdNetworkExtras:pollfishNetworkExtras];
```

### Step 6: Publish your app on the store

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option.
