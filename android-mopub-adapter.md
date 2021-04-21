<div class="changelog" data-version="6.0.2.0">
v6.0.2.0

- Updating adapter with the new Pollfish Android SDK v6.0.2.0
    
v5.6.0.0

- New PollfishMoPubAdapter

</div>

This guide is for publishers looking to use MoPub mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

# Prerequisites

* Android API 21 or later
* [Pollfish Publisher Account](https://www.pollfish.com/dashboard/dev/)
* [MoPub Developer Account](https://app.mopub.com/login)
* [Pollfish SDK](https://www.pollfish.com/docs/android)
* [MoPub SDK](https://github.com/mopub/mopub-android-sdk#download)

> **Note:** Apps designed for [Children and Families program](https://play.google.com/about/families/ads-monetization/) should not be using Pollfish SDK, since Pollfish does not collect responses from users less than 16 years old    

> **Note:** Pollfish SDK requires minSdk 21. If your app supports a lower minSdk you can still use the adapter by adding the following blocks on your code.

**AndroidManifest.xml**

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    ... >

    <uses-sdk tools:overrideLibrary="com.pollfish.pollfish" />

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

</br>

Below you can find a step by step guide on how to incorporate Pollfish surveys with MoPub mediation:

# Step 1: Add MoPub Rewarded Ads in your app 

If you have not implemented [Rewarded Ads](https://developers.mopub.com/publishers/android/rewarded-ad/) in your app yet, you can follow the documentation implementation as described by MoPub. 

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

First you need to sign in to your [MoPub account](https://www.mopub.com/). In your app's section you can click to create a **New Ad Unit** and select **Rewarded Video**

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub_ad_unit.png"/>

<br/>

In the configuration of the Ad Unit you can specify a name for your rewarded placement. If you want you can specify the reward name and a fix amount by clicking **Add Reward**.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-add-reward.png"/>
<br/>

If you don't apply this setting, the Pollfish adapter will provide a dynamic value as you specified it on your Pollfish Dashboard, in the App Settings area, based on the actual price of each survey completed.

<br/>

# Step 2: Configure Ad Sources for your Rewarded Ad unit

You need to add Pollfish Network as a **Custom Native Network**
line item and link it with your Rewarded Ad unit. 

Log in to your MoPub account. On the top, click on the **Orders** tab and then select **Create Order**. If you already have an existing **Order** item you will need to modify it by clicking on it.

In the **Create Order** form, fill the required fields and press **Save & Create line item**

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-android-new-order.png"/>

<br/>

Next you will be prompted to create a **New Line Item**

Please make sure the correct order item is selected. Then set **Pollfish Network** as the line item name and **Network line item** as the Line item type.

On the **Network** field select **Custom SDK Network**. Set **com.mopub.mobileads.PollfishMoPubAdapter** in the **Custom event class** field and optionally provide a JSON formatted text with your Pollfish confiiguration (alternatively you can pass those params in code as described in Step 6) in the **Custom event data** field. 

> **Note:** In order for **PollfishMoPubAdapter** to work, you need to provide the configuration at least one time. If you skip please make sure you provide this configuration during the **RewardedAd** request in code (Step 6). Configuration parameters in code will override Web UI parameters if provided in both places.

Field | Value 
--- | ---
**Custom event class** | com.mopub.mobileads.PollfishMoPubAdapter<br/>
**Custom event data:** | JSON with Pollfish SDK configuration prams (optional)

<br/>

JSON configuration structure

No | Key | Type
------------ | -------------| -------------
2.1 | **`api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish | String
2.2 | **`release_mode`** <br/> Sets Pollfish SDK to Developer or Release mode | Bool
2.4 | **`oferrwall_mode`** <br/> Sets Pollfish SDK to Oferwall Mode | Bool
2.4 | **`request_uuid`** <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks | String

Example:

```json
{
    "api_key": "API_KEY", 
    "release_mode": true,
    "offerwall_mode": true,
    "request_uuid": "REQUEST_UUID" 
}
```

If you want to configure those params in code (section 6) fill the **Custom event data** field with an empty JSON object .

```json
{}
```

> **Note:** Pollfish SDK works by default in production mode. If you would like to test with test surveys you should use `release_mode` false or explicitly request that in code as described in Step 6.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-android-new-line-1.png"/>

<br/>

Next head to the **Budget & Schedule** section and fill the **Rate** field with a value ranging between $70-$80 since Pollfish rewarded surveys eCPMs usually fluctuates in that range.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-new-line-item-1-budget.png"/>

<br/>

Click next to proceed on the next step where you will select the Ad Unit on which this line item will apply. Please select Android only Ad Units.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-android-new-line-2.png"/>

<br/>

Click next to proceed on the next step where you will select the audience targeting of this Netwrok line item. Fill those fields as you wish or proceed with the default values.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-new-line-item-3.png"/>

<br/>

# Step 3: Set Up Pollfish

## 3.1. Obtain a Publisher Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

## 3.2. Add new app on Pollfish Publisher Dashboard and copy the given API Key

Login at [www.pollfish.com](www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Publisher Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

# Step 4: Add PollfishMoPubAdapter to your project

## 4.1. Add Pollfish aar library to your project

Download Pollfish Android SDK or reference it through maven().

**Download Pollfish Android SDK**

Import Pollfish **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

**Retrieve Pollfish Android SDK through maven()**

Retrieve Pollfish through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```
dependencies {
    implementation 'com.pollfish:pollfish-googleplay:6.0.2'
}
```

## 4.2. Integrate Google Play Services to your project

Applications that integrate Pollfish SDK are required to include Google Play Services library in order to give access to the Advertising ID of a device to the SDK. Further details regarding integration with the Google Play services library can be found [here](https://developers.google.com/android/guides/setup).

```java
dependencies {
    implementation 'com.google.android.gms:play-services-ads-identifier:17.0.0'
}
```

## 4.3: Add MoPub SDK to your porject

Retrieve MoPub SDK through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```
dependencies {
    implementation 'com.pollfish.mediation:pollfish-mopub:6.0.2.0'
}
```

**OR**

Visit MoPub SDK [GitHub page](https://github.com/mopub/mopub-android-sdk#download) for more info and alternative ways of downloading and integrating their SDK in your app.

## 4.4: Add Pollfish MoPub Adapter to your project

Import Pollfish MoPub Adapter **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish MoPub Adapter aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

**Retrieve Pollfish MoPub Adapter through maven()**

Retrieve Pollfish MoPub Adapter through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```
dependencies {
    implementation 'com.pollfish.mediation:pollfish-mopub:6.0.2.0'
}
```

<br/>

# Step 5: Request for a RewardedAd

Import `com.mopub.common` and `com.mopub.mobileads` packages

<span style="text-decoration:underline">Kotlin</span>

```kotlin
import com.mopub.common.*
import com.mopub.mobileads.*
```

<span style="text-decoration:underline">Java</span>

```java
import com.mopub.common.*;
import com.mopub.mobileads.*;
```

Implement `SdkInitializationListener` interface to listen for MoPub SDK intialisation completion

<span style="text-decoration:underline">Kotlin</span>

```kotlin
class MainActivity : AppCompatActivity(), SdkInitializationListener {
    
     override fun onInitializationFinished() {}

}
```

<span style="text-decoration:underline">Java</span>

```java
public class MainActivity extends AppCompatActivity implements SdkInitializationListener {
    
    @Override
    public void onInitializationFinished() {}

}
```

Initialize MoPub SDK and pass `PollfishAdapterConfiguration` class name on the initialisation configuration.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
val configuration = SdkConfiguration.Builder("AD_UNIT_ID")
    .withAdditionalNetwork(PollfishAdapterConfiguration::class.java.name)
    .withMediatedNetworkConfiguration(
        PollfishAdapterConfiguration::class.java.name, emptyMap()
    )
    .build()

MoPub.initializeSdk(this, configuration, this)
```

<span style="text-decoration:underline">Java</span>

```java
SdkConfiguration configuration = new SdkConfiguration.Builder("AD_UNIT_ID")
    .withAdditionalNetwork(PollfishAdapterConfiguration.class.getName())
    .withMediatedNetworkConfiguration(
        PollfishAdapterConfiguration.class.getName(), new HashMap<>())
    .build();

MoPub.initializeSdk(this, configuration, this);
```

Request a RewardedAd from MoPub using the Pollfish configuration params that you provided on MoPub's Web UI (step 2). If no configuration is provided or if you want to override any of those params provided in the Web UI please see step 6.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
MoPubRewardedAds.setRewardedAdListener(this)
MoPubRewardedAds.loadRewardedAd("AD_UNIT_ID")
```

<span style="text-decoration:underline">Java</span>

```java
MoPubRewardedAds.setRewardedAdListener(this);
MoPubRewardedAds.loadRewardedAd("AD_UNIT_ID");
```

Implement `MoPubRewardedAdListener` to get notified when the rewarded ad is ready to be shown

<span style="text-decoration:underline">Kotlin</span>

```kotlin
class MainActivity : AppCompatActivity(), 
    ...,
    MoPubRewardedAdListener {

    override fun onRewardedAdClicked(adUnitId: String) {}

    override fun onRewardedAdClosed(adUnitId: String) {}

    override fun onRewardedAdCompleted(adUnitIds: Set<String?>, reward: MoPubReward) {}

    override fun onRewardedAdLoadFailure(adUnitId: String, errorCode: MoPubErrorCode) {}

    override fun onRewardedAdLoadSuccess(adUnitId: String) {}

    override fun onRewardedAdShowError(adUnitId: String, errorCode: MoPubErrorCode) {}

    override fun onRewardedAdStarted(adUnitId: String) {}

}
```

<span style="text-decoration:underline">Java</span>

```java
public class MainActivity extends AppCompatActivity implements MoPubRewardedAdListener {

    @Override
    public void onRewardedAdClicked(String s) {}

    @Override
    public void onRewardedAdClosed(String s) {}

    @Override
    public void onRewardedAdCompleted(Set<String> set, MoPubReward reward) {}

    @Override
    public void onRewardedAdLoadFailure(String s, MoPubErrorCode moPubErrorCode) {}

    @Override
    public void onRewardedAdLoadSuccess(String s) {}

    @Override
    public void onRewardedAdShowError(String s, MoPubErrorCode moPubErrorCode) {}

    @Override
    public void onRewardedAdStarted(String s) {}

}
```

When the Rewarded Ad is ready present the ad by invoking `showRewardedAd`

<span style="text-decoration:underline">Kotlin</span>

```kotlin
MoPubRewardedAds.showRewardedAd("AD_UNIT_ID")
```

<span style="text-decoration:underline">Java</span>

```java
MoPubRewardedAds.showRewardedAd("AD_UNIT_ID");
```

<br/>

# Step 6: Create PollfishMoPubMediationSettings object (Optional)

Pollfish MoPub Adapter provides different options that you can use to control the behaviour of Pollfish SDK.

<br/>

Below you can see how to initialise **`PollfishMoPubMediationSettings`**  that is used to configure the behaviour of Pollfish SDK.

<br/>

```kotlin
PollfishMoPubAdapter.PollfishMoPubMediationSettings
    .create(apiKey: "API_KEY", 
        requestUUID: "REQUEST_UUID", 
        releaseMode: true,
        offerwallMode: true)
```

No | Description
------------ | -------------
6.1 | **`apikey`** <br/> Sets Pollfish SDK API key as provided by Pollfish
6.2 | **`requestUUID`** <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
6.3 | **`releaseMode`** <br/> Sets Pollfish SDK to Developer or Release mode
6.4 | **`offerwallMode`** <br/> Sets Pollfish SDK to Offerwall Mode

<br/>

### **6.1 `apiKey`**

Pollfish API Key as provided by Pollfish on  [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign up to the platform. If you have already specified Pollfish API Key on MoPub's UI, this param will override the one defined on Web UI.

### **6.2 `requestUUID`**

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

### **6.3 `releaseMode`**

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish MoPub Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

### **6.4 `offerwall_mode`**

Enables offerwall mode. If not set, one single survey is shown each time.

<br/>

Below you can see an example on how you can pass info to Pollfish MoPub Adapter connfiguration:

<span style="text-decoration:underline">Kotlin</span>

```kotlin
val configuration = SdkConfiguration.Builder(adUnitId)
    ...
    .withMediationSettings(
        PollfishMoPubAdapter.PollfishMoPubMediationSettings
            .create(
                apiKey = "YOUR_POLLFISH_API_KEY",
                requestUUID = "REQUEST_UUID",
                releaseMode = true,
                offerwallMode = false
            )
    )
    .build()

MoPub.initializeSdk(this, configuration, this)
```

<span style="text-decoration:underline">Java</span>

```java
SdkConfiguration configuration = new SdkConfiguration.Builder(adUnitId)
    ...
    .withMediationSettings(
        PollfishMoPubAdapter.PollfishMoPubMediationSettings
            .create("YOUR_POLLFISH_API_KEY", "REQUEST_UUID", true, false)
    )
    .build()

MoPub.initializeSdk(this, configuration, this);
```

# Step 7: Publish your app on the store

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option. You can read more [here](https://www.pollfish.com/docs/demographic-surveys)

