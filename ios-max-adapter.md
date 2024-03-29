<div class="changelog" data-version="6.4.2.0">
v6.4.2.0

- Updating with Pollfish iOS SDK v6.4.2

v6.4.1.0

- Updating with Pollfish iOS SDK v6.4.1

v6.4.0.0

- Updating with Pollfish iOS SDK v6.4.0

v6.3.1.1

- Adding the option to configure the Pollfish user id through the adapter

v6.3.1.0

- Updating with Pollfish iOS SDK v6.3.1

v6.3.0.0

- Updating with Pollfish iOS SDK v6.3.0

v6.2.7.0

- Updating with Pollfish iOS SDK v6.2.7

v6.2.5.1

- Fixing issue with missing armv7 architecture
- Changing lower deployment target to iOS 10

v6.2.5.0

- Updating with Pollfish SDK v6.2.5

v6.2.4.0

- Initial release

</div>

This guide is for publishers looking to use Max mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

<br/>

# Prerequisites

- [Pollfish Developer Account](https://www.pollfish.com/dashboard/dev/)
- [AppLovin Developer Account](https://dash.applovin.com/login)
- iOS 11.0 or later
- XCode 12

> **Note:** Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower.

</br>

# Quick Guide

- Set up Pollfish
- Set up AppLovin Rewarded Ads
- Add Pollfish Max Adapter to your project
- Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Pollfish surveys with AppLovin's Max mediation:

## 1. Set Up Pollfish

### 1.1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

<br/>

### 1.2. Add new app on Pollfish Publisher Dashboard and copy the given API Key

Login at [www.pollfish.com](www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Publisher Dashboard. Copy then the given API key for this app in order to use later on.

<br/>

## 2. Set up AppLovin Rewarded Ads

### 2.1. Create a new Network

First you need to sign in to your [AppLovin account](https://dash.applovin.com/login). Add Pollfish Network as a **Custom Network**. On the side menu navigate to Mediation -> Manage -> Networks

Scroll down to the bottom of the list and click on **Click here to add a Custom Network**

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_create_new_network.png"/>

<br/>

Next you will be prompted to create a **New Custom Network**

On the **Network Type** field select **SDK**. Set **Pollfish** as the value of **Custom Network Name** field. Set the **iOS Adapter Class Name** with the value **PollfishMediationAdapter**. Optionally, you can fill **Android/Fire OS Adapter Class Name** with **com.applovin.mediation.adapters.PollfishMediationAdapter**.

<br/>

### 2.2. Create a Rewarded Ad Unit

If you have not created a Rewarded Ad Unit in your app yet, navigate to Mediation -> Manage -> Ad Units and click **New Ad Unit**.

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_ad_unit_1.png"/>

<br/>

Give your Ad Unit a name and select the iOS option as the Platform. Start typing the name of your app, in the application name text field. If your app has already been publisher on the App Store you should be able to select it from the result list. If you haven't publisher your app yet, click on the **Manualy add your package name**. Fill your bundle ID as found in your project's General settings and click **Create**.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/max_ad_unit_2.png"/>

<br/>

Scroll down till you find the **Custom Networks & Deals** section and enable **Pollfish** newtork. 

<br/>

Paste the Pollfish Api Key as provided by the Pollfish Dashboard (step 1.2) into the Placement ID input field. 

<br/>

Optionally provide a JSON formatted string with your Pollfish confiiguration (alternatively you can pass those params in code as described in Step 6) using the `setLocalExtraParameterForKey` method of your `MARewardedAd` object instance. 

<br/>

> **Note:** In order for **PollfishMaxAdapter** to work, you need to provide the configuration at least one time. If you skip please make sure you provide this configuration during the **RewardedAd** request in code (Step 6). Configuration parameters in code will override Web UI parameters if provided in both places.

JSON configuration structure

Key | Type | Required
----| ---- | --------
**`api_key` (Deprecated)** <br/> Sets Pollfish SDK API key as provided by Pollfish | String | No (if placement id is set)
**`release_mode`** <br/> Sets Pollfish SDK to Developer or Release mode | Bool | Yes
**`request_uuid`** <br/> Sets a pass-through param to be received via the server-to-server callbacks | String | No

Example:

```json
{
    "api_key": "API_KEY", // This is deprecated, use the Placement ID instead
    "release_mode": true,
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

## 3. Add Pollfish Max Adapter to your project

### **Retrieve Pollfish Max Adapter through CocoaPods**

Add a Podfile with PollfishMaxAdapter pod reference:

```ruby
pod 'PollfishMaxAdapter'
```

You can find the latest PollfishMaxAdapter version on CocoaPods [here](https://cocoapods.org/pods/PollfishMaxAdapter)

Run pod install on the command line to install PollfishMax pod.

<br/>

### **Manually import PollfishMaxAdapter**

Download the following frameworks

* [Pollfish SDK](https://www.pollfish.com/docs/ios)
* [AppLovin SDK](https://dash.applovin.com/documentation/mediation/manual-integration-ios)
* [PollfishMaxAdapter](https://github.com/pollfish/ios-max-adapter)

and add them in your App's target dependecies 

1. Navigate to your project
2. Select your App's target and go to the **General** tab section **Frameworks, Libraries and Embedded Content**
3. Add all three dependent framewokrs one by one by pressing the + button -> Add other and selecting the appropriate framework

Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework
- SystemConfiguration.framework 
- WebKit.framework (added in Pollfish v4.4.0)

<br/>

## Important step Objective-C based projects

For Objective-C based projects you will need to create an empty Swift file including Foundation framework and a bridging header file named `YourProjectName-Bridging-Header.h`. Skipping this step will result to compilation failure.


You can see an example [here](https://github.com/pollfish/ios-max-adapter/tree/master/PollfishMaxAdapterExampleObjC)

<br/>

## 4. Request for a RewardedAd

<br/>

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

<br/>

Import `AppLovinSDK` 

<span style="text-decoration:underline">Swift</span>

```swift
import AppLovinSDK
```

<span style="text-decoration:underline">Objective C</span>

```objc
#import <AppLovinSDK/AppLovinSDK.h>
```

<br/>

Initialize the SDK in your app delegate’s `application:applicationDidFinishLaunching:` method

<span style="text-decoration:underline">Swift</span>

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        
    ALSdk.shared()!.mediationProvider = "max"
    
    ALSdk.shared()!.initializeSdk(completionHandler: nil)
    
    return true
}
```

<span style="text-decoration:underline">Objective C</span>

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [ALSdk shared].mediationProvider = @"max";
    
    [[ALSdk shared] initializeSdkWithCompletionHandler:^(ALSdkConfiguration *configuration) {}];
}
```

<br/>

Implement `MARewardedAdDelegate` so that you are notified when your ad is ready and of other ad-related events.

<br/>

Request IDFA Permission (Recommended but optional)

Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower.

To display the App Tracking Transparency authorization request for accessing the IDFA, update your `Info.plist` to add the `NSUserTrackingUsageDescription` key with a custom message describing your usage. Below is an example description text:

```xml
<key>NSUserTrackingUsageDescription</key>
<string>This identifier will be used to deliver personalized ads/surveys to you.</string>
```

To present the authorization request, call `requestTrackingAuthorization`. We recommend waiting for the completion callback prior to initializing.

<span style="text-decoration:underline">Swift</span>

```swift
#if canImport(AppTrackingTransparency)
import AppTrackingTransparency
#endif

...

override func viewDidAppear(_ animated: Bool) {
    if #available(iOS 14, *) {
        requestIDFAPermission()
    } else {
        createRewardedAd()
    }
}

@available(iOS 14, *)
func requestIDFAPermission() {
    #if canImport(AppTrackingTransparency)
    ATTrackingManager.requestTrackingAuthorization { status in
        DispatchQueue.main.async {
            self.createRewardedAd()
        }
    }
    #endif
}
```

<span style="text-decoration:underline">Objective C</span>

```objc
#if __has_include(<AppTrackingTransparency/AppTrackingTransparency.h>)
#import <AppTrackingTransparency/AppTrackingTransparency.h>
#endif

...

- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
    
    if (@available(iOS 14, *)) {
        [self requestIDFAPermission];
    } else {
        [self createRewardedAd];
    }
}

- (void)requestIDFAPermission {
#if __has_include(<AppTrackingTransparency/AppTrackingTransparency.h>)
    if (@available(iOS 14, *)) {
        [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
            dispatch_async(dispatch_get_main_queue(), ^{
                [self createRewardedAd];
            });
        }];
    } else {
        // Fallback on earlier versions
    }
#endif
}
```

<br/>

Request a RewardedAd from AppLovin by calling `load` in the `MARewardedAd` object instance you've created. By default Pollfish Max Adapter will use the configuration as provided on AppLovin's dashboard (step 2). If no configuration is provided or if you want to override any of those params please see step 6.

<br/>

<span style="text-decoration:underline">Swift</span>

```swift
class ViewController: UIViewController, MARewardedAdDelegate {

    var rewardedAd: MARewardedAd!

    ...

    func createRewardedAd() {
        rewardedAd = MARewardedAd.shared(withAdUnitIdentifier: "AD_UNIT_ID")
        rewardedAd.delegate = self
        rewardedAd.load()
    }

    func didLoad(_ ad: MAAd) {}

    func didDisplay(_ ad: MAAd) {}

    func didHide(_ ad: MAAd) {}

    func didClick(_ ad: MAAd) {}

    func didFailToLoadAd(forAdUnitIdentifier adUnitIdentifier: String, withError error: MAError) {}

    func didFail(toDisplay ad: MAAd, withError error: MAError) {}

    func didStartRewardedVideo(for ad: MAAd) {}

    func didCompleteRewardedVideo(for ad: MAAd) {}

    func didRewardUser(for ad: MAAd, with reward: MAReward) {}

}
```

<span style="text-decoration:underline">Objective C</span>

```objc
@interface ViewController()<MARewardedAdDelegate>
@property (nonatomic, strong) MARewardedAd *rewardedAd;
@end

@implementation ViewController

...

- (void)createRewardedAd
{
    self.rewardedAd = [MARewardedAd sharedWithAdUnitIdentifier: @"YOUR_AD_UNIT_ID"];
    self.rewardedAd.delegate = self;
    [self.rewardedAd loadAd];
}

#pragma mark - MAAdDelegate Protocol

- (void)didLoadAd:(MAAd *)ad {}

- (void)didFailToLoadAdForAdUnitIdentifier:(NSString *)adUnitIdentifier withError:(MAError *)error {}

- (void)didDisplayAd:(MAAd *)ad {}

- (void)didClickAd:(MAAd *)ad {}

- (void)didHideAd:(MAAd *)ad {}

- (void)didFailToDisplayAd:(MAAd *)ad withError:(MAError *)error {}

#pragma mark - MARewardedAdDelegate Protocol

- (void)didStartRewardedVideoForAd:(MAAd *)ad {}

- (void)didCompleteRewardedVideoForAd:(MAAd *)ad {}

- (void)didRewardUserForAd:(MAAd *)ad withReward:(MAReward *)reward {}

@end
```

When the Rewarded Ad is ready, present the ad by invoking `rewardedAd.show()`. Just to be sure, you can combine show with a check to see if the Ad you are about to show is actualy ready.

<span style="text-decoration:underline">Swift</span>

```swift
if rewardedAd.isReady {
    rewardedAd.show()
}
```

<span style="text-decoration:underline">Objective C</span>

```objc
if ( [self.rewardedAd isReady] )
{
    [self.rewardedAd showAd];
}
```

<br/>

## 5. Publish your app on the store

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option. You can read more [here](https://www.pollfish.com/docs/demographic-surveys)

<br/>

# Optional section

## 6. Use and control Pollfish Max Adapter in your Rewarded Ad Unit

Pollfish Max Adapter provides different options that you can use to control the behaviour of Pollfish SDK. This configuration, if applied, will override any configuration done in AppLovin's dashboard.

<br/>

| No  | Description                                                                                                                  |
| --- | -----------------------------------------------------------------------------------------------------------------------------|
| 6.1 | **`api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish                                                        |
| 6.2 | **`request_uuid`** <br/> Sets a pass-through param to be received via the [s2s callbacks](https://www.pollfish.com/docs/s2s) |
| 6.3 | **`release_mode`** <br/> Toggles Pollfish SDK Developer or Release mode                                                      |
| 6.4 | **`user_id`** <br/> Sets a unique identifier to identify a user                                                              |

<br/>

### 6.1 `api_key`

Pollfish API Key as provided by Pollfish on [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign in and create an app. If you have already specified Pollfish API Key on AppLovin's UI, this param will override the one defined on Web UI.

<br/>

### 6.2 `request_uuid`

Sets a pass-through param to be received via the server-to-server callbacks.

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard. On each survey completion you will receive a callback to your server including the `request_uuid` param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

<br/>

### 6.3 `release_mode`

Sets Pollfish SDK to Developer or Release mode.

- **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
- **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish Max Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

<br/>

### 6.4 `user_id`

An optional id used to identify a user

Setting the `userId` will override the default behaviour and use that instead of the Advertising Id in order to identify a user

<span style="color: red">You can pass the id of a user as identified on your system. Pollfish will use this id to identify the user across sessions instead of an ad id/idfa as advised by the stores. You are solely responsible for aligning with store regulations by providing this id and getting relevant consent by the user when necessary. Pollfish takes no responsibility for the usage of this id. In any request from your users on resetting/deleting this id and/or profile created, you should be solely liable for those requests.</span>

<br/>

Below you can see all the available configuration options for Pollfish Max Adapter.

<br/>

```swift
rewardedAd = MARewardedAd.shared(withAdUnitIdentifier: "AD_UNIT_ID")
rewardedAd.setLocalExtraParameterForKey("api_key", value: "YOUR_API_KEY")
rewardedAd.setLocalExtraParameterForKey("request_uuid", value: "REQUEST_UUID")
rewardedAd.setLocalExtraParameterForKey("release_mode", value: true)
rewardedAd.setLocalExtraParameterForKey("user_id", value: "USER_ID")
```

<br/>

## 7. Payouts on Screenouts

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described [here](https://www.pollfish.com/docs/pay-on-screenouts).

<br/>

# More info

You can read more info on how the Pollfish SDKs work or how to get started with AppLovin's Max at the following links:

[Pollfish iOS SDK](https://pollfish.com/docs/ios)

[AppLovin Max iOS SDK](https://dash.applovin.com/documentation/mediation/ios/getting-started/integration)
