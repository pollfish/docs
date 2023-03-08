<div class="changelog" data-version="6.4.0.0">
v6.4.0.0

- Updating with Pollfish iOS SDK v6.4.0

v6.3.1.1

- Internal fixes

v6.3.1.0

- Updating with Pollfish iOS SDK v6.3.1

v6.3.0.0

- Updating with Pollfish iOS SDK v6.3.0

v6.2.7.0

- Updating with Pollfish iOS SDK v6.2.7

v6.2.5.0

- Updating with Pollfish iOS SDK v6.2.5

v6.2.4.0

- Updating with Pollfish iOS SDK v6.2.4

v6.2.3.0

- Updating with Pollfish iOS SDK v6.2.3

v6.2.2.0

- Updating with Pollfish iOS SDK v6.2.2

v6.2.1.0

- Updating with Pollfish iOS SDK v6.2.1

v6.2.0.0

- Updating with Pollfish iOS SDK v6.2.0

v6.1.0.0

- Updating with Pollfish iOS SDK v6.1.0

v6.0.3.0

- Updating with Pollfish iOS SDK v6.0.3

v6.0.2.0

- Updating with Pollfish iOS SDK v6.0.2

v6.0.1.0
    
- Updating with Pollfish iOS SDK 6.0.1
    
v6.0.0.0
    
- Updating with Pollfish iOS SDK 6.0.0
- Updating with Google-Mobile-SDK v8.3.0
    
v.5.5.2.0

- Updating with Pollfish iOS SDK 5.5.2

v.5.5.1.0

- Updating with Pollfish iOS SDK 5.5.1

v.5.5.0.0

- Changing packaging to .xcframework
- Adding support for arm64 devices
    
v.5.4.1.1

- Updating with Pollfish iOS SDK 5.4.1

v.5.3.1.1

- Updating with Pollfish iOS SDK 5.3.1

v.5.2.5.2

- Updating User Not Eligible listener behaviour

v.5.2.5.1

- Updating with Pollfish iOS SDK 5.2.5

v.5.2.4.1

- Updating with Pollfish iOS SDK 5.2.4

v.5.2.3.1

- Updating with Pollfish iOS SDK 5.2.3
- Updating User Rejection listener behaviour

v.5.2.2.1

- Updating with Pollfish iOS SDK 5.2.2

v.5.2.1.1

- Updating with Pollfish iOS SDK 5.2.1

v.5.1.0.2

- Initial release

</div>

This guide is for publishers looking to use AdMob mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

# Prerequisites

* [Pollfish Developer Account](https://www.pollfish.com/dashboard/dev/)
* [AdMob Account](https://apps.admob.com/)
* iOS 11.0 or later

<br/>


> **Note:** Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower. Offerwall integrations perform better compared to single survey integrations when no IDFA permission is given

</br>

# Quick Guide

* Set up AdMob Rewarded Ads
* Set up Pollfish
* Add Pollfish AdMob Adapter to your project
* Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Pollfish surveys with AdMob mediation:

## 1. Set up AdMob Rewarded Ads

### 1.1. Create a Rewarded Ad Unit

If you have not implemented [Rewarded Ads](https://developers.google.com/admob/ios/rewarded-ads) in your app yet, you can follow the documentation Implement as described by AdMob. 

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

First you need to sign in to your [AdMob account](https://apps.admob.com/). In your app you can click on **Ad Units** and then **ADD AD UNITS** and select **Rewarded** Ads

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/ad_unit_ios.png"/>
<br/>


In the configuration of the Ad Unit popup you can specify a name for your rewarded placement and then a name for the reward and a value. If you want to apply the same reward to the user no matter which ad network is served, check the **Apply to all networks in Mediation Groups** box.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/rewarded_ad_unit_ios.png"/>

<br/>

If you don't apply this setting, the Pollfish adapter will provide a dynamic value as you specified it on your Pollfish Dashboard, in the App Settings area, based on the actual price of each survey completed.


### 1.2. Configure Mediation Settings for your AdMob Rewarded Ad unit

You need to add Pollfish to the mediation configuration for your Rewarded Ad unit. 

Log in to your AdMob account. On the left side menu, click on the **Mediation** and then in **Mediation Groups** Tab. If you already have an existing Mediation Group you will need to modify it (click on the name of the Mediation Group and press **Edit**).

if you do not have a Mediation Group yet, click to create one with **CREATE MEDIATION GROUP**.

In the Ad Format drop down menu select **Rewarded** and for platform **iOS**

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/created_ios.png"/>

<br/>

and then you can name the Mediation Group if you do not have one already. Next, set the mediation group status to **Enabled**

Afterwards you should click **ADD AD UNITS** and associate the Mediation group with an existing AdMob Rewarded Ad unit.

You should now see the ad units card populated with the ad units you selected, as shown below:

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/ad_units_ios.png"/>

<br/>

You then have to add Pollfish Network to the Mediationn Waterfall of the group. Click on **ADD CUSTOM EVENT**

You can add a name to differentiate Pollfish Network from your other ad sources (for example Pollfish Netowrk) and an estimated eCPM. Pollfish surveys average eCPMs, range betweenn $70-$80.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/custom_event_aa.png"/>

<br/>

You can then configure Pollfish ad unit by adding the class name of Pollfish AdMob Mediation Adapter

**Class Name:** GADMediationAdapterPollfish<br/>
**Parameter:** JSON with Pollfish SDK configuration prams (optional)

Users can pass a **JSON string** to provide the necessary params for Pollfish SDK to work (similarly they can pass those params as described in Step 5. 

Key | Type
------------ | -------------
**`api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish | String
**`release_mode`** <br/> Sets Pollfish SDK to Developer or Release mode | Boolean
**`request_uuid`** <br/> Sets a pass-through param to be received via the server-to-server callbacks | String
**`offerwall_mode`** <br/> Sets Pollfish SDK to Offerwall Mode | Boolean

Example:

```json
{
    "api_key": "Pollfish API Key", 
    "release_mode": true,
    "request_uuid": "My user id",
    "offerwall_mode": false
}
```

> **Note:** Pollfish SDK works by default in production mode. If you would like to test with test surveys you should use release_mode false or explicitly request that in code as described in Step 5.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/pollfish_ios_mediation.png"/>

<br/>

## 2. Set Up Pollfish

### 2.1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

<br/>

### 2.2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

<br/>

### 2.3. Add Pollfish framework to your project

**Manual integration**

[Download Pollfish iOS SDK](https://storage.googleapis.com/pollfish_production/sdk/iOS/Pollfish%20iOS%20SDK%206.2.5.zip)

In Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.  

The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane).  

**Note: The framework is a folder and you should add the whole folder into your project.**

Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework
- SystemConfiguration.framework 
- WebKit.framework (added in Pollfish v4.4.0)

**Note: If your deployment target is lower than iOS 7.0, change the AdSupport.framework from Required to Optional.**

<br/>

**CocoaPoda integration**

Add a Podfile with Pollfish framework as a pod reference:

```ruby
pod 'Pollfish'
```

You can find latest Pollfish iOS SDK version on CocoaPods [here](https://cocoapods.org/pods/Pollfish)  

Run **pod install** on the command line to install  Pollfish cocoapod.

<br/>

## 3. Add Pollfish AdMob Adapter to your project

### **Manual integration**

Download Pollfish iOS AdMob Adapter framework and then in Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.

<br>

### **CocoaPods**

Add a Podfile with Pollfish framework as a pod reference:

```ruby
pod 'PollfishAdMobAdapter'
```

You can find latest Pollfish iOS SDK version on CocoaPods here

Run pod install on the command line to install Pollfish cocoapod.

<br>

### **Swift Package Manager**

The Pollfish AdMob Adapter supports Swift Package Manager starting in version 6.3.0.0. Follow the steps below to import the Swift package.

> **Note:** Note: If migrating from a CocoaPods-based project, run pod deintegrate to remove CocoaPods from your Xcode project. The CocoaPods-generated .xcworkspace file can safely be deleted afterward. If you're adding the Pollfish AdMob Adapter to a project for the first time, this step can be ignored.

<br>

In Xcode, install the Pollfish AdMob Adapter Swift Package by navigating to File > Add Packages....

In the prompt that appears, search for the Pollfish AdMob Adapter Swift Package GitHub repository:

```
https://github.com/pollfish/ios-admob-adapter.git
```

Select the version of the Pollfish AdMob Adapter you want to use. For new projects, we recommend using the Up to Next Major Version.

Once you're finished, Xcode will begin resolving your package dependencies and downloading them in the background. For more details on how to add package dependencies, see [Apple's article](https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app).

<br/>

## 4. Request for a RewardedAd

Import `GoogleMobileAds`

<span style="text-decoration:underline">Swift</span>

```swift
import GoogleMobileAds
```

<span style="text-decoration:underline">Objective C</span>

```objc
@import GoogleMobileAds;
```

<br/>

Initialize the SDK in your app delegate’s `application:applicationDidFinishLaunching:` method

<span style="text-decoration:underline">Swift</span>

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

    GADMobileAds.sharedInstance().start()
    
    return true
}
```

<span style="text-decoration:underline">Objective C</span>

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [[GADMobileAds sharedInstance] startWithCompletionHandler:nil];
    return YES;
}
```

<br/>

Implement `GoogleMobileAds` so that you are notified when your ad is ready and of other ad-related events.

<br/>

Request IDFA Permission (Recommended but optional)

Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower. Offerwall integrations perform better compared to single survey integrations when no IDFA permission is given.

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

Request a GADRewardedAd from AdMob by calling `load` in the `GADRewardedAd` object passing a `GADRequest` instance and your `AD_UNIT_ID` id. By default Pollfish AdMob Adapter will use the configuration as provided on AdMob's dashboard. If no configuration is provided or if you want to override any of those params please see step 3.

<br/>

<span style="text-decoration:underline">Swift</span>

```swift
class ViewController: UIViewController, GADFullScreenContentDelegate {

    var rewardedAd: GADRewardedAd?

    ...

    func createRewardedAd() {
        let request = GADRequest()

        GADRewardedAd.load(withAdUnitID: "AD_UNIT_ID",
                           request: request) { (ad, error) in

            guard let error = error else {
                print("Failed to load ad with error: \(error!.localizedDescription)")
                return
            }
            
            self.rewardedAd = ad
            self.rewardedAd?.fullScreenContentDelegate = self
        }
    }

    func adDidDismissFullScreenContent(_ ad: GADFullScreenPresentingAd) {}
    
    func ad(_ ad: GADFullScreenPresentingAd, didFailToPresentFullScreenContentWithError error: Error) {}
    
    func adDidPresentFullScreenContent(_ ad: GADFullScreenPresentingAd) {}

}
```

<span style="text-decoration:underline">Objective C</span>

```objc
@interface ViewController()<GADFullScreenContentDelegate>
@property(nonatomic, strong) GADRewardedAd *rewardedAd;
@end

@implementation ViewController

...

- (void)createRewardedAd
{
    GADRequest *request = [GADRequest request];

    [GADRewardedAd loadWithAdUnitID:@"AD_UNIT_ID" request:request completionHandler:^(GADRewardedAd *ad, NSError *error) {
        if (error) {
            NSLog(@"Failed to load interstitial ad with error: %@", [error localizedDescription]);
            return;
        }
        
        self.rewardedAd = ad;
        self.rewardedAd.fullScreenContentDelegate = self;
    }];
}

#pragma mark - GADFullScreenContentDelegate Protocol

- (void)adDidPresentFullScreenContent:(id)ad {}

- (void)ad:(id)ad didFailToPresentFullScreenContentWithError:(NSError *)error {}

- (void)adDidDismissFullScreenContent:(id)ad {}

@end
```

When the Rewarded Ad is ready, present the ad by invoking `rewardedAd.present` which accepts a `ViewController` and a reward completion block. Just to be sure, you can combine present with a nullity check to see if the Ad you are about to show is actualy ready.

<span style="text-decoration:underline">Swift</span>

```swift
if (rewardedAd != nil) {
    rewardedAd?.present(fromRootViewController: self) {
        let reward = self.rewardedAd!.adReward
        print("Reward received with currency \(reward.type), amount \(reward.amount)")
    }
} 
```

<span style="text-decoration:underline">Objective C</span>

```objc
if (self.rewardedAd) {
    [self.rewardedAd presentFromRootViewController:self userDidEarnRewardHandler:^(void) {
        GADAdReward *reward = self.rewardedAd.adReward;
        NSString *rewardMessage = [NSString stringWithFormat:@"Reward received with currency %@, amount %lf", reward.type, [reward.amount doubleValue]];
        NSLog(@"%@", rewardMessage);
    }];
} 
```

<br/>

## 5. Publish your app on the store

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option.

<br/>

# Optional section

## 6. Configure programmatically Pollfish SDK behaviour

Pollfish AdMob Adapter provides different options that you can use to control the behaviour of Pollfish SDK. This configuration, if applied, will override any configuration done in AdMob's dashboard.

<br/>

Below you can see all the available options of **GADPollfishRewardedNetworkExtras** instance that is used to configure the behaviour of Pollfish SDK.

<br/>

No | Description | Type
------------ | ------------- | ----
6.1 | **`.pollfishAPIKey`**  <br/> Sets Pollfish SDK API key as provided by Pollfish | String
6.2 | **`.requestUUID`**  <br/> Sets a pass-through param to be received via the server-to-server callbacks | String
6.3 | **`.releaseMode`**  <br/> Sets Pollfish SDK to Developer or Release mode | Boolean
6.4 | **`.offerwallMode`** <br/> Sets Pollfish SDK to Offerwall Mode | Boolean


### 6.1 `.pollfishAPIKey`

Pollfish API Key as provided by Pollfish on  [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign up to the platform.  If you have already specified Pollfish API Key on AdMob's UI, this param will be ignored.

### 6.2 `.requestUUID`

Sets a pass-through param to be received via the server-to-server callbacks

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

### 6.3 `.releaseMode`

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

Pollfish AdMob Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

### 6.4 `.offerwallMode`

Enables offerwall mode. If not set, one single survey is shown each time.

Below you can see an example on how you can use `GADPollfishRewardedNetworkExtras` to pass info to Pollfish AdMob Adapter:

<span style="text-decoration:underline">Swift</span>

```swift
import PollfishAdMobAdapter

...

let request = GADRequest()
        
let pollfishNetworkExtras = GADPollfishRewardedNetworkExtras()
pollfishNetworkExtras.pollfishAPIKey = "POLLFISH_API_KEY"
pollfishNetworkExtras.releaseMode = false
pollfishNetworkExtras.requestUUID = "USER_ID"
pollfishNetworkExtras.offerwallMode = false

request.register(pollfishNetworkExtras)
```

<span style="text-decoration:underline">Objective C</span>

```objc
#import <PollfishAdMobAdapter/GADPollfishRewardedNetworkExtras.h>

...

GADRequest *request = [GADRequest request];
    
GADPollfishRewardedNetworkExtras *pollfishNetworkExtras = [[GADPollfishRewardedNetworkExtras alloc] init];
    
pollfishNetworkExtras.pollfishAPIKey = @"POLLFISH_API_KEY";
pollfishNetworkExtras.releaseMode = false;
pollfishNetworkExtras.requestUUID = @"YOUR_USER_ID";
pollfishNetworkExtras.offerwallMode = false;
    
[request registerAdNetworkExtras:pollfishNetworkExtras];
```

<br/>

## 7. Payouts on Screenouts

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described [here](https://www.pollfish.com/docs/pay-on-screenouts).

<br/>

# More info

You can read more info on how the Pollfish SDKs work or how to get started with Google AdMob at the following links:

[Pollfish iOS SDK](https://pollfish.com/docs/ios)

[AdMob iOS SDK](https://developers.google.com/admob/ios/quick-start)
