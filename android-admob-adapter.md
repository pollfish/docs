<div class="changelog" data-version="6.2.5.0">
v6.2.5.0

- Updated with Pollfish Android SDK v6.2.5

v6.2.4.2

- Internal fixes

v6.2.4.1

- Internal fixes

v6.2.4.0

- Updated with Pollfish Android SDK v6.2.4

v6.2.3.0

- Updated with Pollfish Android SDK v6.2.3

v6.2.2.0

- Updated with Pollfish Andorid SDK v6.2.2

v6.2.1.0

- Updated with Pollfish Android SDK v6.2.1

v6.2.0.0

- Updated with Pollfish Android SDK v6.2.0

v6.1.6.0

- Updated with Pollfish Android SDK v6.1.6

v6.1.5.1

- Internal fixes

v6.1.5.0

- Updated with Pollfish Android SDK v6.1.5

v6.1.4.0

- Updated with Pollfish Android SDK v6.1.4

v6.1.3.0

- Updated with Pollfish Android SDK v6.1.3

v6.1.2.0

- Updated with Pollfish Andorid SDK v6.1.2

v6.1.1.0
	
- Updated with Pollfish Android SDK v6.1.1
	
v6.1.0.0

- Updated with Pollfish Android SDK v6.1.0

v6.0.4.0

- Updated with Pollfish Android SDK v6.0.4

v6.0.3.0

- Update with Pollfish Android SDK V6.0.3

v6.0.2.0
	
- Updated with Pollfish Android SDK v6.0.2
- Added build support for Android SDK lower than 21
- Updated with Google Play Ads v20

v5.6.0.1
	
- Updated with Pollfish Android SDK v5.6.0

v5.5.1.0
	
- Updated with Pollfish Android SDK v5.5.1

v5.4.1.0
	
- Updated with Pollfish Android SDK v5.4.1

v5.3.3.2
	
- Removed close notifications from User Rejected and User Not Eligible callbacks

v5.3.3.1
	
- Updated with Android SDK v5.3.3 

v5.3.2.1
	
- Updated with Android SDK v5.3.2 

v5.3.0.1
	
- Added functionality to render on top of called Activity 
- Updated with Android SDK v5.3.0

v5.2.0.1
	
- Fixed issues with view hierarchy
- Updated with Android SDK v5.2.0

v5.1.0.3
	
- Updated User Not Eligible listener behaviour	
	
v5.1.0.2
	
- Updated User Rejection listener behaviour

v5.1.0.1.
	
- Updated to Pollfish SDK v5.1.0.1
- Added check to dismiss multiple initializations when Pollfish panel is open
- Added JSON support for parameter retrieved from AdMob's UI

v5.0.2.1
	
- Initial Release

</div>

This guide is for publishers looking to use AdMob mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

<br/>

# Prerequisites

* [Pollfish Developer Account](https://www.pollfish.com/dashboard/dev/)
* [AdMob Account](https://apps.admob.com/)
* Android API 21 or later
* Java version 1.8

<br/>

> **Note:** Apps designed for [Children and Families program](https://play.google.com/about/families/ads-monetization/) should not be using Pollfish SDK, since Pollfish does not collect responses from users less than 16 years old    

> **Note:** Pollfish SDK requires minSdk 21. If your app supports a lower minSdk you can still build your app.

<details><summary> ➤ For apps with minSDK lower than 21 please follow the steps here (Click to expand)</summary>

**AndroidManifest.xml**

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    ... >

    <uses-sdk tools:overrideLibrary="com.pollfish" />

    <application
	... >
        ...
    </application>
```

**app/build.gradle**

```groovy
defaultConfig {
    ...
    multiDexEnabled true
}

dependencies {
    ...
    implementation 'androidx.multidex:multidex:2.0.1'
}
```
</details>

</br>

# Quick Guide

* Set up AdMob Rewarded Ads
* Set up Pollfish
* Add Pollfish AdMob Adapter to your project
* Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Pollfish surveys with AdMob mediation:

## 1. Set up AdMob Rewarded Ads

### 1.1. Create a Rewarded Ad Unit

If you have not implemented [Rewarded Ads](https://developers.google.com/admob/android/rewarded-ads) in your app yet, you can follow the documentation Implement as described by AdMob. 

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

First you need to sign in to your [AdMob account](https://apps.admob.com/). In your app you can click on **Ad Units** and then **ADD AD UNITS** and select **Rewarded** Ads

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/create_ad_unit.png"/>

<br/>

In the configuration of the Ad Unit popup you can specify a name for your rewarded placement and then a name for the reward and a value. If you want to apply the same reward to the user no matter which ad network is served, check the **Apply to all networks in Mediation Groups** box.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/configure_ads.png"/>

<br/>

If you don't apply this setting, the Pollfish adapter will provide a dynamic value as you specified it on your Pollfish Dashboard, in the **App Settings** area, based on the actual price of each survey completed.

<br/>

### 1.2 Configure Mediation Settings for your AdMob Rewarded Ad unit

You need to add Pollfish to the mediation configuration for your Rewarded Ad unit. 

Log in to your AdMob account. On the left side menu, click on the **Mediation** and then in **Mediation Groups** Tab. If you already have an existing Mediation Group you will need to modify it (click on the name of the Mediation Group and press **Edit**).

if you do not have a Mediation Group yet, click to create one with **CREATE MEDIATION GROUP**.

In the Ad Format drop down menu select **Rewarded** and for platform **Android**

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/new_mediation_group.png"/>

<br/>

and then you can name the Mediation Group if you do not have one already. Next, set the mediation group status to **Enabled**

Afterwards you should click **ADD AD UNITS** and associate the Mediation group with an existing AdMob Rewarded Ad unit.

You should now see the ad units card populated with the ad units you selected, as shown below:

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/ad_units.png"/>

<br/>

You then have to add Pollfish Network to the Mediation Waterfall of the group. Click on **ADD CUSTOM EVENT**

You can add a name, in the **Label** section, to differentiate Pollfish Network from your other ad sources (for example Pollfish Netowrk) and an estimated eCPM. Pollfish surveys average eCPMs, range usually betweenn $70-$80.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/custom_event_aa.png"/>

<br/>

You can then configure Pollfish ad unit by adding the class name of Pollfish AdMob Mediation Adapter

**Class Name:** com.pollfish.mediation.PollfishAdMobAdapter<br/>
**Parameter:** JSON with Pollfish SDK configuration prams (optional)

Users can pass a **JSON string** to provide the necessary params for Pollfish SDK to work (similarly they can pass those params as described in Step 5. 

Key | Type
------------ | -------------
**`api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish | String
**`release_mode`** <br/> Sets Pollfish SDK to Developer or Release mode | Boolean
**`request_uuid`** <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks | String
**`offerwall_mode`** <br/> Sets Pollfish SDK to Offerwall Mode | Boolean

Example:

```json
{
    "api_key": "Pollfish API Key", 
    "release_mode": true, 
    "request_uuid": "My user id",
    "offerwall_mode": false
}
```

> **Note:** Pollfish SDK works by default in production mode. If you would like to test with test surveys you should use release_mode false or explicitly request that in code as described in Step 5.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/sdk/iOS/add_android_class.png"/>

<br/>

### 1.3 Add Google Play Ads to your project

Applications that integrate Pollfish SDK are required to include Google Play Services library in order to give access to the Advertising ID of a device to the SDK. Further details regarding integration with the Google Play services library can be found [here](https://developers.google.com/android/guides/setup).

```java
dependencies {
    implementation 'com.google.android.gms:play-services-ads:20.6.0'
}
```

<br/>

**Android 12**

Apps updating their target API level to 31 (Android 12) or higher will need to declare a Google Play services normal permission in the AndroidManifest.xml file.

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

You can read more about Google Advertising ID changes [here](https://support.google.com/googleplay/android-developer/answer/6048248).


<br/>

## 2. Set Up Pollfish

### 2.1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

<br/>

### 2.2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

<br/>

### 2.3. Add Pollfish SDK to your project

Download Pollfish Android SDK or reference it through maven().

**Download Pollfish Android SDK**

Click [here](https://storage.googleapis.com/pollfish_production/sdk/Android/Pollfish%20Google%20Play%20Android%20SDK-6.2.5.zip) to download the latest version of Pollfish Android SDK 

**Import Pollfish `.aar` file to your project libraries**

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**Integrate Google Play Services to your project**

Applications that integrate Pollfish SDK are required to include Google Play Services library in order to give access to the Advertising ID of a device to the SDK. Further details regarding integration with the Google Play services library can be found [here](https://developers.google.com/android/guides/setup).

```groovy
dependencies {
    implementation 'com.google.android.gms:play-services-ads-identifier:17.0.0'
}
```

**OR**

**Retrieve Pollfish Android SDK through maven()**

Retrieve Pollfish through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```groovy
dependencies {
  implementation 'com.pollfish:pollfish-googleplay:6.2.5'
}
```

<br/>

## 3. Add Pollfish AdMob Adapter to your project

Import Pollfish AdMob Adapter **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish AdMob Adapter aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

#### **Retrieve Pollfish AdMob Adapter through maven()**

Retrieve Pollfish through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```groovy
dependencies {
  implementation 'com.pollfish.mediation:pollfish-admob:6.2.5.0'
}
```

<br/>

## 4. Request for a RewardedAd

Import the following packages

<span style="text-decoration:underline">Kotlin</span>

```kotlin
import com.google.android.gms.ads.AdError;
import com.google.android.gms.ads.AdRequest;
import com.google.android.gms.ads.FullScreenContentCallback;
import com.google.android.gms.ads.LoadAdError;
import com.google.android.gms.ads.MobileAds;
import com.google.android.gms.ads.rewarded.RewardedAd;
import com.google.android.gms.ads.rewarded.RewardedAdLoadCallback;
```

<span style="text-decoration:underline">Java</span>

```java
import com.google.android.gms.ads.AdError;
import com.google.android.gms.ads.AdRequest;
import com.google.android.gms.ads.FullScreenContentCallback;
import com.google.android.gms.ads.LoadAdError;
import com.google.android.gms.ads.MobileAds;
import com.google.android.gms.ads.rewarded.RewardedAd;
import com.google.android.gms.ads.rewarded.RewardedAdLoadCallback;
```

<br/>

Initialize AdMob SDK by calling `MobileAds.initialize` method passing a `Context` and an `OnInitializationCompleteListener` listener as arguments.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    ...

    MobileAds.initialize(this) {
        // Initialization completed
        createAndLoadRewardedAd()
    }
}
```

<span style="text-decoration:underline">Java</span>

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    ...

    MobileAds.initialize(this, initializationStatus -> {
        // Initialization completed
        createAndLoadRewardedAd();
    });
}
```

Request a Rewarded A from AdMob by calling `RewardedAd.load` passing a `Context`, you `AD_UNIT_KEY`, an `AdRequest` object instance and a `RewardedAdLoadCallback` abstract class implementation as arguments.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
val adRequest = AdRequest.Builder().build()

RewardedAd.load(this, "AD_UNIT_KEY", adRequest, object : RewardedAdLoadCallback() {
    override fun onAdLoaded(rewardedAd: RewardedAd) {
        
        rewardedAd.fullScreenContentCallback = object : FullScreenContentCallback() {
            override fun onAdFailedToShowFullScreenContent(adError: AdError) {}

            override fun onAdShowedFullScreenContent() {}

            override fun onAdDismissedFullScreenContent() {}
        }
    }

    override fun onAdFailedToLoad(loadAdError: LoadAdError) {}
})
```

<span style="text-decoration:underline">Java</span>

```java
AdRequest request = new AdRequest.Builder().build();

RewardedAd.load(this, "AD_UNIT_KEY", request, new RewardedAdLoadCallback() {

    @Override
    public void onAdLoaded(@NonNull RewardedAd rewardedAd) {
        mRewardedAd.setFullScreenContentCallback(new FullScreenContentCallback() {
            @Override
            public void onAdFailedToShowFullScreenContent(@NonNull AdError adError) {}

            @Override
            public void onAdShowedFullScreenContent() {}

            @Override
            public void onAdDismissedFullScreenContent() {}
        });
    }

    @Override
    public void onAdFailedToLoad(@NonNull LoadAdError loadAdError) {}

});
```

When the Rewarded Ad is ready, present the ad by invoking `rewardedAd.show` passing an `Activity` and a reward completion block. Just to be sure, you can combine show with a check to see if the Ad you are about to show is actually ready.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
mRewardedAd?.show(this) { reward: RewardItem ->
    // Reward received
}
```

<span style="text-decoration:underline">Java</span>

```java
if (mRewardedAd != null) {
    mRewardedAd.show(MainActivity.this, reward -> {
        // Reward received
    });
}
```

<br/>

## 5. Publish your app on the store

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option.

<br/>

# Optional section

## 6. Configure programmatically Pollfish SDK behaviour

Pollfish AdMob Adapter provides different options that you can use to control the behaviour of Pollfish SDK. This configuration, if applied, will override any configuration done in AdMob's dashboard.

<br/>

Below you can see all the available options of **PollfishExtrasBundleBuilder** instance that is used to configure the behaviour of Pollfish SDK.

<br/>

No | Description | Type
------------ | ------------- | ----
6.1 | **`.setAPIKey(String apiKey)`**  <br/> Sets Pollfish SDK API key as provided by Pollfish | String
6.2 | **`.setRequestUUID(String requestUUID)`**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks | String
6.3 | **`.setReleaseMode(boolean releaseMode)`**  <br/> Sets Pollfish SDK to Developer or Release mode | Boolean
6.4 | **`.setOfferwallMode(boolean offerwallMode)`** <br/> Sets Pollfish SDK to Offerwall Mode | Boolean

### 6.1 `.setAPIKey(String apiKey)`

Pollfish API Key as provided by Pollfish on  [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign up to the platform.  If you have already specified Pollfish API Key on AdMob's UI, this param will be ignored.

### 6.2 `.setRequestUUID(String requestUUID)`

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

### 6.3 `.setReleaseMode(boolean releaseMode)`

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish AdMob Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

### 6.4 `.offerwallMode(boolean offerwallMode)`

Enables offerwall mode. If not set, one single survey is shown each time.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
val bundle = PollfishExtrasBundleBuilder()
    .setAPIKey(POLLFISH_API_KEY)
    .setReleaseMode(false)
    .setRequestUUID("MY_UUID")
    .setOfferwallMode(false)
    .build()

val request = AdRequest.Builder()
    .addNetworkExtrasBundle(PollfishAdMobAdapter::class.java, bundle)
    .build()
```

<span style="text-decoration:underline">Java</span>

```java
Bundle pollfishBundle = new PollfishExtrasBundleBuilder()
    .setAPIKey("YOUR_POLLFISH_API_KEY")
    .setReleaseMode(false)
    .setRequestUUID("MY_ID")
    .setOfferwallMode(false)
    .build();

AdRequest request = new AdRequest.Builder()
    .addNetworkExtrasBundle(PollfishAdMobAdapter.class, pollfishBundle)
    .build();
```

<br/>

## 7. Payouts on Screenouts

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described [here](https://www.pollfish.com/docs/pay-on-screenouts).

<br/>

## 8. Proguard

If you use proguard with your app, please insert the following lines in your proguard configuration file:  

```java
-dontwarn com.pollfish.**
-keep class com.pollfish.** { *; }
```

<br/>

# More info

You can read more info on how the Pollfish SDKs work or how to get started with Google AdMob at the following links:

[Pollfish Android SDK](https://pollfish.com/docs/android/google-play)

[AdMob Android SDK](https://developers.google.com/admob/android/quick-start)
