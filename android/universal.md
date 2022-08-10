<div class="changelog" data-version="6.2.5">
v6.2.5

- Fixing crashes when the back button is pressed

v6.2.4

- Fixing issue with immersive mode in Android APIs lower than 30
- Fixing issue causing RejectedExecutionException

v6.2.3

- Adding support for IronSource mediation adapter

v6.2.2

- Fixing crashes caused by a RuntimeException in Pollfish survey activity

v6.2.1

- Fixing issue with missing android:exported attribute in AndroidManifest.xml

v6.2.0

- Internal fixes

v6.1.6

- Internal fixes

v6.1.5

- Internal fixes

v6.1.4

- Internal fixes

v6.1.3

- Internal fixes

v6.1.2

- Internal fixes

v6.1.1

- Fixed `NullPointerException` on `imageView.animate()`

v6.1.0

- Fixed Pollfish failing to initialize when app returns from Stop state

v6.0.4

- Fixed ThreadPoolScheduler issue

v6.0.3

- Remove Pollfish termination when app goes on background
- Internal fixes

v6.0.2

- Fixed overlay on Unity
- Fixed issues with date formatting on old Android devices

v6.0.1

- Fix Id retrieval issue

v6.0.0

- New Android SDK

</div>

# Prerequisites

- Android SDK 21 or higher
- Java verion 1.8
- Create [Pollfish Developer Account](https://pollfish.com/login/publisher) and register an App

</br>

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

# Migration guide

In this guide you can see the changes on the Pollfish public interface from previous Android SDK versions (prior v6)

<br/>

<details><summary>➤ <b>Kotlin</b> (Click to expand)</summary>

<table>
<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Gradle** <br/>

```groovy
implementation 'com.pollfish:pollfish:5.6.0:universalRelease@aar'
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```groovy
implementation 'com.pollfish:pollfish-universal:6.2.5'
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Import** <br/>

```kotlin
import com.pollfish.constants.Position
import com.pollfish.constants.UserProperties
import com.pollfish.interfaces.*
import com.pollfish.main.PollFish
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```kotlin
import com.pollfish.Pollfish
import com.pollfish.builder.*
import com.pollfish.callback.*
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialisation** <br/>

```kotlin
PollFish.initWith(activity, params)
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```kotlin
Pollfish.initWith(activity, params)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Pollfish Params** <br/>

```kotlin
PollFish.ParamsBuilder("API_KEY")
    ...
    .build()
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```kotlin
Params.Builder("API_KEY")
    ...
    .build()
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **User Properties** <br/>

```kotlin
val userProperties = UserProperties()
    .setCareer(UserProperties.Career.ADVERTISING)
    .setEducation(UserProperties.EducationLevel.POST_GRADUATE)
    ...

params.userProperties(userProperties)
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```kotlin
val userProperties = UserProperties.Builder()
    .career(UserProperties.Career.ADVERTISING)
    .educationLevel(UserProperties.EducationLevel.POST_GRADUATE)
    ...
    .build()

params.userProperties(userProperties)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Show on top of activity** <br/>

```kotlin
PollFish.showOnTopOfActivity(activity)
```

</table>
</details>

<br/>

<details><summary>➤ <b>Java</b> (Click to expand)</summary>
<table>
<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Gradle** <br/>

```groovy
implementation 'com.pollfish:pollfish:5.6.0:universalRelease@aar'
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```groovy
implementation 'com.pollfish:pollfish-universal:6.2.5'
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Import** <br/>

```java
import com.pollfish.constants.Position;
import com.pollfish.constants.UserProperties;
import com.pollfish.interfaces.*;
import com.pollfish.main.PollFish;
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```java
import com.pollfish.Pollfish;
import com.pollfish.builder.*;
import com.pollfish.callback.*;
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialisation** <br/>

```java
PollFish.initWith(activity, params);
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```java
Pollfish.initWith(activity, params)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Pollfish Params** <br/>

```java
PollFish.ParamsBuilder params = new PollFish.ParamsBuilder("API_KEY")
    ...
    .build();
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```java
Params params = new Params.Builder("API_KEY")
    ...
    .build();
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **User Properties** <br/>

```java
UserProperties userProperties = new UserProperties()
    ...
    .setCareer(UserProperties.Career.ADVERTISING)
    .setEducation(UserProperties.EducationLevel.POST_GRADUATE);

params.userProperties(userProperties);
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```java
UserProperties userProperties = new UserProperties.Builder()
    ...
    .career(UserProperties.Career.ADVERTISING)
    .educationLevel(UserProperties.EducationLevel.POST_GRADUATE)
    .build();

params.userProperties(userProperties)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Show on top of activity** <br/>

```java
PollFish.showOnTopOfActivity(activity);
```

</table>
</details>

<br/>

# Quick Guide

1. Obtain a Publisher Account
2. Register a new App on the Pollfish Dashboard and copy the given API key
3. Download and import Pollfish .aar file
4. Embed Pollfish in your code and call init
6. Update your privacy policy, enable **releaseMode** and publish
7. Request your account to get verified from Pollfish Team

<br/>

# Steps Analytically

## 1. Obtain a Publisher Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

## 2. Add new app on Pollfish Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

## 3. Download and import Pollfish .aar file

Download Pollfish Android SDK or reference it through the maven repository.

#### **Download Pollfish Android SDK**

Import Pollfish **.AAR** file to your project libraries  

If you are using Android Studio, right click on your project and select New Module. Then select Import .JAR or .AAR Package option and from the file browser locate Pollfish aar file. Right click again on your project and in the Module Dependencies tab choose to add Pollfish module that you recently added, as a dependency.

**For Java based projects** you will have to include the Kotlin runtime library in your module dependencies and set the java to version 1.8.

```groovy
android {
    ...
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

dependencies {
    ...
    implemetation "org.jetbrains.kotlin:kotlin-stdlib:1.6.10"
}
```

> **Note:** Skipping this step will result on runtime exception during Pollfish initialization.

**OR**

#### **Retrieve Pollfish Android SDK through mavenCentral()**

Retrieve Pollfish through **mavenCentral()** with gradle by adding the following line in your app level **build.gradle** in dependencies section:

```groovy
dependencies {
    ...
    implementation 'com.pollfish:pollfish-universal:6.2.5'
}
```

## 4. Embed Pollfish in your code

<br/>

### 4.1 Import Pollfish classes

Import Pollfish classes with the following lines at the top of your Activity’s class file:

<span style="text-decoration: underline">Kotlin:</span>
```kotlin
import com.pollfish.Pollfish
import com.pollfish.builder.*
import com.pollfish.callback.*
```

<span style="text-decoration: underline">Java:</span>
```java
import com.pollfish.Pollfish;
import com.pollfish.builder.*;
import com.pollfish.callback.*;
```

<br/>

### 4.2 Add support for cleartext http traffic (Optional)

If you are looking to use Pollfish Mediation surveys from all the providers, in order to avoid any faulty behaviour on new Android devices we would advice that you allow cleartext http traffic. To achieve that you need to create a new file named **network_security_config.xml** under **res/xml** and add the following inside:

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true">
        <trust-anchors>
            <certificates src="system" />
        </trust-anchors>
    </base-config>
</network-security-config>
```

add in your Androidmanifest.xml reference the file above in the **android:networkSecurityConfig** tag as below:

```xml
 <application
    ...
    android:networkSecurityConfig="@xml/network_security_config">
```

<br/>

### 4.3 Initialize Pollfish

In order to initialize, you will need to build an instance of Params using `Params.Builder`. The `Params.Builder` has only one mandatory parameter which is the API key of your app (step 2 above). 

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .rewardMode(true)
    .build()

Pollfish.initWith(activity, params);
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = Params.Builder("API_KEY")
    .rewardMode(true)
    .build();

Pollfish.initWith(activity, params);
```

Once you have created the `Params` instance, then you can call `Pollfish.initWith()` in the `onCreate()` function of your Activity and you are ready to go.

Below you can see an example:

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
override fun onCreate(savedInstanceState: Bundle) {
    ...

    Pollfish.initWith(this, params)
}
```

<span style="text-decoration: underline">Java:</span>

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    ...
 
    Pollfish.initWith(this, params);
}
```

<br/>

### 4.3.1 Pollfish initialization Params available options (Optional)

You can set several params to control the behaviour of Pollfish survey panel within your app with the use of `Params` instance. Below you can see all the available options.

<br/>

> **Note:** All the params are optional, except the **`releaseMode`** setting that turns your integration in release mode prior publishing to any Android App store

<br/>

No          | Description
------------|------------
4.3.1.1     | **`.indicatorPosition(Position)`** <br/> Sets the Position where you wish to place the Pollfish indicator
4.3.1.2     | **`.requestUUID(String)`** <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
4.3.1.3     | **`.indicatorPadding(Int)`** <br/> Sets the padding (in dp) from top or bottom according to the Position of the indicator
4.3.1.4     | **`.userLayout(ViewGroup)`** <br/> Sets a layout container that Pollfish surveys will be rendered above it
4.3.1.5     | **`.releaseMode(Boolean)`** <br/>  Sets Pollfish SDK to Developer or Release mode
4.3.1.6     | **`.rewardMode(Boolean)`** <br/> Initializes Pollfish in reward mode
4.3.1.7     | **`.offerwallMode(Boolean)`** <br/> Sets Pollfish to offerwall mode
4.3.1.8     | **`.userProperties(UserProperties)`** <br/> Provides user attributes upfront during initialization
4.3.1.9     | **`.rewardInfo(RewardInfo)`** <br/> An object holding information regarding the survey completion reward. If set, `signature` must be calculated in order to receive surveys. See [here](https://www.pollfish.com/docs/api-documentation) in section **`Notes for sig query parameter`**
4.3.1.10    | **`.clickId(String)`** <br/> A pass through param that will be passed back through server-to-server callback
4.3.1.11    | **`.signature(String)`** <br/> An optional parameter used to secure the `rewardConversion` and `rewardName` parameters passed on `RewardInfo` object

> **Note:** You can also register and listen for different callbacks that fire during a survey lifecycle through the `Params.Builder`. You can read more in section 9.

<br/>

#### **4.3.1.1 `.indicatorPosition(Position)`**

Sets the Position where you wish to place Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png) 

<br/>

Also this setting sets from which side of the screen you would like Pollfish survey panel to slide in.

<br/> 

Pollfish indicator is shown only if Pollfish is used in a non rewarded mode.

<br/>

<span style="text-decoration: underline">There are six different options available: </span> 

* `Position.TOP_LEFT`
* `Position.BOTTOM_LEFT`
* `Position.MIDDLE_LEFT`
* `Position.TOP_RIGHT`
* `Position.MIDDLE_RIGHT`
* `Position.BOTTOM_RIGHT` 

If you do not set explicity a position for Pollfish indicator, it will appear by default at `Position.TOP_LEFT`

<br/>

> **Note:** If you would like to skip the Pollfish Indicator please set the `rewardMode` to `true`

<br/>

Below you can see an example on how you can set Pollfish indicator to slide from top right corner of the screen:

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .indicatorPosition(Position.TOP_RIGHT)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .indicatorPosition(Position.TOP_RIGHT)
    .build();
```

<br/>

> **Note:** This choice affects also from which side the survey panel will slide-in.

<br/>

#### **4.3.1.2 `.requestUUID(String)`**

Sets a unique id to identify a user or a request and be passed back to the publisher through server-to-server callbacks. You can read more on how to retrieve this param through the callbacks [here](https://www.pollfish.com/docs/s2s)

<br/>

Below you can see an example on how you can pass a requestUUID during initialization:

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .requestUUID("YOUR_UUID")
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .requestUUID("YOUR_UUID")
    .build();
```

<br/>

#### **4.3.1.3 `.indicatorPadding(Int)`** 

Sets padding (in dp) of Pollfish indicator, from top or bottom of the screen according to the specified Position of the indicator. Default value is 8. 

<br/>

Below you can see an example on how to add padding of 50 from the bottom of the screen, prior rendering Pollfish indicator.

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .indicatorPosition(Position.BOTTOM_RIGHT)
    .indicatorPadding(50)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .indicatorPosition(Position.BOTTOM_RIGHT)
    .indicatorPadding(50)
    .build();
```

<br/>

> **Note:** If the Pollfish Indicator is used in the middle position, padding is calculated from the top

<br/>

#### **4.3.1.4 `.userLayout(ViewGroup)`**

Sets user's View layout that Pollfish surveys will be rendered above it. If Pollfish regular init function affects the UI of your app by creating flings or any other issues you can try passing a view layout of your app that can be used to render Pollfish surveys above it.

Preferrably you should let the SDK handle rendering on its own.

Here is an example of how a user can pass a `ViewGroup` through `Params.Builder` instance during initialization.

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .userLayout(viewGroup)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .userLayout(viewGroup)
    .build();
```

<br/>

#### **4.3.1.5 `.releaseMode(Boolean)`** 

Sets Pollfish SDK to Developer or Release mode. If you do not set this param it will turn the SDK to Developer mode by default in order for the publisher to be able to test the survey flow.

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

* **Debug/Developer mode** is used to show to the publisher how Pollfish will be shown through an app (useful during development and testing - always returns a survey).  
* **Release mode** is the mode to be used for a released app on any Android App store (start receiving paid surveys).  

<br/>

Below you can see an example on how you can turn your app in Release mode explicitly:

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .releaseMode(true)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .releaseMode(true)
    .build();
```

> **Note:** You should not be testing in release mode since your account can get banned automatically from the system.

<br/>

#### **4.3.1.6 `.rewardMode(Boolean)`**

Initializes Pollfish in reward mode. This means that Pollfish Indicator (section 5.3.1.1) will not be shown and Pollfish survey panel will be automatically hidden until the publisher explicitly calls Pollfish `show` function (The publisher should wait for the Pollfish Survey Received Callback). This behaviour enables the option for the publishers, to show a custom prompt to incentivize the users to participate in a survey.

> **Note:** If not set, the default value is false and Pollfish indicator is shown.

This mode should be used if you want to incentivize users to participate to surveys. We have a detailed guide on how to implement the rewarded approach [here](https://www.pollfish.com/docs/rewarded-surveys)

You can view an example in code on how to achieve this behaviour [here](https://github.com/pollfish/android-sdk-pollfish)

<br/>

Below you can see an example of setting Pollfish to reward mode during initialization:

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .rewardMode(true)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .rewardMode(true)
    .build();
```

> **Note:** Reward mode should be used along with the Survey Received callback so the publisher knows when to prompt the user and call `Pollfish.show()`

<br/>

#### **4.3.1.7 `.offerwallMode(Boolean)`

Enables Pollfish in offerwall mode. If not specified Pollfish shows one survey at a time.

<br/>

Below you can see an example on how you can intialize Pollfish in Offerwall mode:

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .offerwallModel(true)
    .rewardMode(true)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .offerwallModel(true)
    .rewardMode(true)
    .build();
```

> **Note:** Since in order to use Offerwall approach you need to have a virtual economy in place. You should use this with `rewardMode` set to `true`

<br/>

#### **4.3.1.8 `.userProperties(UserProperties)`** 

Passing user attributes to skip or shorten Pollfish Demographic surveys.

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and archieve better fill rate and higher priced surveys.

> **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default.

> **Note:** You can read more on demographic surveys along with a list with all the available options <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

An example of how you can create and pass a `UserProperties` object during initialization can be seen below:

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val userProperties = UserProperties.Builder()
    .parentalStatus(UserProperties.ParentalStatus.TWO)
    .organizationRole(UserProperties.OrganizationRole.ADVERTISING)
    .numberOfEmployees(UserProperties.NumberOfEmployees.FIFTY_ONE_TO_HUNDREND)
    .educationLevel(UserProperties.EducationLevel.POST_GRADUATE)
    .career(UserProperties.Career.ADVERTISING)
    .income(UserProperties.Income.HIGH_I)
    .maritalStatus(UserProperties.MaritalStatus.SINGLE)
    .gender(UserProperties.Gender.MALE)
    .yearOfBirth(1926)
    .addSpokenLanguage(UserProperties.SpokenLanguage.GREEK)
    .addSpokenLanguage(UserProperties.SpokenLanguage.ENGLISH)
    .customAttribute("key", "value")
    .build()

val params = Params.Builder("API_KEY")
    .userProperties(userProperties)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
UserProperties userProperties = new UserProperties.Builder()
    .parentalStatus(UserProperties.ParentalStatus.TWO)
    .organizationRole(UserProperties.OrganizationRole.ADVERTISING)
    .numberOfEmployees(UserProperties.NumberOfEmployees.FIFTY_ONE_TO_HUNDREND)
    .educationLevel(UserProperties.EducationLevel.POST_GRADUATE)
    .career(UserProperties.Career.ADVERTISING)
    .income(UserProperties.Income.HIGH_I)
    .maritalStatus(UserProperties.MaritalStatus.SINGLE)
    .gender(UserProperties.Gender.MALE)
    .yearOfBirth(1926)
    .addSpokenLanguage(UserProperties.SpokenLanguage.GREEK)
    .addSpokenLanguage(UserProperties.SpokenLanguage.ENGLISH)
    .customAttribute("key", "value")
    .build();

Params params = new Params.Builder("API_KEY")
    .userProperties(userProperties)
    .build();
```

<br/>

#### **4.3.1.9 `.rewardInfo(RewardInfo)`**

An object passing information during initialization regarding the reward settings, overriding the values as speciefied on the Publisher's Dashboard

<br/>

```kotlin
data class RewardInfo(
    val rewardName: String,
    val rewardConversion: Double
)
```

Field                  | Description
-----------------------|------------
**`rewardName`**       | Overrides the reward name as specified in the Publisher's Dashboard
**`rewardConversion`** | Overrides the reward conversion as specified on the Publisher's Dashboard. Conversion is expecting a number matching this function ( ```1 USD = X Points``` ) where ```X``` is a ```Double``` number.

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val rewardInfo = RewardInfo("Diamonds", 1.1)

val params = Params.Builder("API_KEY")
    .rewardInfo(rewardInfo)
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
RewardInfo rewardInfo = new RewardInfo("Diamondsd", 1.1);

Params params = new Params.Builder("API_KEY")
    .rewardInfo(rewardInfo)
    .build();
```

> **Note:** It's preferable to handle the reward settings through the Publisher's Dashboard

> **Warning:** If a `rewardInfo` is set, please make sure to calculate and set the correct signature. By skipping this step you will be unable to receive surveys.

<br/>

#### **4.3.1.10 `.clickId(String)`**

A pass through parameter that will be returned back to the publisher through server-to-server callbacks as specified [here](https://www.pollfish.com/docs/s2s)

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .clickId("CLICK_ID")
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .clickId("CLICK_ID")
    .build();
```

<br/>

#### **4.3.1.11 `.signature(String)`**

An optional parameter used to secure the `rewardName` and `rewardConversion` parameters as provided in the `RewardInfo` object (5.3.1.9)

This parameter can be used optionally to prevent tampering around reward conversion, if passed during initialisation. The platform supports url validation by requiring a hash of the `rewardConversion`, `rewardName`, and `clickId`. Failure to pass validation will result in no surveys return and firing **`PollfishSurveyNotAvailable`** callback.

In order to generate the `signature` field you should sign the combination of `rewardConversion+rewardName+clickId` parameters using the HMAC-SHA1 algorithm and your account's secret_key that can be retrieved from the Account Information section on your Pollfish Dashboard.

Please keep in mind if your `rewardConversion` is a whole number, you have to calculate the signature useing the floating point value with 1 decimal point.

```kotlin
val rewardConversion = 2
val rewardName = "Dollars"
val clickId = "CLICK_ID"

val valueToSign = "2.0DollarsCLICK_ID" // This will be signed using HMAC-SHA1 and your account's secret key
```

The `signature` value should then be encoded using Base64.

> **Note:** Although `rewardConversion` is mandatory for the hashing to work, the `rewardName` and `clickId` parameters are optional and you should add them for extra security.

<br/>

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
val params = Params.Builder("API_KEY")
    .signature("SIGNATURE")
    .build()
```

<span style="text-decoration: underline">Java:</span>

```java
Params params = new Params.Builder("API_KEY")
    .signature("SIGNATURE")
    .build();
```

<br/>

**At this point you are ready to go live! Turn your app to Release mode by setting `.releaseMode(true)` and submit your app to any Android App stroe.**

<br/>

## 5. Update your privacy policy, enable releaseMode and publish

Add the following paragraph to your app's privacy policy:


*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Publishers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user's device data (including Advertising ID, Device ID, other available electronic identifiers and further response meta-data is automatically sent, via our app, to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully the Pollfish respondent terms located at [https://www.pollfish.com/terms/respondent](https://www.pollfish.com/terms/respondent). These data will be associated with your answers to the questionnaires whenever Pollfish sends such questionnaires to eligible users. Pollfish may share such data with third parties, clients and business partners, for commercial purposes. By downloading the application, you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by visiting the following link [https://www.pollfish.com/respondent/opt-out](https://www.pollfish.com/respondent/opt-out). We once more invite you to check the Pollfish respondent's terms of use, if you wish to have more detailed view of the way Pollfish works and with whom Pollfish may further share your data."*  

<br/>

> **Note:** It's important that you include this disclosure both in the privacy policy posted on your App Store but also in the privacy policy included in your app. 

<br/>

**At this point you are ready to go live! Sign your app with a release key or explicitly set .releaseMode(true) - in your Params.Builder and publish to any Android app store**

---
<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://help.pollfish.com/en/articles/1163768-why-i-cannot-see-any-surveys-on-my-app">FAQ page</a>
<br/><br/>

> **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a Standalone Demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process that users need to go through, in order to join the platform. If a paid survey is available at that point of time, the demographic questions will be inserted at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market research. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this type of targeting.

<br/>
<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>
<br/>


In our efforts to include publishers and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Cost Per Action (CPA) field which will be 0 USD cents and also Survey Type which will be `Pollfish/Demographics`. Secondly, publishers can disable the Standalone Demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 5.3.1.8 and skip or shorten this way, Pollfish Demographic surveys.

<br/>
### 5.1 Complete the Google Play Data Safety questionnaire

When you publish your app your will be asked to complete the Google Play Data Safety questionnaire. For any info relevant to data collected and used from the Pollfish SDK please advice the following [link](https://www.pollfish.com/terms/google-play-data-safety-questionnaire). 
<br/>	
	 
# 6. Request your account to get verified from Pollfish Team

After your app is published on an app store you should request your account to get verified from your Pollfish Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.

> **Note:** Review process can take from a few minutes to a few hours depending on the 24/7 Pollfish Review Team availability.

<br/>

# Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour like listening and acting on different callbacks. All the steps below are optional.

<br/>

# 7. Manually show or hide Pollfish

You can manually show or hide Pollfish survey panel by calling anywhere after initialization and when a survey is received:  

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Pollfish.show()
```

<span style="text-decoration: underline">Java:</span>

```java
Pollfish.show();
```

**or**

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Pollfish.hide()
```

<span style="text-decoration: underline">Java:</span>

```java
Pollfish.hide();
```

<br/>

# 8. Listening for Pollfish Survey lifecycle events

In order to get notified for Pollfish Survey lifecycle events you will have to register and listen to the appropriate listeners either by:
* implementing the relevant interfaces on the Activity level 
* or by passing the interface through the `Params.Builder` (section 5).

<br/>

There are seven available interfaces to implement:

No  | Interface | Method
----|-----------|-------------
8.1 | `PollfishSurveyReceivedListener` | **`pollfishSurveyReceived(SurveyInfo?)`** <br/> Get notified when a survey is received
8.2 | `PollfishSurveyCompletedListener` | **`pollfishSurveyCompleted(SurveyInfo)`** <br/> Get notified when a survey is completed
8.3 | `PollfishUserNotEligibleListener` | **`pollfishUserNotEligible`** <br/> Get notified when a user is not eligible for a Pollfish survey
8.4 | `PollfishSurveyNotAvailableListener` | **`pollfishSurveyNotAvailable`** <br/> Get notified when no survey is available
8.5 | `PollfishOpenedListener` | **`pollfishOpened`** <br/> Get notified when Pollfish panel has opened
8.6 | `PollfishClosedListener` | **`pollfishClosed`** <br/> Get notified when Pollfish panel has closed
8.7 | `PollfishUserRejectedSurveyListener` | **`pollfishUserRejectedSurvey`** <br/> Get notified when a user rejected a survey

<br/>

**`SurveyInfo`**

This object contains information regarrding the survey that has been received or completed by the user.

```kotlin
data class SurveyInfo(
    val surveyCPA: Int?,
    val surveyIR: Int?,
    val surveyLOI: Int?,
    val surveyClass: String?,
    val rewardName: String?,
    val rewardValue: Int?,
    val remainingCompletes: Int?
) 
```

Field | Description
------------ | -------------
**`surveyCPA`**                | Money to be earned from survey received in US dollar cents (estimated based on daily exchange currency)
**`surveyIR`**                 | The current estimation for the survey incidence rate as an integer number in the range 0-100. This param is optional and will have as default the value -1 if it was not set and the IR was not computed reliably
**`surveyLOI`**                | The expected time in minutes that it takes to complete the survey. This param is optional and will have as default the value -1 if it was not set and the LOI was not computed reliably
**`surveyClass`**        | Information about the survey network and type
**`rewardName`**         | A virtual reward name as specified on Publisher Dashboard 
**`rewardValue`**        | A virtual reward value as calculated via a given exchange rate on Publisher Dashboard 
**`remainingCompletes`** | The number of remaining completes for the survey

<br/>

The syntax for survey_class values is:

```
survey_class: provider["/"type]
provider: "Pollfish" | "Toluna" | "Cint" | "InnovateMR" | "SaySo" | "Dynata" | "Yuno" | "PureSpectrum" | "Opinionetwork" | "SchlesingerGroup" | "YunoRouter" | "IpsosMediation" | "ProdegeMR"
type: "Basic" | "Playful" | "ThirdParty" | "Demographics" | "Internal"
```

which is the network name followed by an optional slash and survey type.

The provider is the network that provides the survey. The syntax rule has all the networks currently supported by Pollfish.

The type is that of the survey as described in the network's documentation. The exception is the type "Demographics" which
is always used to identify surveys whose purpose is to collect demographic data for the users.

The whole set of values currently supported are:

| Value              | Description
|:------------------|:----------------
| **`Pollfish`**              | Pollfish Basic survey
| **`Pollfish/Basic`**        | Pollfish Basic survey (another name)
| **`Pollfish/Playful`**      | Pollfish Playful survey 
| **`Pollfish/ThirdParty`**   | Pollfish 3rd party survey
| **`Pollfish/Demographics`** | Pollfish Demographic survey
| **`Pollfish/Internal`**     | Pollfish internal survey created by the publisher
| **`Toluna`**                | Toluna survey   
| **`Cint`**                  | Cint survey   
| **`InnovateMR`**            | InnovateMR survey   
| **`SaySo`**                 | SaySo survey   
| **`Dynata`**                | Dynata survey
| **`Yuno`**       | Yuno survey 
| **`PureSpectrum`**       | PureSpectrum survey 
| **`Opinionetwork`**       | Opinionetwork survey
| **`SchlesingerGroup`**       | SchlesingerGroup survey
| **`YunoRouter`**       | YunoRouter survey 
| **`IpsosMediation`**       | IpsosMediation survey 
| **`ProdegeMR`**       | ProdegeMR survey 

<br/>

> **Note:** When a new mediation network enters the Pollfish network the appropriate values will be added.

<br/>

## 8.1. Get notified when a Pollfish survey is received

You can be notified when a Pollfish survey is received. With this notification publisher can also get informed about the type of survey that was received, money to be earned if survey gets completed, shown in USD cents and other info around the survey such as LOI and IR.

To listen for this event you should implement `PollfishSurveyReceivedListener` Interface and override `onPollfishSurveyReceived` function

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
class MainActivity : AppCompatActivity(), PollfishSurveyReceivedListener {
    
    override fun onPollfishSurveyReceived(surveyInfo: SurveyInfo?) {
        ...
    }

}
```

<span style="text-decoration: underline">Java:</span>

```java
public class MainActivity extends AppCompatActivity implements PollfishSurveyReceivedListener {

    @Override
    public void onPollfishSurveyReceived(@Nullable SurveyInfo surveyInfo) {
        ...
    }

}
```

**or**

Pass an inline object in `Params.Builder`

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Params.Builder("API_KEY")
    .pollfishSurveyReceivedListener(object : PollfishSurveyReceivedListener {
        override fun onPollfishSurveyReceived(surveyInfo: SurveyInfo?) {
            ...
        }
    })
```

<span style="text-decoration: underline">Java:</span>

```java
new Params.Builder("API_KEY")
    .pollfishSurveyReceivedListener( surveyInfo -> { 
        ...
    })
```

<br/>

> **Note:** When Offerwall mode is enabled, Survey Received callback returns a `null` `SurveyInfo` object. It just notifies that surveys are available within the Offerwall.

<br/>

## 8.2. Get notified when a Pollfish survey is completed

You can be notified when a user completed a survey. With this notification, publisher can also get informed about the type of survey, money earned from that survey in USD cents and other info around the survey such as LOI and IR.

To listen for this event you should implement  `PollfishSurveyCompletedListener` Interface and override `onPollfishSurveyCompleted` function

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
class MainActivity : AppCompatActivity(), PollfishSurveyCompletedListener {
    
    override fun onPollfishSurveyCompleted(surveyInfo: SurveyInfo) {
        ...
    }

}
```

<span style="text-decoration: underline">Java:</span>

```java
public class MainActivity extends AppCompatActivity implements PollfishSurveyCompletedListener {

    @Override
    public void onPollfishSurveyCompleted(@NotNull SurveyInfo surveyInfo) {
        ...
    }

}
```

**or**

Pass an inline object in `Params.Builder`

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Params.Builder("API_KEY")
    .pollfishSurveyCompletedListener(object : PollfishSurveyCompletedListener {
        override fun onPollfishSurveyCompleted(surveyInfo: SurveyInfo) {
            ...    
        }
    })
```

<span style="text-decoration: underline">Java:</span>

```java
new Params.Builder("API_KEY")
    .pollfishSurveyCompletedListener( surveyInfo -> { 
        ...
    })
```

<br/>

## 8.3. Get notified when a user is not eligible for a Pollfish survey

You can be notified when a user is not eligible for a Pollfish survey. In market research monetization users can get screened out while completing a survey because they are not relevant with audience that the market researcher was looking for. In that case the user not eligible notification will fire and the publisher will make no money from that survey. User not eligible notification will fire after survey received when user starts completing the survey.

To listen for this event you should implement  `PollfishUserNotEligibleListener` Interface and override `onUserNotEligible` function

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
class MainActivity : AppCompatActivity(), PollfishUserNotEligibleListener {
   
    override fun onUserNotEligible() {
        ...
    }

}
```

<span style="text-decoration: underline">Java:</span>

```java
public class MainActivity extends AppCompatActivity implements PollfishUserNotEligibleListener {

    @Override
    public void onUserNotEligible() {
        ...
    }

}
```

**or**

Pass an inline object in `Params.Builder`

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Params.Builder("API_KEY")
    .pollfishSurveyCompletedListener(object : PollfishUserNotEligibleListener {
        override fun onUserNotEligible() {
            ...    
        }
    })
```

<span style="text-decoration: underline">Java:</span>

```java
new Params.Builder("API_KEY")
    .pollfishUserNotEligibleListener( () -> { 
        ...
    })
```

<br/>

## 8.4. Get notified when no surveys are available for that user

You can be notified when Pollfish survey is not available. 

To listen for this event you should implement  `PollfishSurveyNotAvailableListener` Interface and override `onPollfishSurveyNotAvailable` function

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
class MainActivity : AppCompatActivity(), PollfishSurveyNotAvailableListener {
    
    override fun onPollfishSurveyNotAvailable() {
        ...
    }

}
```

<span style="text-decoration: underline">Java:</span>

```java
public class MainActivity extends AppCompatActivity implements PollfishSurveyNotAvailableListener {

    @Override
    public void onPollfishSurveyNotAvailable() {
        ...
    }

}
```

**or**

Pass an inline object in `Params.Builder`

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Params.Builder("API_KEY")
    .pollfishSurveyNotAvailableListener(object : PollfishSurveyNotAvailableListener {
        override fun onPollfishSurveyNotAvailable() {
            ...    
        }
    })
```

<span style="text-decoration: underline">Java:</span>

```java
new Params.Builder("API_KEY")
    .pollfishSurveyNotAvailableListener( () -> { 
        ...
    })
```

<br/>

## 8.5. Get notified when Pollfish Survey panel has opened

You can register and get notified when a Pollfish survey panel has opened. Publishers usually use this notification to pause a game until Pollfish panel is closed again.

To listen for this event you should implement  `PollfishOpenedListener` Interface and override `onPollfishOpened` function

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
class MainActivity : AppCompatActivity(), PollfishOpenedListener {
    
    override fun onPollfishOpened() {
        ...
    }

}
```

<span style="text-decoration: underline">Java:</span>

```java
public class MainActivity extends AppCompatActivity implements PollfishOpenedListener {

    @Override
    public void onPollfishOpened() {
        ...
    }

}
```

**or**

Pass an inline object in `Params.Builder`

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Params.Builder("API_KEY")
    .pollfishOpenedListener(object : PollfishOpenedListener {
        override fun onPollfishOpened() {
            ...    
        }
    })
```

<span style="text-decoration: underline">Java:</span>

```java
new Params.Builder("API_KEY")
    .pollfishOpenedListener( () -> { 
        ...
    })
```

<br/>

## 8.6. Get notified when Pollfish Survey panel has closed

You can register and get notified when a Pollfish survey panel has closed. Publishers usually use this notification to resume a game that they have previously paused when Pollfish panel opened.

To listen for this event you should implement  `PollfishClosedListener` Interface and override `onPollfishClosed` function

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
class MainActivity : AppCompatActivity(), PollfishClosedListener {
    
    override fun onPollfishClosed() {
        ...
    }

}
```

<span style="text-decoration: underline">Java:</span>

```java
public class MainActivity extends AppCompatActivity implements PollfishClosedListener {

    @Override
    public void onPollfishClosed() {
        ...
    }

}
```

**or**

Pass an inline object in `Params.Builder`

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Params.Builder("API_KEY")
    .pollfishClosedListener(object : PollfishClosedListener {
        override fun onPollfishClosed() {
            ...    
        }
    })
```

<span style="text-decoration: underline">Java:</span>

```java
new Params.Builder("API_KEY")
    .pollfishClosedListener( () -> { 
        ...
    })
```

<br/>

## 8.7 Get notified when a user rejected a survey

You can register and get notified when a user rejected a survey

To listen for this event you should implement  `PollfishUserRejectedSurveyListener` Interface and override `onUserRejectedSurvey` function

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
class MainActivity : AppCompatActivity(), PollfishUserRejectedSurveyListener {
    
    override fun onUserRejectedSurvey() {
        ...
    }

}
```

<span style="text-decoration: underline">Java:</span>

```java
public class MainActivity extends AppCompatActivity implements PollfishUserRejectedSurveyListener {

    @Override
    public void onUserRejectedSurvey() {
        ...
    }

}
```

**or**

Pass an inline object in `Params.Builder`

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Params.Builder("API_KEY")
    .pollfishUserRejectedSurveyListener(object : PollfishUserRejectedSurveyListener {
        override fun onUserRejectedSurvey() {
            ...    
        }
    })
```

<span style="text-decoration: underline">Java:</span>

```java
new Params.Builder("API_KEY")
    .pollfishUserRejectedSurveyListener( () -> { 
        ...
    });
```

<br/>

# 9. Check if Pollfish survey is still available on your device

After you initialize Pollfish and a survey is received you can check at any time if the survey is available at the device by calling the following function.

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Pollfish.isPollfishPresent()
```

<span style="text-decoration: underline">Java:</span>

```java
Pollfish.isPollfishPresent();
```

<br/>


# 10. Check if Pollfish survey panel is open

You can check at any time if the survey panel is open by calling the following function.

<span style="text-decoration: underline">Kotlin:</span>

```kotlin
Pollfish.isPollfishPanelOpen()
```

<span style="text-decoration: underline">Java:</span>

```java
Pollfish.isPollfishPanelOpen();
```

<br/>

# 11. Proguard

If you use proguard with your app, please insert the following lines in your proguard configuration file:  

```java
-dontwarn com.pollfish.**
-keep class com.pollfish.** { *; }
```

<br/>

# 12. Server-to-server callbacks on survey completion

If you want to reward your users for completing a survey it is common practice to verify this through server to server callbacks in order to introduce an enhanced security layer to your system. You can easily add your postback  url on your app's page on Pollfish Dashboard. You can read more on how to set server to server callbacks <a href="https://www.pollfish.com/docs/s2s">here</a>.

<br/>

# 13. Payouts on Screenouts

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described <a href="https://www.pollfish.com/docs/pay-on-screenouts">here</a>. 
