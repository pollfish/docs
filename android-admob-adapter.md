<div class="changelog" data-version="5.0.2.1">

v5.0.2
	
- Initial Release

</div>

</br>

This guide is for publishers looking to use AdMob mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

##### Prerequisites

Android SDK 4.1 (API level 16) or later

</br>

Below you can find a step by step guide on how to incorporate Pollfish surveys with AdMob mediation:

### Step 1: Implement AdMob Rewarded Ads in your app 

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


### Step 2: Configure Mediation Settings for your AdMob Rewarded Ad unit

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
You then have to add Pollfish Network to the Mediationn Waterfall of the group. Click on **ADD CUSTOM EVENT**

You can add a name, in the **Label** section, to differentiate Pollfish Network from your other ad sources (for example Pollfish Netowrk) and an estimated eCPM. Pollfish surveys average eCPMs, range usually betweenn $70-$80.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/custom_event_aa.png"/>
<br/>

You can then configure Pollfish ad unit by adding the class name of Pollfish AdMob Mediation Adapter

**Class Name:** com.pollfish.mediation.PollfishAdMobAdapter<br/>

Optionally users can pass Pollfish API key (check section below 3.2) to the adapter from here. Pollfish SDK works by default in production mode. If you would like to test with test surveys we will explain below how to achieve that.

**Parameter:** Your Pollfish API Key (optional)

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/network_pollfish.png"/>
<br/>


### Step 3: Set Up Pollfish

#### 3.1\. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

#### 3.2\. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

#### 3.3\. Add Pollfish aar library to your project

Download Pollfish Android SDK or reference it through jCenter().

#### **Download Pollfish Android SDK**

Import Pollfish **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

#### **Retrieve Pollfish Android SDK through jCenter()**

Retrieve Pollfish through **jCenter()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```
dependencies {
  implementation 'com.pollfish:pollfish:5.0.2:googleplayRelease@aar'
}
```

#### 3.4\. Integrate Google Play Services to your project

Applications that integrate Pollfish SDK are required to include Google Play Services library in order to give access to the Advertising ID of a device to the SDK. Further details regarding integration with the Google Play services library can be found [here](https://developers.google.com/android/guides/setup).

```java
dependencies {
    implementation 'com.google.android.gms:play-services-ads-identifier:16.0.0'
    implementation 'com.google.android.gms:play-services-base:16.0.1'
}
```

### Step 4: Add Pollfish AdMob Adapter to your project

Import Pollfish AdMob Adapter **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish AdMob Adapter aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**OR**

#### **Retrieve Pollfish AdMob Adapter through jCenter()**

Retrieve Pollfish through **jCenter()** with gradle by adding the following line in your project **build.gradle** (not the top level one, the one under 'app') in  dependencies section:  

```
dependencies {
  implementation 'com.pollfish.mediation:pollfish-admob:5.0.2.1'
}
```

### Step 5: Use and control Pollfish AdMob Adapter in your Rewarded Ad Unit 

Pollfish AdMob Adapter provides different options that you can use to control the behaviour of Pollfish SDK.

<br/>
Below you can see all the available options of **PollfishExtrasBundleBuilder** instance that is used to configure the behaviour of Pollfish SDK.
<br/>

No | Description
------------ | -------------
5.1 | **.setAPIKey(String apiKey)**  <br/> Sets Pollfish SDK API key as provided by Pollfish
5.2 | **.setRequestUUID(String requestUUID)**  <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
5.3 | **.setReleaseMode(boolean releaseMode)**  <br/> Sets Pollfish SDK to Developer or Release mode


#### 5.1 .setAPIKey(String apiKey)

Pollfish API Key as provided by Pollfish on Pollfish Dashboard. This value will be used only if you did not specify the API Key in AdMob's UI as desribed in step 2. If you have already specified Pollfish API Key on AdMob's UI, this param will be ignored.

#### 5.2 .setRequestUUID(String requestUUID)

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

#### 5.3 .setReleaseMode(boolean releaseMode)

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish AdMob Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

Below you can see an example on how you can initialize a request for PollfishAdMobAdapter:

```
import com.pollfish.mediation.PollfishAdMobAdapter;
import com.pollfish.mediation.PollfishExtrasBundleBuilder;
```
</br>
```
Bundle pollfishBundle = new PollfishExtrasBundleBuilder()
    .setAPIKey("YOUR_POLLFISH_API_KEY")
    .setReleaseMode(false)
    .setRequestUUID("MY_ID")
    .build();

AdRequest request = new AdRequest.Builder()
                .addTestDevice("xxxxx-xxxx-xxxxxxx")
                .addNetworkExtrasBundle(PollfishAdMobAdapter.class, pollfishBundle)
                .build();
```

### Step 6: Publish 

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option.

