<div class="changelog" data-version="6.0.0-beta">
v.6.0.0

- New Pollfish Swift framework

</div>

# <span style="color:red">Beta version of the upcoming Pollfish iOS SDK v6</span>


Please read the migration guide below.

## Prerequisites

* Use XCode 12 or higher
* Target iOS 9.0 or higher
* Create [Pollfish Developer Account](https://pollfish.com/login/publisher) and register an App
* IDFA tracking permission (iOS 14+)

> **Note:** Pollfish cannot function without the usage of IDFA. Insructions on how to request permission can be found in section 5.

</br>


## Migration guide

In this guide you can see the changes on the Pollfish public interface 

<br/>

<details><summary>Swift</summary>

<table>
<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialisation** <br/>

```swift
Pollfish.initWithAPIKey("API_KEY", andParams: params)
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```swift
Pollfish.initWith(params, delegate: self)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Pollfish Params** <br/>

```swift
let pollfishParams = PollfishParams()

pollfishParams.indicatorPadding = 10;
pollfishParams.releaseMode = true;
...
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```swift
let params = PollfishParams("API_KEY")
    .indicatorPadding(10)
    .releaseMode(true)
    ...
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **User Properties** <br/>

```swift
let userAttributes = UserAttributesDictionary()

userAttributes?.setGender(GENDER(MALE))
userAttributes?.setRace(RACE(WHITE))
userAttributes?.setYearOfBirth(YEAR_OF_BIRTH(_1984))

params.userAttributes = userAttributes
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```swift
let userProperties = UserProperties([
    .gender(.male),
    .race(.white),
    .yearOfBirth(1984)
])

params.userProperties(userProperties)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Pollfish Lifecycle callbacks** <br/>

```swift
NotificationCenter.default.addObserver(
    forName: NSNotification.Name(rawValue: "PollfishSurveyNotAvailable"),
    object: nil,
    queue: nil,
     using:pollfishNotAvailable)

func pollfishNotAvailable(_ notification:Notification) {
    ...
}
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```swift
Pollfish.initWith(params, delegate: self)

extension ViewController: PollfishDelegate {

    func pollfishSurveyNotAvailable() {
        ...
    }

}
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Rotation handling** <br/>

> **Note:** Rotation changes are handled by the SDK

```swift
NotificationCenter.default.addObserver(
    forName: UIDevice.orientationDidChangeNotification,
    object: nil,
    queue: nil,
    using:rotateApp)

func rotateApp(_ notification:Notification){
    initPollfish();
}
```

</table>
</details>

<br/>


<details><summary>Objective C</summary>
<table>
<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Initialisation** <br/>

```objc
[Pollfish initWithAPIKey:@"API_KEY" andParams:params];
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```objc
[Pollfish initWith:params delegate:nil];
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Pollfish Params** <br/>

```objc
PollfishParams *pollfishParams =  [PollfishParams initWith:^(PollfishParams *pollfishParams) {
    pollfishParams.indicatorPadding=10;
    pollfishParams.releaseMode=true;
    ...
}
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];
[params indicatorPadding:10];
[params releaseMode:true];
...
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **User Properties** <br/>

```objc
UserAttributesDictionary *userAttributesDictionary = [UserAttributesDictionary alloc] init];
    
[userAttributesDictionary setGender: GENDER(MALE)];
[userAttributesDictionary setRace:RACE(WHITE)];
[userAttributesDictionary setYearOfBirth:YEAR_OF_BIRTH(_1984)];

params.userAttributes=userAttributesDictionary;
```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```objc
UserProperties *userProperties = [[UserProperties alloc] init];
])

[userProperties gender:GenderMale];
[userProperties race:RaceWhite];
[userProperties yearOfBirth:1995];

params.userProperties(userProperties)
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Pollfish Lifecycle callbacks** <br/>

```objc
[[NSNotificationCenter defaultCenter] addObserver:self 
    selector:@selector(pollfishNotAvailable) name:@"PollfishSurveyNotAvailable" 
    object:nil];

- (void)pollfishNotAvailable
{
   ...
}

```

<tr>
<td>

<span style="color:green">+</span>

<td>
<br/>

```objc
// ViewController.h
@interface ViewController : UIViewController<PollfishDelegate>

@end

// ViewController.m
...

- (void) pollfishSurveyNotAvailable
{
    ...
}
```

<tr>
<td>
<br/>

<span style="color:red">-</span>

<td>

#### **Rotation handling** <br/>

> **Note:** Rotation changes are handled by the SDK

```objc
[[NSNotificationCenter defaultCenter] addObserver:self 
    selector:@selector(didRotate:) 
    name:UIDeviceOrientationDidChangeNotification 
    object:nil];

- (void) didRotate:(NSNotification *)notification
{
    [self initPollfish];
}
```

</table>
</details>

<br/>

## Quick Guide

1. Obtain a Developer Account
2. Register a new App on Pollfish Developer Dashboard and copy the given API Key
3. Download and import Pollfish.xcframework to your project
4. Add AdSupport.framework, AppTackingTransparency.framework, SystemConfiguration.framework and CoreTelephony.framework to your project
5. Request IDFA tracking permission
6. Embed pollfish in your code and call init
7. Set to **Release mode** and release in AppStore
8. Update your privacy policy
9. Request your account to get verified from Pollfish Team

<br/>

## Steps Analytically

### 1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://pollfish.com/login/publisher)

<br/>

### 2. Register a new App on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](https://pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

<br/>

### 3. Download and import Pollfish.xcframework to your project

Download Pollfish iOS SDK from the website and then in Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.  

The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane).  

<br/>

### 4. Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework
- SystemConfiguration.framework 

<br/>

### 5. Request IDFA Tracking permission

To display the App Tracking Transparency authorization request for accessing the IDFA, update your `Info.plist` to add the `NSUserTrackingUsageDescription` key with a custom message describing your usage. Below is an example description text:

```xml
<key>NSUserTrackingUsageDescription</key>
<string>This identifier will be used to deliver personalized surveys to you.</string>
```

To present the authorization request, call `requestTrackingAuthorization`. We recommend waiting for the completion callback prior to initializing.

<span style="text-decoration: underline">Objective-C:</span>
```objc
#import <AppTrackingTransparency/AppTrackingTransparency.h>
#import <AdSupport/AdSupport.h>

- (void) requestIDFA {
    [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
        if (status == ATTrackingManagerAuthorizationStatusAuthorized) {
            // Tracking authorization completed. 
            // Initialize Pollfish here.
            [self initPollfish];
        }
    }];
}
```

<span style="text-decoration: underline">Swift</span>
```swift
import AppTrackingTransparency
import AdSupport

func requestIDFA() {
    ATTrackingManager.requestTrackingAuthorization { status in
        if status == .authorized {
            // Tracking authorization completed. 
            // Initialize Pollfish here.
            self.initPollfish()
        }
    }
}
```

> **Note:** This step is required only for iOS 14+ targeting. If you sould like to see an example in code visit this [repository](https://github.com/pollfish/ios-sdk-pollfish)

<br/>

### 6. Embedding Pollfish into your code

<br/>

### 6.1 Import Pollfish Module

You have to import Pollfish Module in any file that you will use Pollfish.

<span style="text-decoration: underline">Objective-C:</span>
```objc
@import Pollfish;
```

<span style="text-decoration: underline">Swift</span>
```swift
import Pollfish
```
<br/>

### 6.2 Initialize Pollfish

A good place to call Pollfish init function is in the application’s delegate `applicationDidBecomeActive` method. This way it is ensured that Pollfish surveys will be refreshed each time the application will become active. (another placement could be in the `viewDidLoad` or `viewWillAppear` methods of a `ViewController`).

In order to initialize, you need an instance of `PollfishParams` on which you will pass the API key of your app (step 2 above). `PollfishParams` has several params that affect the behaviour of Pollfish survey panel.

Below you can see an example on how you can initialize Pollfish with the help of `PollfishParams` object:

> **Note:** In order to receive Pollfish lifecycle events see section 11.

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) applicationDidBecomeActive:(UIApplication *)application 
{
    PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

    [params rewardMode:BOOL];
    [params releaseMode:BOOL];
    [params offerwallMode:BOOL];

    [Pollfish initWith:params delegate:self];
}
```

<span style="text-decoration: underline">Swift:</span>
```swift
func applicationDidBecomeActive(application: UIApplication) {

    let params = PollfishParams("API_KEY")
        .rewardMode(Bool)
        .releaseMode(Bool)
        .offerwallMode(Bool)
    
    Pollfish.initWith(params)
}
```

<span style="text-decoration: underline">SwiftUI</span>
```swift
struct ContentView: View {
    var pollfishView = PollfishView()
    
    var body: some View {
        NavigationView {
            pollfishView
        }.onAppear() {
            self.initPollfish()
        }
    }

    func initPollfish() {
        let params = PollfishParams("API_KEY")
            .rewardMode(Bool)
            .releaseMode(Bool)
            .offerwallMode(Bool)
            .viewContainer(PollfishView.view)
            
        Pollfish.initWith(params)
    }
}
```

> **Note:** For instructions on how to define a ```SwiftUI``` ```PollfishView``` see section 6.2.4

<br/>

### 6.2.1 PollfishParams available options (optional)

You can set several params to control the behaviour of Pollfish survey panel within your app wih the use of PollfishParams instance. Below you can see all the available options. 

<br/>

> **Note:** All the params are optional, except the **`releaseMode`** setting that turns your integration in release mode prior publishing to the AppStore 

<br/>

No | Description
------------ | -------------
6.2.1 | **`.indicatorPosition(IndicatorPosition)`** <br/> Sets the Position where you wish to place the Pollfish indicator
6.2.2 | **`.requestUUID(String)`** <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
6.2.3 | **`.indicatorPadding(Int)`** <br/> Sets the padding from the top or the bottom of the view, according to the Position of Pollfish indicator
6.2.4 | **`.viewContainer(UIView)`** <br/> Sets a view container that Pollfish surveys will be rendered above it
6.2.5 | **`.releaseMode(Bool)`** <br/> Sets Pollfish SDK to Developer or Release mode
6.2.6 | **`.rewardMode(Bool)`** <br/> Initializes Pollfish in reward mode
6.2.7 | **`.offerwallMode(Bool)`** <br/> Sets Pollfish to offerwall mode
6.2.8 | **`.userProperties(UserProperties)`** <br/> Provides user attributes upfront during initialization
6.2.9| **`.rewardInfo(RewardInfo)`** <br/> An object holding information regarding the survey completion reward
6.2.10| **`.clickId(String)`** <br/> A pass throught param that will be passed back through server-to-server callback
6.2.11| **`.singnature(String)`** <br/> An optional parameter used to secure the `rewardConversion` and `rewardName` parameters passed on `RewardInfo` object

<br/>

#### **6.2.1 `.indicatorPosition(IndicatorPosition)`**
This setting sets the Position where you wish to place Pollfish indicator  ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png) <br/> Pollfish indicator is shown only if Pollfish is used in a non rewarded mode.

There are six different options available:

* `.topLeft`
* `.middleLeft`
* `.bottomLeft`
* `.topRight`
* `.middleRight`
* `.bottomRight`

<br/>

If you do not set explicity a position for Pollfish indicator, it will appear by default at **`.topLeft`**

> **Note:** If you would like to skip the Pollfish Indicator please se the `rewardMode` to `true`

<br/>

Below you can see an example on how you can set Pollfish indicator to slide from the top right middle of the screen:

</br>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params indicatorPosition:IndicatorPositionMiddleRight];
```
<span style="text-decoration: underline">Swift:</span>
```swift
let params = PollfishParams("API_KEY")
    .indicatorPosition(.middleRight);
```

<br/>

`IndicatorPosition` param affects also from which side the survey panel will slide-in (Right or Left).

<br/>

#### **6.2.2 `.requestUUID(String)`**

Sets a unique id to identify a user and be passed through server-to-server callbacks. You can read more on how to retrieve this param through the callbacks <a href="https://www.pollfish.com/docs/s2s">here</a>.

<br/>

Below you can see an example on how you can pass a requestUUID during initialization:

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params requestUUID:@"USER_ID"];
```
<span style="text-decoration: underline">Swift:</span>
```swift
let pollfishParams = PollfishParams("API_KEY")
    .requestUUID="USER_ID";
```

<br/>

#### **6.2.3 `.indicatorPadding(Int)`**

Sets padding from the top or the bottom of the screen according to the Position of the Pollfish indicator. Below you can see an example on how to add padding of 50 from the bottom of the screen, prior rendering Pollfish indicator.

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params indicatorPadding:50];
[params indicatorPosition:IndicatorPositionBottomRight];
```
<span style="text-decoration: underline">Swift:</span>
```swift
let pollfishParams = PollfishParams("API_KEY")
    .indicatorPadding(50)
    .indicatorPosition(.bottomRight)
```

<br/>

> **Note:** If  the pollfish indicator is used in the middle position, padding is calculated from the top

<br/>

#### **6.2.4 `.pollfishViewContainer(UIView)`**

Sets a UIView container where Pollfish survey panel will be rendered. If this param is not set, the SDK will render Pollfish surveys on a new `UIViewController` on top of everything. 

Preferrably you should let the SDK handle the render on its own.

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params viewContainer:self.view];
```

<span style="text-decoration: underline">Swift:</span>
```swift
let pollfishParams = PollfishParams("API_KEY")
    .viewContainer(self.view)
```

For **SwiftUI** based projects, you have to define a struct comforming to  ```UIViewRepresentable``` protocol and expose a UIView field to Pollfish initialisation. The following example demonstrates how to create a custom ```View``` and handle rendering on it's on.

```swift
struct PollfishView: UIViewRepresentable {
    let view = UIView()

    func makeUIView(context: Context) -> UIView {
       view
    }

    func updateUIView(_ uiView: UIView, context: Context) {}
}
```
For instructions on how to initialize with a custom ```View``` see section 6.2

<br/>

#### **6.2.5 `.releaseMode(Bool)`**

Sets Pollfish SDK to Developer or Release mode. If you do not set this param it will turn the SDK to Developer mode by default in order for the developer to be able to test with test surveys.

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing - always returns a survey).  
*   **Release mode** is the mode to be used for a released app on the AppStore (start receiving paid surveys).  

<br/>

> **Note:** Be careful to set releaseMode parameter to true prior releasing to the AppStore!  

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params releaseMode:true];
```

<span style="text-decoration: underline">Swift:</span>
```swift
let pollfishParams = PollfishParams("API_KEY")
    .releaseMode(true)
```
<br/>

#### **6.2.6 `.rewardMode(Bool)`**

Initializes Pollfish in reward mode. This means that Pollfish Indicator will not be shown and Pollfish survey panel will be automatically hidden until the publisher explicitly calls Pollfish show function (The publisher should wait for the pollfish survey received callbacks). This behaviour enables the option for the publisher, to show a custom prompt to incentivize the user to participate to the survey.

> **Note:** If not set, the default value is false and Pollfish indicator is shown.

You can view an example on how to achieve this behaviour [here](https://github.com/pollfish/ios-sdk-pollfish)

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params rewardMode:true];
```

<span style="text-decoration: underline">Swift:</span>
```swift
let pollfishParams = PollfishParams("API_KEY")
    .rewardMode(true)
```

<br/>

You can read more on how you can use the rewardMode to incentivize users to participate to surveys in the following <a href="https://www.pollfish.com/docs/rewarded-surveys">link</a>.

<br/>

#### **6.2.7 `.offerwallMode(Bool)`**

Enables Pollfish in offerwall mode. If not specified Pollfish is shown as one survey at a time.

Below you can see an example on how you can intialize Pollfish in Offerwall mode:

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params offerwallMode:true];
```

<span style="text-decoration: underline">Swift:</span>
```swift
let pollfishParams = PollfishParams("API_KEY")
    .offerwallMode(true)
```

<br/>

#### **6.2.8 `.userProperties(UserProperties)`**

Passing user attributes to skip or shorten Pollfish Demographic surveys.

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and archieve better fill rate and higher priced surveys.

> **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default.

> **Note:** You can read more on demographic surveys and list of available options <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

An example of how you can create and pass a `UserProperties` object during initialization can be the following below:

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
UserProperties *userProperties = [[UserProperties alloc] init];

[userProperties gender:GenderMale];
[userProperties race:RaceWhite];
[userProperties yearOfBirth:1984];
[userProperties maritalStatus:MaritalStatusMarried];
[userProperties parental:ParentalThree];
[userProperties education:EducationUniversity];
[userProperties employment:EmploymentEmployedForWages];
[userProperties career:CareerTelecommunications];
[userProperties income:IncomeMiddleI];
[userProperties spokenLanguages:@[
    [NSNumber numberWithInt:SpokenLanguageGreek],
    [NSNumber numberWithInt:SpokenLanguageEnglish]
]];
[userProperties organizationRole:OrganizationRoleTechnicalStaff];
[userProperties numberOfEmployees:NumberOfEmployeesFiftyOneToHundrend];
[userProperties postalData:@"10017|US"];
[userProperties customAttribute:@"value" forKey:@"key"];

PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];
[params userProperties:userProperties];
```

<span style="text-decoration: underline">Swift:</span>
```swift
let userProperties = UserProperties([
    .gender(.male),
    .race(.white),
    .yearOfBirth(1984),
    .maritalStatus(.married),
    .parental(.three),
    .education(.university),
    .employment(.employedForWages),
    .career(.telecommunications),
    .income(.middleI),
    .spokenLanguages([
        .greek,
        .english
    ])
    .organizationRole(.technicalStaff)
    .numberOfEmployees(.fiftyOneToHundrend)
    .postalData("10017|US")
    .customProperty("key", "value")
])
    
let pollfishParams = PollfishParams("API_KEY")
    .userProperties(userProperties)
```

<br/>

#### **6.2.9 `rewardInfo(RewardInfo)`**

An object holding information regarding the reward settings, overriding the values as speciefied in the Publisher's Dashboard

<br/>

```swift
struct RewardInfo {
    let rewardName: String
    let rewardConversion: Float
}
```

Field | Description
------------ | -------------
**`rewardName`**      | Overrides the reward name as specified in the Publisher's Dashboard
**`rewardConversion`** | Overrides the reward conversion as specified in the Publisher's Dashboard. Conversion is expecting a number matching this function ( ```1 USD = X Points``` ) where ```X``` is a ```Float``` number.

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
RewardInfo *rewardInfo = [[RewardInfo alloc]
                          initWithRewardName:@"Diamonds"
                          rewardConversion:1.1];

PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];
[params rewardInfo:rewardInfo];
```

<span style="text-decoration: underline">Swift:</span>
```swift
let rewardInfo = RewardInfo(rewardName: "Diamonds",
                            rewardConversion: 1.1f)

let pollfishParams = PollfishParams("API_KEY")
    .rewardInfo(rewardInfo)
```

> **Note:** It's preferable to handle the reward settings through the Publisher's Dashboard

<br/>

#### **6.2.10 `clickId(String)`**

A pass through param that will be passed back through server-to-server callbacks as specified [here](https://www.pollfish.com/docs/s2s)

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params clickId:@"CLICK_ID"];
```

<span style="text-decoration: underline">Swift:</span>
```swift
et pollfishParams = PollfishParams("API_KEY")
    .clickId("CLICK_ID")
```

<br/>

#### **6.2.11 `signature(String)`**

An optional parameter used to secure the `rewardName` and `rewardConversion` parameters as passed through the `RewardInfo` object (5.2.10)

This parameter can be used optionally to prevent tampering around reward conversion, if passed during initialisation. The platform supports url validation by requiring a hash of the `rewardConversion`, `rewardName`, and `clickId`. Failure to pass validation will result in firing **`PollfishSurveyNotAvailable`** callback.

In order to generate the `signature` field you should sign the combination of `rewardConversion+rewardName+clickId` parameters using the HMAC-SHA1 algorithm and your account's secret_key that can be retrieved from the Account Information page on your Pollfish Dashboard.

The `signature` value should then be encoded using Base64.

> **Note:** Although `rewardConversion` is mandatory for the hashing to work, the `rewardName` and `clickId` parameters are optional and you should add them for extra security.

<br/>

<span style="text-decoration: underline">Objective-C:</span>
```objc
PollfishParams *params = [[PollfishParams alloc] init:@"API_KEY"];

[params signature:@"SIGNATURE"];
```

<span style="text-decoration: underline">Swift:</span>
```swift
et pollfishParams = PollfishParams("API_KEY")
    .signature("SIGNATURE")
```

---

<br/>

**At this point you are ready to go live! Turn your app to Release mode by setting `.releaseMode(true)` and submit your app to the AppStore.**

<br/>

### 7. Distributing your app to AppStore

Pollfish uses Advertising Identifier (IDFA) for survey distribution and therefore when submitting your app to the App you should select the following options as seen in the image below:  

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/idfa_3.png"/>

<br/>

### 8. Update your App's Privacy Policy in the app and on AppStore Connect

Add the following paragraph to your **App's Privacy Policy**:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Publishers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user's device data (including Advertising ID, Device ID, other available electronic identifiers and further response meta-data is automatically sent, via our app, to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully the Pollfish respondent terms located at [https://www.pollfish.com/terms/respondent](https://www.pollfish.com/terms/respondent). These data will be associated with your answers to the questionnaires whenever Pollfish sends such questionnaires to eligible users. Pollfish may share such data with third parties, clients and business partners, for commercial purposes. By downloading the application, you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by visiting the following link [https://www.pollfish.com/respondent/opt-out](https://www.pollfish.com/respondent/opt-out). We once more invite you to check the Pollfish respondent's terms of use, if you wish to have more detailed view of the way Pollfish works and with whom Pollfish may further share your data."*  

<br/>

and on the **App Store Connect** in the App's Privacy Policy section, update the relevant data collection questionnaire with the following choices as suggested by the latest AppStore's policies:

<br/>

<details><summary>Questionnaire Answers</summary>

| Type | Description | App Tracking | Explanation 
| --- | --- | --- | --- |
| **Contact Info** | --- | --- | --- |
| Name | Such as first or last name | NO |  |
| Email Address | Including but not limited to a hashed email address | NO |  |
| Phone Number | Including but not limited to a hashed phone number | NO |  |
| Physical Addrress | Such as home address, physical address, or mailing address | NO |  |
| Other User Contact Info | Any other information that can be used to contact the user outside the app | NO |  |
| **Health & Fitness** | --- | --- | --- |
| Health | Health and medical data, including but not limited to from the Clinical Health Records API, HealthKit API, MovementDisorderAPIs, or health-related human subject research or any other user provided health or medical data | <ul> <li> **Data use:** Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** No </li> </ul> | Pollfish does not directly collect any health data. However some clients might create surveys that could be asking some general health questions |
| Fitness | Fitness and exercise data, including but not limited to the Motion and Fitness API | <ul> <li> **Data use:** <br> Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** No </li> </ul> | Pollfish does not directly collect any fitness data. However some clients might create surveys that could be asking some general fitness questions |
| **Financial Info** | --- | --- | --- |
| Payment Info | Such as form of payment, payment card number, or bank account number | NO |  |
| Credit Info | Such as credit score | NO |  |
| Other Financial Info | Such as salary, income, assets, debts, or any other financial information | <ul> <li> **Data use:** Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** Yes </li> </ul> | Income data are collected as part of the demographic data during the onboarding process|
| **Location** | --- | --- | --- |
| Precise Location | Information that describes the location of a user or device with the same or greater resolution as a latitude and longitude with three or more decimal places | NO |  |
| Coarse Location | Information that describes the location of a user or device with lower resolution than a latitude and longitude with three or more decimal places, such as approximate location services | NO |  |
|  **Sensitive Info** | --- | --- | --- |
| Sensitive Info | Such as racial or ethnic data, sexual orientation, pregnancy or childbirth information, disability, religious or philosophical beliefs, trade union membership, political opinion, genetic information, or biometric data | <ul> <li> **Data use:** Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** Yes </li> </ul> | Demographic data such as the number of children or race are asked during the demographic data collection process when onboarding a user |
|  **Contacts** | --- | --- | --- |
| Contacts | Such as a list of contacts in the user’s phone, address book, or social graph | NO | |
|  **User Content** | --- | --- | --- |
| Emails or Text Messages | Including subject line, sender, recipients, and contents of the email or message | NO | |
| Photos or Videos | The user’s photos or videos | NO |  |
| Audio Data | The user’s voice or sound recordings | NO | |
| Gameplay Content | Such as user-generated content in-game | NO |  |
| Customer Support | Data generated by the user during a customer support request | NO |  |
| Other User Content | Any other user-generated content | <ul> <li> **Data use:** Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** Yes </li> </ul> | Different types of open ended questions might be asked within surveys |
|  **Browsing History** | --- | --- | --- |
| Browsing History | Information about the content the user has viewed | NO |  |
|  **Search History** | --- | --- | --- |
| Search History | Information about searches the user has performed | NO |  |
|  **Identifiers** | --- | --- | --- |
| User ID | Such as screen name, handle, account ID, assigned user ID, customer number, or other user- or account-level ID that can be used to identify a particular user or account | <ul> <li> **Data use:** Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** Yes </li> </ul> | Publishers can pass a unique user ID and receive it back in s2s callbacks |
| Device ID | Such as the device’s advertising identifier, or other device-level ID | <ul> <li> **Data use:** Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** Yes </li> </ul> | Pollfish SDK works upon the IDFA |
|  **Purchases** | --- | --- | --- |
| Purchase History | An account’s or individual’s purchases or purchase tendencies | NO | |
|  **Usage Data** | --- | --- | --- |
| Product Interaction | Such as app launches, taps, clicks, scrolling information, music listening data, video views, saved place in a game, video, or song, or other information about how the user interacts with the app | NO |  |
| Advertising Data | Such as information about the advertisements the user has seen | NO | Pollfish monitors the number of surveys a user has seen but not any advertisement  within or outside it's context |
| Other Usage Data | Any other data about user activity in the app | NO | |
|  **Diagnostics** | --- | --- | --- |
| Crash Data | Such as crash logs | NO | |
| Performance Data | Such as launch time, hang rate, or energy use | NO | |
| Other Diagnostic Data | Any other data collected for the purposes of measuring technical diagnostics related to the app | NO | |
|  **Other Data** | --- | --- | --- |
| Other Data Types | Any other data types not mentioned | <ul> <li> **Data use:** Third-Party Advertising </li> <li> **Linked to user:** Yes </li> <li> **Tracking:** Yes </li> </ul> | Different types of data can be collected through surveys |

</details>

<br/>

---

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>

<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look at our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>

<br/>

> **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process that users need to go through, in order to join the platform. If a paid survey is available at that point of time, the demographic questions will be preappended at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this type of targeting.

<br/>

<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>

<br/>


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents or by checking the survey class which will be `Pollfish\Demographics`. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. 

You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 6.2.8 - "Passing user properties to skip or shorten Pollfish Demographic surveys" and skip or shorten this way, Pollfish Demographic surveys.

<br/>

### 9. Request your account to get verified

After your app is published on the AppStore you should request your account to get verified from your Pollfish Publisher Dashboard.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/verify_account.png"/>

<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients. At that point, the live version of your app should have Pollfish SDK in release mode.

> **Note:** In order to be able to request your account to get verified you need to provide a url of your app on the AppStore

<br/>

## Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour like listening and acting on different  notifications. All the steps below are optional.
<br/>
<br/>

### 10. Manually show or hide Pollfish (optional)

You can manually hide or show Pollfish survey panel by calling anywhere after initialization:  

<span style="text-decoration: underline">Objective-C:</span>
```objc
[Pollfish show];
```

<span style="text-decoration: underline">Swift:</span>
```swift
Pollfish.show()
```

**or** 

<span style="text-decoration: underline">Objective-C:</span>
```objc
[Pollfish hide];
```

<span style="text-decoration: underline">Swift:</span>
```swift
Pollfish.hide()
```

<br/>

### 11. Listen for Pollfish lifecycle events (optional)

In order to get notified for Pollfish lifecycle events you will have to comform to the `PollfishDelegate` and override the methods of your choice. All methods are optional.

Below you can see an example of comformance to the `PollfishDelegate`

<span style="text-decoration: underline">Objective-C:</span>
```objc
// ViewController.h

@interface ViewController : UIViewController<PollfishDelegate>

@end


// ViewController.m

@interface ViewController()

@end

@implementation ViewController

...

// Override here the methods of your choice

@end
```

<span style="text-decoration: underline">Swift:</span>
```swift

class ViewController: UIViewController {
   ...
}

extension ViewController: PollfishDelegate {
    // Override here the methods of your choice
}
```

Please make sure you pass the conforming class durring initialisation

<span style="text-decoration: underline">Objective-C:</span>
```objc
[Pollfish initWith:params delegate:self];
```

<span style="text-decoration: underline">Swift:</span>
```swift
Pollfish.initWith(params, delegate: self)
```

There are seven methods available to override:

No | Delegate Method
------------ | -------------
11.1 | **`pollfishSurveyReceived(SurveyInfo?)`** <br/> Get notified when a survey is received
11.2 | **`pollfishSurveyCompleted(SurveyInfo)`** <br/> Get notified when a survey is completed
11.3 | **`pollfishUserNotEligible`** <br/> Get notified when a user is not eligible for a Pollfish survey
11.4 | **`pollfishSurveyNotAvailable`** <br/> Get notified when no survey is available
11.5 | **`pollfishOpened`** <br/> Get notified when Pollfish panel has opened
11.6 | **`pollfishClosed`** <br/> Get notified when Pollfish panel has closed
11.7 | **`pollfishUserRejectedSurvey`** <br/> Get notified when a user rejected a survey

<br/>

**`SurveyInfo`** 

This object contains information regarding the survey that has been received or completed by the user.

```swift
struct SurveyInfo {
    let cpa: Int?
    let loi: Int?
    let ir: Int?
    let surveyClass: String?
    let rewardName: String?
    let rewardValue: Int?
    let remainingCompletes: Int?
}
```

Field | Description
------------ | -------------
**`cpa`**                | Money to be earned from survey received in US dollar cents (estimated based on daily exchange currency)
**`ir`**                 | The current estimation for the survey incidence rate as an integer number in the range 0-100. This param is optional and will have as default the value -1 if it was not set and the IR was not computed reliably
**`loi`**                | The expected time in minutes that it takes to complete the survey. This param is optional and will have as default the value -1 if it was not set and the LOI wan not computed reliably
**`surveyClass`**        | Information about the survey network and type
**`rewardName`**         | A virtual reward name as specified on Publisher Dashboard 
**`rewardValue`**        | A virtual reward value as caluclated via a given echange rate on Publisher Dashboard 
**`remainingCompletes`** | The number of remaining completes for the survey

<br/>

The syntax for survey_class values is:

```
survey_class: provider["/"type]
provider: "Pollfish" | "Toluna" | "Cint" | "Lucid" | "InnovateMR" | "SaySo" | "Dynata"
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

<br/>

> **Note:** When a new mediation network enters the Pollfish network the appropriate values will be added.

<br/>

### 11.1 Get notified when a survey is received

You can be notified when a survey is received via the `PollfishDelegate`.

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) pollfishSurveyReceivedWithSurveyInfo:(SurveyInfo *)surveyInfo
{
    if (surveyInfo != nil) {
        NSLog(@"Pollfish Survey Received - %@", surveyInfo);
    } else {
        NSLog(@"Pollfish Survey Offerwall Received");
    }
}
```

<span style="text-decoration: underline">Swift:</span>
```swift
func pollfishSurveyReceived(surveyInfo: SurveyInfo?) {
    guard let surveyInfo = surveyInfo else { 
        print("Pollfish Survey Offerwall Received")
        return 
    }

    print("Pollfish Survey Received - \(surveyInfo)")
}
```

<br/>

As you may see in the example above you can get informed for the following values by overriding `pollfishSurveyReceived` method: 

> **Note:** When offerwall mode is enabled, it returns a `nil` object. It just notifies that surveys are available within the offerwall.

<br/>

### 11.2 Get notified when a survey is completed

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) pollfishSurveyCompletedWithSurveyInfo:(SurveyInfo *)surveyInfo
{
    NSLog(@"Pollfish Survey Completed - %@", surveyInfo);
}
```

<span style="text-decoration: underline">Swift:</span>
```swift
func pollfishSurveyCompleted(surveyInfo: SurveyInfo) {
    print("Pollfish Survey Completed - \(surveyInfo)")
}
```

<br/>

### 11.3 Get notified when a user is not eligible for a Pollfish survey


You can be notified when a user is not eligible for a Pollfish survey after accepting to take one, via the `PollfishDelegate`.  

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) pollfishUserNotEligible
{
    NSLog(@"Pollfish User Not Eligible!");
}
```

<span style="text-decoration: underline">Swift:</span>
```swift
func pollfishUserNotEligible() {
     print("Pollfish User Not Eligible!")
}
```

<br/>

### 11.4 Get notified when no surveys are available for that user

You can be notified when surveys are not available for that user via the `PollfishDelegate`.  

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) pollfishSurveyNotAvailable
{
    NSLog(@"Pollfish Survey Not Available!");
}
```

<span style="text-decoration: underline">Swift:</span>
```swift
func pollfishSurveyNotAvailable() {
     print("Pollfish Survey Not Available!")
}
```

<br/>

### 11.5 Get notified when Pollfish panel has opened

You can be notified when a user opens Pollfish survey panel via the `PollfishDelegate`.  

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) pollfishOpened
{
    NSLog(@"Pollfish has opened!");
}
```

<span style="text-decoration: underline">Swift:</span>
```swift
func pollfishOpened() {
     print("Pollfish has opened!")
}
```

<br/>

### 11.6 Get notified when Pollfish panel has closed

You can be notified when a user closes Pollfish survey panel via the `PollfishDelegate`.  

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) pollfishClosed
{
    NSLog(@"Pollfish has closed!");
} 
```

<span style="text-decoration: underline">Swift:</span>
```swift
func pollfishClosed() {
     print("Pollfish has closed!")
}
```

<br/>

### 11.7 Get notified when a user rejected a survey


You can be notified when a user rejected a survey via the `PollfishDelegate`.  

<span style="text-decoration: underline">Objective-C:</span>
```objc
- (void) pollfishUserRejectedSurvey
{
    NSLog(@"Pollfish User Rejected Survey");
}
```

<span style="text-decoration: underline">Swift:</span>
```swift
func pollfishUserRejectedSurvey() {
     print("Pollfish User Rejected Survey")
}
```

<br/>

### 12. Check if Pollfish survey is still available on your device (optional)

After you initialize Pollfish and a survey is received you can check at any time if the survey is available at the device.

<span style="text-decoration: underline">Objective-C:</span>
```objc
[Pollfish isPollfishPresent];
```

<span style="text-decoration: underline">Swift:</span>
```swift
Pollfish.isPollfishPresent()
```

### 13. Check if Pollfish survey panel is open (optional)

You can check at any time if the survey panel is visible.

<span style="text-decoration: underline">Objective-C:</span>
```objc
[Pollfish isPollfishPanelOpen];
```

<span style="text-decoration: underline">Swift:</span>
```swift
Pollfish.isPollfishPanelOpen()
```
