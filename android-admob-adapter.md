This guide is for publishers looking to use AdMob mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

##### Prerequisites

Android SDK 4.1 (API level 16) or later

</br></br>

### Step 1: Implement AdMob Rewarded Ads

Implement [Rewarded Ads](https://developers.google.com/admob/android/rewarded-ads) as described in AdMob.

### Step 2: Set Up Pollfish

#### 2.1\.. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

#### 2.2\. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

#### 2.3\. Add Pollfish aar library to your project

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

#### 2.4\. Integrate Google Play Services to your project

Applications that integrate Pollfish SDK are required to include Google Play Services library in order to give access to the Advertising ID of a device to the SDK. Further details regarding integration with the Google Play services library can be found [here](https://developers.google.com/android/guides/setup).

```java
dependencies {
    implementation 'com.google.android.gms:play-services-ads-identifier:16.0.0'
    implementation 'com.google.android.gms:play-services-base:16.0.1'
}
```

### Step 3: Configure mediation settings for your AdMob Rewarded Ad unit

You need to add Pollfish to the mediation configuration for your Rewarded Ad unit. 

First you need to sign in to your [AdMob account](https://apps.admob.com/). On the left side menu, click on the **Mediation** and then in **Mediation Groups** Tab. If you already have an existing Mediation Group you will need to modify it (click on the name of the Mediation Group and press **Edit**).

if you do not have a Mediation Group yet, click to create one with **CREATE MEDIATION GROUP**.

In the Ad Format drop down menu select **Rewarded** and for platform **Android**


<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/new_mediation_group.png"/>
<br/>

and then you can name the Mediation Group if you do not have one already. Next, set the mediation group status to **Enabled**

Afterwards you should click **ADD AD UNITS** and associate the Mediation group with an existing AdMob Rewarded Ad unit.

You should now see the ad units card populated with the ad units you selected, as shown below:

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/ad_units.png"/>

You then have to add Pollfish Network to the Mediationn Waterfall of the group. Click on **ADD CUSTOM EVENT**

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/add_source.png/>

