This guide is for publishers looking to use AdMob mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

### Prerequisites

Android SDK 4.1 (API level 16) or later

### Step 1: Implement AdMob Rewarded Ads

Implement (Rewarded Ads](https://developers.google.com/admob/android/rewarded-ads) as described in AdMob.

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

