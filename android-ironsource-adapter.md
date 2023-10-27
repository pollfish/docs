<div class="changelog" data-version="7.0.0-beta01.0">
v7.0.0-beta01.0

- Updated with new Prodege Android SDK v7.0.0-beta01
- Introduced placements and rewarded video ads

v6.4.0.0

- Updated with Pollfish Android SDK v6.4.0

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

v6.2.4.1

- Internal fixes

v6.2.4.0

- Initial release

</div>

This guide is for publishers looking to use IronSource LevelPlay to load and show Rewarded Ads from Prodege in the same waterfall with other Rewarded Ads.

<br/>

# Prerequisites

- [Prodege Publisher Account](www.pollfish.com/login/publisher)
- [IronSource Developer Account](https://platform.ironsrc.com/partners)
- Android API 21 or later
- Java 1.8
- Kotlin 1.9.0

> **Note:** Apps designed for [Children and Families program](https://play.google.com/about/families/ads-monetization/) should not be using Prodege SDK, since Prodege does not collect responses from users less than 16 years old.

> **Note:** Prodege SDK requires minSdk 21. If your app supports a lower minSdk you can still build your app please refer to section 7.

</br>

# Quick Guide

- Set up Prodege Rewarded Ads
- Set up IronSource Rewarded Ads
- Add Prodege IronSource Adapter to your project
- Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Prodege surveys with IronSource mediation:

## 1. Set Up Prodege Rewarded Ads

### 1.1. Obtain a Publisher Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher).

<br/>

### 1.2. Add new app on the Publisher Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on the [Publisher Dashboard](https://www.pollfish.com/publisher/). Copy then the given API key for this app in order to use later on.

<br/>

### 1.3. Create a Rewarded Ad Placement and copy the given Placement Id

Create a Rewarded placement by clicking "Create a Placement". Provide a name an select the ad unit and ad format. Copy the given placement id in order to use later on.

<br/>

## 2. Set up IronSource Rewarded Ads

### 2.1. Add Prodege Network

First you need to sign in to your [IronSource account](https://platform.ironsrc.com/partners). Add Prodege Network as a **Custom Network**. On the side menu navigate to Monetize -> Setup -> SDK Netwokrs.

Select you application from the Applications list and on the top of the page you will find a **Manage Networks** button. Click it and then click on the **Custom Adapter** option. 

Type **`15bfa6bdd`** as the Custom Adapter Network key on the input prompt and click **Enter Key**. 

<br/>

<img style="margin: 0 auto; display: block; max-height: 200px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_new_network.png"/>

<br/>

You will be prompted to enter your Prodege Reporting Key.
You can retrieve your account key by loging in to the [Publisher Dashboard](https://www.pollfish.com/publisher/) and navigating to your **Account information**.

<br/>

<img style="margin: 0 auto; display: block; max-height: 200px;" src="https://storage.googleapis.com/pollfish_production/doc_images/prodege_reporting_key.png"/>

<br/>

<img style="margin: 0 auto; display: block; max-height: 400px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_network_initial_setup.png"/>

<br/>

Select **Reporting API** for revenue reporting and click **Save**. You will find your newly added Network under the name **Prodege** on each app's mediation network list.

<br/>

<img style="margin: 0 auto; display: block; max-height: 300px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_android_app_networks.png"/>

<br/>

Configure Prodege Network by clicking on the **Setup** button on the **Prodege** network row from your App's Network list.

Fill the following input fields.

| Key                                                                                                                                                             | Level    | Type    | Nullable |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------|----------|
| **2.1.1. `api_key`** <br/> Your application's API key as provided by the [Publisher Dashboard](https://www.pollfish.com/publisher/).                            | App      | String  | No       |
| **2.1.2. `test_mode`** <br/> Toggles the Prodege SDK Test mode.                                                                                                 | App      | String  | Yes      |
| **2.1.3. `placement_id`** <br/> Your ad unit's placement id as provided by the [Publisher Dashboard](https://www.pollfish.com/publisher/).                      | Instance | String  | No       |
| **2.1.4. `request_uuid`** <br/> Sets a pass-through param to be received via the server-to-server callbacks [s2s callbacks](https://www.pollfish.com/docs/s2s). | Instance | String  | Yes      |
| **2.1.5. `muted`** <br/> Toggles Prodege video ads mute state.                                                                                                  | Instance | Boolean | Yes      |

<br/>

### 2.1.1 `api_key`

Your application's API key as provided by the [Publisher Dashboard](https://www.pollfish.com/publisher/).

<br/>

### 2.1.2 `test_mode`

Toggles the Prodege SDK Test mode.

- **`true`** is used to show to the developer how Prodege ads will be shown through an app (useful during development and testing).
- **`false`** is the mode to be used for a released app in any app store (start receiving paid surveys).

<br/>

### 2.1.3 `placement_id`

Your ad unit's placement id as provided by the [Publisher Dashboard](https://www.pollfish.com/publisher/).

<br/>

### 2.1.4 `request_uuid` or `null`

Sets a pass-through param to be received via the server-to-server callbacks.

In order to register for such callbacks you can set up your server URL on your app's page on [Publisher Dashboard](https://www.pollfish.com/publisher/). On each conversion you will receive a callback to your server including the request_uuid param passed.

If you would like to read more on s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

<br/>

### 2.1.5. `muted`

Sets Prodege video ads mute state.

<br/>

<img style="margin: 0 auto; display: block; max-height: 600px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_android_network_configuration.png"/>

<br/>

After adding the above required info click **Save**

<br/>

## 3. Add Prodege IronSource Adapter to your project

### **3.1. Retrieve Prodege IronSource Adapter through maven()**

Retrieve Prodege IronSource Adapter through **maven()** with gradle by adding the following line in your app's module **build.gradle** file:

```groovy
dependencies {
    implementation 'com.pollfish.mediation:prodege-ironsource:7.0.0-beta01.0'
}
```

<br/>

### **3.2. Manual installation**

> **Note:** If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .aar Package option and from the file browser locate the `.aar` file. Right click again on your project and in the Module Dependencies tab choose to add the module that you recently added, as a dependency.

<br/>

### 3.2.1. Download Prodege Android IronSource Adapter `.aar` file and import it into your project's libraries

Click [here](https://storage.googleapis.com/pollfish_production/sdk/IronSource/Prodege%20Android%20IronSource%20Adapter-7.0.0-beta01.0.zip) to download the latest version of Prodege Android IronSource Adapter SDK.

<br/>

### 3.2.2. Download Prodege Android SDK `.aar` file and import it into your project's libraries

Click [here](https://storage.googleapis.com/pollfish_production/sdk/Android/Prodege%20Android%20SDK-7.0.0-beta01.zip) to download the latest version of Prodege Android SDK 

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

Apps updating their target API level to 31 (Android 12) or higher will need to declare a Google Play services normal permission in the AndroidManifest.xml file.

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

You can read more about Google Advertising ID changes [here](https://support.google.com/googleplay/android-developer/answer/6048248).

<br/>

## 4. Request for a RewardedAd

<br/>

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step.

<br/>

Import the following packages.

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

You can view a short example on how to intergate rewarded ads below.

<span style="text-decoration:underline">Kotlin</span>

```kotlin
class MainActivity : AppCompatActivity(), RewardedVideoListener {

    override fun onCreate(savedInstanceState: Bundle?) {
        // ...

        IntegrationHelper.validateIntegration(this)
        IronSource.setRewardedVideoListener(this)
        IronSource.init(this, "APP_KEY")
    }

    override fun onResume() {
        // ...

        IronSource.onResume(this)
    }

    override fun onPause() {
        // ...

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
        // ...

        IntegrationHelper.validateIntegration(this);
        IronSource.setRewardedVideoListener(this);
        IronSource.init(this, "APP_KEY");
    }

    @Override
    protected void onResume() {
        // ...
        
        IronSource.onResume(this);
    }

    @Override
    protected void onPause() {
        // ...

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

If everything worked fine during the previous steps, you are ready to proceed with publishing your app.

> **Note:** After you take your app live, you should request your account to get verified through the [Publisher Dashboard](https://www.pollfish.com/publisher/) in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Prodege to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option. You can read more [here](https://www.pollfish.com/docs/demographic-surveys).

<br/>

# Optional section

## 6. Configure the Prodege SDK programmatically

Prodege IronSource Adapter provided a couple of options you can use to control the behaviour of Prodege SDK. Any configuration, if applied, will override the corresponding configuration done in IronSource's dashboard.

### **6.1. `.setUserId(String)`**

An optional id used to identify a user.

Setting the Prodege's `userId` will override the default behaviour and use that instead of the Advertising Id in order to identify a user.

> **Note:** <span style="color: red">You can pass the id of a user as identified on your system. Prodege will use this id to identify the user across sessions instead of an ad id/idfa as advised by the stores. You are solely responsible for aligning with store regulations by providing this id and getting relevant consent by the user when necessary. Prodege takes no responsibility for the usage of this id. In any request from your users on resetting/deleting this id and/or profile created, you should be solely liable for those requests.</span>

<span style="text-decoration:underline">Kotlin</span>

```kotlin
ProdegeCustomAdapter.setUserId("USER_ID")
```

<span style="text-decoration:underline">Java</span>

```java
ProdegeCustomAdapter.setUserId("USER_ID");
```

<br/>

### **6.2. `.setTestMode(Boolean)`**

- **`true`** is used to show to the developer how Prodege ads will be shown through an app (useful during development and testing).
- **`false`** is the mode to be used for a released app in any app store (start receiving paid surveys).

If you have already specified the test mode on IronSource's UI, this will override the one defined on Web UI.

Prodege IronSource Adapter works by default in live mode. If you would like to test with test ads:

<span style="text-decoration:underline">Kotlin</span>

```kotlin
ProdegeCustomAdapter.setTestMode(true)
```

<span style="text-decoration:underline">Java</span>

```java
ProdegeCustomAdapter.setTestMode(true);
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

You can read more info on how the Prodege SDKs work or how to get started with IronSource at the following links:

[Prodege Android SDK](https://pollfish.com/docs/android)

[IronSource Android SDK](https://developers.is.com/ironsource-mobile/android/android-sdk)
