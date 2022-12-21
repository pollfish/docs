<div class="changelog" data-version="6.3.3.0">
V6.3.3.0

- Updated with Pollfish Android SDK v6.3.3

V6.3.2.0

- Updated with Pollfish Android SDK v6.3.2

V6.3.1.0

- Updated with Pollfish Android SDK v6.3.1

v6.3.0.0

- Updated with Pollfish Android SDK v6.3.0

v6.2.5.0

- Updated with Pollfish Android SDK v6.2.5

v6.2.4.1

- Internal fixes

v6.2.4.0

- Initial release

</div>

This guide is for publishers looking to use ironSource LevelPlay to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

<br/>

# Prerequisites

- [Pollfish Developer Account](https://www.pollfish.com/dashboard/dev/)
- [IronSource Developer Account](https://platform.ironsrc.com/partners)
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

- Set up IronSource Rewarded Ads
- Set up Pollfish
- Add Pollfish IronSource Adapter to your project
- Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Pollfish surveys with IronSource mediation:

## 1. Set up IronSource Rewarded Ads

### 1.1. Add Pollfish Network

First you need to sign in to your [IronSource account](https://platform.ironsrc.com/partners). Add Pollfish Network as a **Custom Network**. On the side menu navigate to Monetize -> Setup -> SDK Netwokrs

Select you application from the Applications list and on the top of the page you will find a **Manage Networks** button. Click it and then click on the **Custom Adapter** option. 

Type **`15baf95f5`** as the Custom Adapter Network key on the input prompt and click **Enter Key**. 

<br/>

<img style="margin: 0 auto; display: block; max-height: 200px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_add_custom_network_1.png"/>

<br/>

You will be prompted to enter your Pollfish Reporting Key.
You can retrieve your account key by loging in to Pollfish Publisher account and navigating to your **Account information**.

<br/>

<img style="margin: 0 auto; display: block; max-height: 200px;" src="https://storage.googleapis.com/pollfish_production/doc_images/retrieve_reporting_key.png"/>

<br/>

<img style="margin: 0 auto; display: block; max-height: 400px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_add_custom_network_2.png"/>

<br/>

Select **Reporting API** for revenue reporting and click **Save**. You will find your newly added Network under the name **Pollfish** on each app's mediation network list.

<br/>

<img style="margin: 0 auto; display: block; max-height: 300px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_android_network_list.png"/>

<br/>

Configure Pollfish Network by clicking on the **Setup** button on the **Pollfish** network row from your App's Network list.

Fill the following input fields.

Key | Type
-------------| -------------
**1.1.1. `api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish | String
**1.1.2. `request_uuid`** <br/> Sets a pass-through param to be received via the server-to-server callbacks | String
**1.1.3. `release_mode`** <br/> Sets Pollfish SDK to Developer or Release mode | Boolean
**1.1.4. `oferrwall_mode`** <br/> Sets Pollfish SDK to Oferwall Mode | Boolean

<br/>

### 1.1.1 `api_key`

Pollfish API Key as provided by Pollfish on [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign up to the platform.

### 1.1.2 `request_uuid` or `null`

Sets a pass-through param to be received via the server-to-server callbacks

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

### 1.1.3. `release_mode`

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

### 1.1.4 `oferrwall_mode`

Enables offerwall mode. If not set, one single survey is shown each time.

<br/>

<img style="margin: 0 auto; display: block; max-height: 300px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_android_network_list.png"/>

<br/>

After adding the above required info click **Save**

<br/>

### 1.2. Add IronSource SDK to your porject

Retrieve IronSource SDK through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in dependencies section:

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

## 3. Add Pollfish IronSource Adapter to your project

Import Pollfish IronSource Adapter **.aar** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .aar Package option and from the file browser locate Pollfish MoPub Adapter aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

**Retrieve Pollfish IronSource Adapter through maven()**

Retrieve Pollfish IronSource Adapter through **maven()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```groovy
dependencies {
    implementation 'com.pollfish.mediation:pollfish-ironsource:6.3.0.0'
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

## 4. Request for a RewardedAd

<br/>

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

<br/>

IImport the following packages

<span style="text-decoration:underline">Kotlin</span>

```kotlin
import com.ironsource.mediationsdk.IronSource
import com.ironsource.mediationsdk.integration.IntegrationHelper
import com.ironsource.mediationsdk.logger.IronSourceError
import com.ironsource.mediationsdk.model.Placement
import com.ironsource.mediationsdk.sdk.RewardedVideoListener
```

<span style="text-decoration:underline">Java</span>

```java
import com.ironsource.mediationsdk.IronSource;
import com.ironsource.mediationsdk.integration.IntegrationHelper;
import com.ironsource.mediationsdk.logger.IronSourceError;
import com.ironsource.mediationsdk.model.Placement;
import com.ironsource.mediationsdk.sdk.RewardedVideoListener;
```

<br/>Initialize IronSource SDK by calling the `init` method, passing the `Activity` and your App Key as provided by the IronSource dashboard. Do this as soon as possible after your app starts, for example in the `onCreate()` method of your launch Activity.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    ...

    IntegrationHelper.validateIntegration(this)
    IronSource.setRewardedVideoListener(this)
    IronSource.init(this, "APP_KEY")
}
```

<span style="text-decoration:underline">Java</span>

```java
protected void onCreate(Bundle savedInstanceState) {
    ...

    IntegrationHelper.validateIntegration(this);
    IronSource.setRewardedVideoListener(this);
    IronSource.init(this, "APP_KEY");
}
```

<br/>

Implement `RewardedVideoListener` so that you are notified when your ad is ready and of other ad-related events.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
class MainActivity : AppCompatActivity(), RewardedVideoListener
```

<span style="text-decoration:underline">Java</span>

```java
class MainActivity extends AppCompatActivity implements RewardedVideoListener
```

<br/>

When the Rewarded Ad is ready, present the ad by invoking `IronSource.showRewardedVideo`. Just to be sure, you can combine show with a check to see if the Ad you are about to show is actualy ready.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
if (IronSource.isRewardedVideoAvailable())
    IronSource.showRewardedVideo()
```

<span style="text-decoration:underline">Java</span>

```java
if (IronSource.isRewardedVideoAvailable())
    IronSource.showRewardedVideo();
```

<br/>

You can view a short example on how to intergate rewarded ads below

<span style="text-decoration:underline">Kotlin</span>

```kotlin
class MainActivity : AppCompatActivity(), RewardedVideoListener {

    override fun onCreate(savedInstanceState: Bundle?) {
        ...

        IntegrationHelper.validateIntegration(this)
        IronSource.setRewardedVideoListener(this)
        IronSource.init(this, "APP_KEY")
    }

    override fun onResume() {
        ...

        IronSource.onResume(this)
    }

    override fun onPause() {
        ...

        IronSource.onPause(this)
    }

    fun onShowRewardedAdClick(view: View) {
        if (IronSource.isRewardedVideoAvailable())
            IronSource.showRewardedVideo()
    }

    override fun onRewardedVideoAdOpened() {}

    override fun onRewardedVideoAdClosed() {}

    override fun onRewardedVideoAvailabilityChanged(available: Boolean) {}

    override fun onRewardedVideoAdStarted() {}

    override fun onRewardedVideoAdEnded() {}

    override fun onRewardedVideoAdRewarded(placement: Placement) {}

    override fun onRewardedVideoAdShowFailed(ironSourceError: IronSourceError?) {}

    override fun onRewardedVideoAdClicked(placement: Placement) {}

}
```

<span style="text-decoration:underline">Java</span>

```java
class MainActivity extends AppCompatActivity implements RewardedVideoListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        ...

        IntegrationHelper.validateIntegration(this);
        IronSource.setRewardedVideoListener(this);
        IronSource.init(this, "APP_KEY");
    }

    @Override
    protected void onResume() {
        ...
        
        IronSource.onResume(this);
    }

    @Override
    protected void onPause() {
        ...

        IronSource.onPause(this);
    }

    void onShowRewardedAdClick(View view) {
        if (IronSource.isRewardedVideoAvailable())
            IronSource.showRewardedVideo();
    }
    
    @Override
    public void onRewardedVideoAdOpened() {}

    @Override
    public void onRewardedVideoAdClosed() {}

    @Override
    public void onRewardedVideoAvailabilityChanged(boolean available) {}

    @Override
    public void onRewardedVideoAdStarted() {}

    @Override
    public void onRewardedVideoAdEnded() {}

    @Override
    public void onRewardedVideoAdRewarded(Placement placement) {}

    @Override
    public void onRewardedVideoAdShowFailed(IronSourceError ironSourceError) {}

    @Override
    public void onRewardedVideoAdClicked(Placement placement) {}

}
```

<br/>

## 5. Publish your app on the store

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option. You can read more [here](https://www.pollfish.com/docs/demographic-surveys)

<br/>

# Optional section

## 6. Payouts on Screenouts

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described [here](https://www.pollfish.com/docs/pay-on-screenouts).

<br/>

## 7. Proguard

If you use proguard with your app, please insert the following lines in your proguard configuration file:  

```java
-dontwarn com.pollfish.**
-keep class com.pollfish.** { *; }
```

<br/>

# More info

You can read more info on how the Pollfish SDKs work or how to get started with IronSource at the following links:

[Pollfish Android SDK](https://pollfish.com/docs/android/google-play)

[IronSource Android SDK](https://developers.is.com/ironsource-mobile/android/android-sdk)
