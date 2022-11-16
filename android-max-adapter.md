<div class="changelog" data-version="6.3.0.0">
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

This guide is for publishers looking to use Max mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

<br/>

# Prerequisites

- [Pollfish Developer Account](https://www.pollfish.com/dashboard/dev/)
- [AppLovin Developer Account](https://dash.applovin.com/login)
- Android API 21 or later
- Java version 1.8

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

- Set up AppLovin Rewarded Ads
- Set up Pollfish
- Add Pollfish Max Adapter to your project
- Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Pollfish surveys with AppLovin's Max mediation:

## 1. Set up AppLovin Rewarded Ads

### 1.1. Create a new Network

First you need to sign in to your [AppLovin account](https://dash.applovin.com/login). Add Pollfish Network as a **Custom Network**. On the side menu navigate to Mediation -> Manage -> Networks

Scroll down to the bottom of the list and click on **Click here to add a Custom Network**

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_create_new_network.png"/>

<br/>

Next you will be prompted to create a **New Custom Network**

On the **Network Type** field select **SDK**. Set **Pollfish** as the value of **Custom Network Name** field. Set **com.applovin.mediation.adapters.PollfishMediationAdapter** as the **Android/Fire OS Adapter Class Name**. Optionally, you can fill the **iOS Adapter Class Name** with the value **PollfishMaxAdapter**.

<br/>

### 1.2. Create a Rewarded Ad Unit

If you have not created a Rewarded Ad Unit in your app yet, navigate to Mediation -> Manage -> Ad Units and click **New Ad Unit**.

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_ad_unit_1.png"/>

<br/>

Give your Ad Unit a name and select the Android option as the Platform. Start typing the name of your app, in the application name text field. If your app has already been publisher on the Google Play you should be able to select it from the result list. If you haven't publisher your app yet, click on the **Manualy add your package name**. Fill your application package name as found in your AndroidManifest.xml file and click **Create**.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_ad_unit_2.png"/>

<br/>

Scroll down till you find the **Custom Networks & Deals** section and enable **Pollfish** newtork. Optionally provide a JSON formatted string with your Pollfish confiiguration (alternatively you can pass those params in code as described in Step 6) using the `setLocalExtraParameter` method of your `RewardedAd` object instance. 

<br/>

> **Note:** In order for **PollfishMaxAdapter** to work, you need to provide the configuration at least one time. If you skip please make sure you provide this configuration during the **RewardedAd** request in code (Step 6). Configuration parameters in code will override Web UI parameters if provided in both places.

JSON configuration structure

Key | Type
-------------| -------------
**`api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish | String
**`release_mode`** <br/> Sets Pollfish SDK to Developer or Release mode | Bool
**`oferrwall_mode`** <br/> Sets Pollfish SDK to Oferwall Mode | Bool
**`request_uuid`** <br/> Sets a pass-through param to be received via the server-to-server callbacks | String

Example:

```json
{
    "api_key": "API_KEY", 
    "release_mode": true,
    "offerwall_mode": true,
    "request_uuid": "REQUEST_UUID" 
}
```

<br/>

If you want to configure those params in code (section 6) leave the **Custom Parameters** field empty.

> **Note:** Pollfish SDK works by default in production mode. If you would like to test with test surveys you should use `release_mode` false or explicitly request that in code as described in Step 6.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_ad_unit_3.png"/>

<br/>

Next, fill the CPM Price field with a value ranging between $70-$80 since Pollfish rewarded surveys eCPMs usually fluctuates in that range.

Finally, click create.

<br/>

### 1.3. Add AppLovin SDK to your porject

Retrieve AppLovin SDK through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in dependencies section:

```groovy
dependencies {
    implementation 'com.applovin:applovin-sdk:11.1.2'
}
```

<br/>

## 2 Set Up Pollfish

### 2.1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

<br/>

### 2.2. Add new app on Pollfish Publisher Dashboard and copy the given API Key

Login at [www.pollfish.com](www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Publisher Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

<br/>

## 2.3. Add Pollfish SDK to your project

Download Pollfish Android SDK or reference it through maven().

**Download Pollfish Android SDK**

Click [here](https://storage.googleapis.com/pollfish_production/sdk/Android/Pollfish%20Google%20Play%20Android%20SDK-6.2.5.zip) to download the latest version of Pollfish Android SDK 

**Import Pollfish `.aar` file to your project libraries**

If you are using Android Studio, right click on your project and select New Module. Then select Import .jar or .aar Package option and from the file browser locate Pollfish aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**Integrate Google Play Services to your project**

Applications that integrate Pollfish SDK are required to include Google Play Services library in order to give access to the Advertising ID of a device to the SDK. Further details regarding integration with the Google Play services library can be found [here](https://developers.google.com/android/guides/setup).

```groovy
dependencies {
    implementation 'com.google.android.gms:play-services-ads-identifier:17.0.0'
}
```

**OR**

**Retrieve Pollfish Android SDK through maven()**

Retrieve Pollfish through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in dependencies section:

```groovy
dependencies {
    implementation 'com.pollfish:pollfish-googleplay:6.3.0'
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

## 3. Add Pollfish Max Adapter to your project

Import Pollfish Max Adapter **.aar** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .aar Package option and from the file browser locate Pollfish Max Adapter aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

**Retrieve Pollfish Max Adapter through maven()**

Retrieve Pollfish Max Adapter through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```groovy
dependencies {
    implementation 'com.pollfish.mediation:pollfish-max:6.3.0.0'
}
```

<br/>

## 4. Request for a RewardedAd

<br/>

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

<br/>

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
    ...

    AppLovinSdk.getInstance(this).mediationProvider = AppLovinMediationProvider.MAX

    AppLovinSdk.getInstance(this).initializeSdk {
        createRewardedAd()
    }
}
```

<span style="text-decoration:underline">Java</span>

```java
protected void onCreate(Bundle savedInstanceState) {
    ...

    AppLovinSdk.getInstance(this).setMediationProvider(AppLovinMediationProvider.MAX);

    AppLovinSdk.getInstance(this).initializeSdk(config -> {
        createRewardedAd();
    });
}
```

<br/>

Implement `MaxRewardedAdListener` so that you are notified when your ad is ready and of other ad-related events.

<br/>

Request a RewardedAd from AppLovin by calling `loadAd()` in the `RewardedAd` object instance you've created. By default Pollfish Max Adapter will use the configuration as provided on AppLovin's dashboard (step 2). If no configuration is provided or if you want to override any of those params please see step 6.

<br/>

<span style="text-decoration:underline">Kotlin</span>

```kotlin
class MainActivity : AppCompatActivity(), MaxRewardedAdListener {

    private lateinit var rewardedAd: RewardedAd

    ...

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

    ...

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

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option. You can read more [here](https://www.pollfish.com/docs/demographic-surveys)

<br/>

# Optional section

## 6. Configure programmatically Pollfish SDK behaviour

Pollfish Max Adapter provides different options that you can use to control the behaviour of Pollfish SDK. This configuration, if applied, will override any configuration done in AppLovin's dashboard.

<br/>

| No  | Description                                                                                                                                      |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 6.1 | **`api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish                                                                            |
| 6.2 | **`request_uuid`** <br/> Sets a pass-through param to be received via the server-to-server callbacks [s2s callbacks](https://www.pollfish.com/docs/s2s) |
| 6.3 | **`release_mode`** <br/> Toggles Pollfish SDK Developer or Release mode                                                                          |
| 6.4 | **`offerwallMode`** <br/> Sets Pollfish SDK to Offerwall Mode                                                                                    |

<br/>

### 6.1 `api_key`

Pollfish API Key as provided by Pollfish on [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign in and create an app. If you have already specified Pollfish API Key on AppLovin's UI, this param will override the one defined on Web UI.

<br/>

### 6.2 `request_uuid`

Sets a pass-through param to be received via the server-to-server callbacks

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard. On each survey completion you will receive a callback to your server including the `request_uuid` param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

<br/>

### 6.3 `release_mode`

Sets Pollfish SDK to Developer or Release mode.

- **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
- **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish Max Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

<br/>

### 6.4 `offerwall_mode`

Enables offerwall mode. If not set, one single survey is shown each time.

<br/>

```kotlin
rewardedAd = MaxRewardedAd.getInstance("25aa38dc0445505f", this)
rewardedAd.setLocalExtraParameter("release_mode", false)
rewardedAd.setLocalExtraParameter("offerwall_mode", true)
rewardedAd.setLocalExtraParameter("api_key", "YOUR_POLLFISH_API_KEY")
rewardedAd.setLocalExtraParameter("request_uuid", "REQUEST_UUID")
```

<br/>


## 7. Payouts on Screenouts

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described [here](https://www.pollfish.com/docs/pay-on-screenouts).

<br/>

# More info

You can read more info on how the Pollfish SDKs work or how to get started with AppLovin's Max at the following links:

[Pollfish Android SDK](https://pollfish.com/docs/android/google-play)

[AppLovin Max Android SDK](https://dash.applovin.com/documentation/mediation/android/getting-started/integration)
