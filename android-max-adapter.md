<div class="changelog" data-version="7.0.0-beta07.0">
v7.0.0-beta07.0

- Updated with Prodege Android SDK v7.0.0-beta07

v7.0.0-beta06.0

- Updated with Prodege Android SDK v7.0.0-beta06

v7.0.0-beta05.0

- Updated with Prodege Android SDK v7.0.0-beta05

v7.0.0-beta04.0

- Updated with Prodege Android SDK v7.0.0-beta04

v7.0.0-beta03.0

- Updated with Prodege Android SDK v7.0.0-beta03

v7.0.0-beta02.0

- Updated with Prodege Android SDK v7.0.0-beta02

v7.0.0-beta01.0

- Updated with new Prodege Android SDK v7.0.0-beta01
- Introduced placements and rewarded video ads

v6.4.0.0

- Updated with Pollfish Android SDK v6.4.0

v6.3.3.1

- Adding the option to configure the Pollfish user id through the adapter

v6.3.3.0

- Updated with Pollfish Android SDK v6.3.3

v6.3.2.0

- Updated with Pollfish Android SDK v6.3.2

v6.3.1.0

- Updated with Pollfish Android SDK v6.3.1

v6.3.0.0

- Updated with Pollfish Android SDK v6.3.0

v6.2.5.0

- Updated with Pollfish Android SDK v6.2.5

v6.2.4.0

- Updated with Pollfish Android SDK v6.2.4

v6.2.3.0

- Updated with Pollfish Android SDK v6.2.3

v6.2.2.0

- Initial release

</div>

This guide is for publishers looking to use Max mediation to load and show Rewarded Ads from Prodege in the same waterfall with other Rewarded Ads.

<br/>

# Prerequisites

- [Prodege Publisher Account](www.pollfish.com/login/publisher)
- [AppLovin Developer Account](https://dash.applovin.com/login)
- Android API 21 or later
- Java version 1.8
- Kotlin 1.9.0

> **Note:** Apps designed for [Children and Families program](https://play.google.com/about/families/ads-monetization/) should not be using Prodege SDK, since Prodege does not collect responses from users less than 16 years old.

> **Note:** Prodege SDK requires minSdk 21. If your app supports a lower minSdk you can still build your app please refer to section 7.

</br>

# Quick Guide

- Set up Prodege Rewarded Ads
- Set up AppLovin Rewarded Ads
- Add Prodege Max Adapter to your project
- Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Prodege rewarded ads with AppLovin's Max mediation:

## 1. Set up Prodege Rewarded Ads

### 1.1. Obtain a Publisher Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher).

<br/>

### 1.2. Add a new app on the Publisher Dashboard and copy the given API Key

Login at [www.pollfish.com](www.pollfish.com/login/publisher) and click "Add a new app" on the [Publisher Dashboard](https://www.pollfish.com/publisher/). Copy the given API key for this app in order to use later on.

<br/>

### 1.3. Create a Rewarded Ad Placement and copy the given Placement Id

Create a Rewarded placement by clicking "Create a Placement". Provide a name an select the ad unit and ad format. Copy the given placement id in order to use later on.

<br/>

## 2. Set up AppLovin Rewarded Ads

### 2.1. Create a new Network

First you need to sign in to your [AppLovin account](https://dash.applovin.com/login). Add Prodege Network as a **Custom Network**. On the side menu navigate to Mediation -> Manage -> Networks.

Scroll down to the bottom of the list and click on **Click here to add a Custom Network**.

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_create_prodege_network.png"/>

<br/>

Next you will be prompted to create a **New Custom Network**.

On the **Network Type** field select **SDK**. Set **`Prodege`** as the value of **Custom Network Name** field. Set **`com.applovin.mediation.adapters.ProdegeMediationAdapter`** as the **Android/Fire OS Adapter Class Name**. Optionally, you can fill the **iOS Adapter Class Name** with the value **`ProdegeMaxAdapter`**.

<br/>

### 2.2. Create a Rewarded Ad Unit

If you have not created a Rewarded Ad Unit in your app yet, navigate to Mediation -> Manage -> Ad Units and click **New Ad Unit**.

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step.

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_ad_unit_1.png"/>

<br/>

Give your Ad Unit a name and select the Android option as the Platform. Start typing the name of your app, in the application name text field. If your app has already been publisher on the Google Play you should be able to select it from the result list. If you haven't publisher your app yet, click on the **Manualy add your package name**. Fill your application package name as found in your AndroidManifest.xml file and click **Create**.

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_ad_unit_2.png"/>

<br/>

Scroll down till you find the **Custom Networks & Deals** section and enable **Prodege** newtork. 

Paste your application's API Key as provided by the [Publisher Dashboard](https://www.pollfish.com/publisher/) (section 1.2) into the App ID input field. Although the App ID is marked as optional, it is actullay required in order for the integration to work.

Paste your ad unit's placement id as provided by the [Publisher Dashboard](https://www.pollfish.com/publisher/) (section 1.3) into the Placement ID input field.

Optionally provide a JSON formatted string for your Prodege adapter configuration (alternatively you can pass those params in code as described in section 6) using the `setLocalExtraParameter` method of your `RewardedAd` object instance. 

JSON configuration structure

| Key                                                                                                                                                             | Type    | Required |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|----------|
| **2.2.1. `request_uuid`** <br/> Sets a pass-through param to be received via the server-to-server callbacks [s2s callbacks](https://www.pollfish.com/docs/s2s). | String  | No       |
| **2.2.2. `muted`** <br/> Toggles Prodege video ads mute state.                                                                                                  | Boolean | No       |

Example:

```json
{
    "request_uuid": "REQUEST_UUID",
    "muted": false
}
```

> **Note:** Prodege SDK respects the AppLovin's SDK test mode state. If you would like to test, while the AppLovin is not in test mode, with test ads you should specify it in code as described in section 6.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_configure_prodege_network.png"/>

<br/>

Next, fill the CPM Price field with a value ranging between $10-$50 since Prodege rewarded ads eCPMs usually fluctuates in that range.

Finally, click create.

<br/>

## 3. Add Prodege Max Adapter to your project

### **3.1. Retrieve Prodege Max Adapter through maven()**

Retrieve Prodege Max Adapter through **maven()** with gradle by adding the following line in your app's module **build.gradle** file:  

```groovy
dependencies {
    implementation 'com.prodege.mediation:prodege-max:7.0.0-beta06.0'
}
```

<br>

### **3.2. Manual installation**

> **Note:** If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .aar Package option and from the file browser locate the `.aar` file. Right click again on your project and in the Module Dependencies tab choose to add the module that you recently added, as a dependency.

<br/>

### 3.2.1. Download Prodege Android Max Adapter `.aar` file and import it into your project's libraries

Click [here](https://storage.googleapis.com/pollfish_production/sdk/AppLovin/Prodege%20Android%20Max%20Adapter-7.0.0-beta06.0.zip) to download the latest version of Prodege Android Max Adapter SDK.

<br/>

### 3.2.2. Download Prodege Android SDK `.aar` file and import it into your project's libraries

Click [here](https://storage.googleapis.com/pollfish_production/sdk/Android/Prodege%20Android%20SDK-7.0.0-beta06.zip) to download the latest version of Prodege Android SDK. 

<br/>

### 3.2.3. Integrate Google Play Services to your project (Optional)

Applications that integrate Prodege SDK may use Google Play Services library in order to give access to the Advertising ID of a device to the SDK. Further details regarding integration with the Google Play services library can be found [here](https://developers.google.com/android/guides/setup). By skipping this step you have to provide a userId during initialization. Refer to section 6 for more details.

```groovy
dependencies {
    implementation 'com.google.android.gms:play-services-ads-identifier:18.0.1'
}
```

<br/>

**Android 12**

Apps updating their target API level to 31 (Android 12) or higher will need to declare a Google Play services normal permission in the `AndroidManifest.xml` file.

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

You can read more about Google Advertising ID changes [here](https://support.google.com/googleplay/android-developer/answer/6048248).

<br/>

## 4. Request for a RewardedAd

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

Import the following packages

<span style="text-decoration:underline">Kotlin</span>

```kotlin
import com.applovin.mediation.*
import com.applovin.mediation.ads.MaxRewardedAd
import com.applovin.sdk.AppLovinMediationProvider
import com.applovin.sdk.AppLovinSdk
```

<span style="text-decoration:underline">Java</span>

```java
import com.applovin.mediation.*;
import com.applovin.mediation.ads.MaxRewardedAd;
import com.applovin.sdk.AppLovinMediationProvider;
import com.applovin.sdk.AppLovinSdk;
```

<br/>

Initialize AppLovin SDK by calling the `initializeSdk()` method, passing that method an `Activity` context. Do this as soon as possible after your app starts, for example in the `onCreate()` method of your launch Activity.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    // ...

    AppLovinSdk.getInstance(this).mediationProvider = AppLovinMediationProvider.MAX

    AppLovinSdk.getInstance(this).initializeSdk {
        createRewardedAd()
    }
}
```

<span style="text-decoration:underline">Java</span>

```java
protected void onCreate(Bundle savedInstanceState) {
    // ...

    AppLovinSdk.getInstance(this).setMediationProvider(AppLovinMediationProvider.MAX);

    AppLovinSdk.getInstance(this).initializeSdk(config -> {
        createRewardedAd();
    });
}
```

<br/>

Implement `MaxRewardedAdListener` so that you are notified when your ad is ready and of other ad-related events.

Request a RewardedAd from AppLovin by calling `loadAd()` in the `RewardedAd` object instance you've created. By default Prodege Max Adapter will use the configuration as provided on AppLovin's dashboard (section 2). If no configuration is provided or if you want to override any of those params please see section 6.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
class MainActivity : AppCompatActivity(), MaxRewardedAdListener {

    private lateinit var rewardedAd: RewardedAd

    // ...

    private fun createRewardedAd() {
        rewardedAd = MaxRewardedAd.getInstance("AD_UNIT_ID", this);
        rewardedAd.setListener(this);
        loadRewardedAd();
    }

    private fun loadRewardedAd() {
        rewardedAd.loadAd()
    }

    override fun onAdLoaded(ad: MaxAd?) {}

    override fun onAdDisplayed(ad: MaxAd?) {}

    override fun onAdHidden(ad: MaxAd?) {}

    override fun onAdClicked(ad: MaxAd?) {}

    override fun onAdLoadFailed(adUnitId: String?, error: MaxError?) {}

    override fun onAdDisplayFailed(ad: MaxAd?, error: MaxError?) {}

    override fun onRewardedVideoStarted(ad: MaxAd?) {}

    override fun onRewardedVideoCompleted(ad: MaxAd?) {}

    override fun onUserRewarded(ad: MaxAd?, reward: MaxReward?) {}

}
```

<span style="text-decoration:underline">Java</span>

```java
class MainActivity extends AppCompatActivity implements MaxRewardedAdListener {

    private RewardedAd rewardedAd;

    // ...

    private void createRewardedAd() {
        rewardedAd = MaxRewardedAd.getInstance("AD_UNIT_ID", this);
        rewardedAd.setListener(this);
        loadRewardedAd();
    }

    private void loadRewardedAd() {
        rewardedAd.loadAd();
    }

    @Override
    public void onRewardedVideoStarted(MaxAd ad) {}

    @Override
    public void onRewardedVideoCompleted(MaxAd ad) {}

    @Override
    public void onUserRewarded(MaxAd ad, MaxReward reward) {}

    @Override
    public void onAdDisplayed(MaxAd ad) {}

    @Override
    public void onAdHidden(MaxAd ad) {}

    @Override
    public void onAdClicked(MaxAd ad) {}

    @Override
    public void onAdLoadFailed(String adUnitId, MaxError error) {}

    @Override
    public void onAdDisplayFailed(MaxAd ad, MaxError error) {}
}
```

When the Rewarded Ad is ready, present the ad by invoking `rewardedAd.showAd()`. Just to be sure, you can combine show with a check to see if the Ad you are about to show is actualy ready.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
if (rewardedAd.isReady) {
    rewardedAd.showAd()
}
```

<span style="text-decoration:underline">Java</span>

```java
if (rewardedAd.isReady()) {
    rewardedAd.showAd();
}
```

<br/>

## 5. Publish your app on the store

If everything worked fine during the previous steps, you are ready to proceed with publishing your app.

> **Note:** After you take your app live, you should request your account to get verified through Prodege Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Prodege to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option. You can read more [here](https://www.pollfish.com/docs/demographic-surveys).

<br/>

# Optional section

## 6. Configure the Prodege SDK programmatically

Prodege Max Adapter provides different options that you can use to control the behaviour of Prodege SDK. This configuration, if applied, will override any configuration done in AppLovin's dashboard.

<br/>

### **6.1. Initialization configuration**

Below you can see all the availbale options for configuring Prodege SDK prior to the AppLovin SDK initialization.

<br/>

### 6.1.1. `userIdentifier`

An optional id used to identify a user.

Setting the AppLovin's `userIdentifier` will override the default behaviour and use that instead of the Advertising Id in order to identify a user.

> **Note:** <span style="color: red">You can pass the id of a user as identified on your system. Prodege will use this id to identify the user across sessions instead of an ad id/idfa as advised by the stores. You are solely responsible for aligning with store regulations by providing this id and getting relevant consent by the user when necessary. Prodege takes no responsibility for the usage of this id. In any request from your users on resetting/deleting this id and/or profile created, you should be solely liable for those requests.</span>

<span style="text-decoration:underline">Kotlin</span>

```kotlin
AppLovinSdk.getInstance(this).userIdentifier = "USER_ID"
```

<span style="text-decoration:underline">Java</span>

```java
AppLovinSdk.getInstance(this).setUserIdentifier("USER_ID");
```

<br/>

### 6.1.2. `testMode`

Toggles the Prodege SDK Test mode.

- **`true`** is used to show to the developer how Prodege ads will be shown through an app (useful during development and testing).
- **`false`** is the mode to be used for a released app in any app store (start receiving paid surveys).

If you have already specified the preferred mute state on AppLovin's UI, this will override the one defined on Web UI.

Prodege Max Adapter respects the AppLovin's SDK test mode state by default. If you would like to test Prodege ads, while AppLovin SDK is in live mode.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
AppLovinSdk.getInstance(this).settings.setExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_TEST_MODE,
    "true"
)
```

<span style="text-decoration:underline">Java</span>

```java
AppLovinSdk.getInstance(this).getSettings().setExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_TEST_MODE, 
    "true"
);
```

<br/>

### 6.1.3. `muted`

You can set globally the video mute state for both AppLovin and Prodege.

If you have already specified the preferred mute state on AppLovin's UI, this will override the one defined on Web UI.

Prodege Max Adapter respects the AppLovin's SDK mute state by default.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
AppLovinSdk.getInstance(this).settings.isMuted = true
```

<span style="text-decoration:underline">Java</span>

```java
AppLovinSdk.getInstance(this).getSettings().setMuted(true);
```

<br/>

After configuring the Prodege Max Adapter you can proceed with the AppLovin SDK initialization.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
AppLovinSdk.getInstance(this).initializeSdk {
    // ...
}
```

<span style="text-decoration:underline">Java</span>

```java
AppLovinSdk.getInstance(this).initializeSdk(config -> {
    // ...
});
```

<br/>

### **6.2. Rewarded Ad configuration**

Below you can see all the supported options for configuring your `MaxRewardedAd` intance.

Start by gettings a `MaxRewardedAd` by calling:.

<span style="text-decoration:underline">Kotlin</span>

``` kotlin
val rewardedAd = MaxRewardedAd.getInstance(...);
```

<span style="text-decoration:underline">Java</span>

```java
MaxRewardedAd rewardedAd = MaxRewardedAd.getInstance(...);
```

<br/>

### 6.2.1. `placementId`

Your ad unit's placement id as provided by [Publisher Dashboard](https://www.pollfish.com/publisher/). 

If you have already specified a placement id on AppLovin's UI, this param will override the one defined on Web UI.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
rewardedAd.setLocalExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_PLACEMENT_ID,
    "PLACEMENT_ID"
)
```

<span style="text-decoration:underline">Java</span>

```java
rewardedAd.setLocalExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_PLACEMENT_ID, 
    "PLACEMENT_ID"
);
```

<br/>

### 6.2.2. `requestUuid`

Sets a pass-through param to be received via the server-to-server callbacks.

In order to register for such callbacks you can set up your server URL on your app's page on the [Publisher Dashboard](https://www.pollfish.com/publisher/). On each survey completion you will receive a callback to your server including the `request_uuid` param passed.

If you would like to read more on Prodege s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s).

If you have already specified a placement id on AppLovin's UI, this will override the one defined on Web UI.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
rewardedAd.setLocalExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_REQUEST_UUID,
    "REQUEST_UUID"
)
```

<span style="text-decoration:underline">Java</span>

```java
rewardedAd.setLocalExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_REQUEST_UUID,
    "REQUEST_UUID"
)
```

<br/>

### 6.2.3 `muted`

Sets Prodege video ads mute state. 

If you have already specified the preferred mute state on AppLovin's UI or by setting the global AppLovin SDK mute state, this will override any of the previous configurations.

Prodege Max Adapter respects the AppLovin's SDK mute state by default. If you would like to toggle the mute state only for Prodege ads:

<span style="text-decoration:underline">Kotlin</span>

```kotlin
rewardedAd.setLocalExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_MUTED, 
    false
)
```

<span style="text-decoration:underline">Java</span>

```java
rewardedAd.setLocalExtraParameter(
    ProdegeMediationAdapter.LOCAL_EXTRA_REQUEST_UUID,
    "REQUEST_UUID"
)
```

<br/>

Finally, after configuring your rewarded ad.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
rewardedAd.loadAd()
```

<span style="text-decoration:underline">Java</span>

```java
rewardedAd.loadAd();
```

<br/>

## 7. Minimum SDK version

Prodege SDK requires at minimum Android API 21 in order to work. You can still build your app if your app minimum target is lower than 21.

**AndroidManifest.xml**

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-sdk tools:overrideLibrary="com.prodege" />

    <!-- ... -->
```

**app/build.gradle**

```groovy
defaultConfig {
    // ...

    multiDexEnabled true
}

dependencies {
    // ...

    implementation 'androidx.multidex:multidex:2.0.1'
}
```

<br/>

## 8. Payouts on Screenouts

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described [here](https://www.pollfish.com/docs/pay-on-screenouts).

<br/>

## 9. Proguard

If you use proguard with your app, please insert the following lines in your proguard configuration file:  

```java
-dontwarn com.prodege.**
-keep class com.prodege.** { *; }
```

<br/>

# More info

You can read more info on how the Prodege SDKs work or how to get started with AppLovin's Max at the following links:

[Prodege Android SDK](https://pollfish.com/docs/android-v7)

[AppLovin Max Android SDK](https://dash.applovin.com/documentation/mediation/android/getting-started/integration)
