<div class="changelog" data-version="6.0.1.0">
v6.0.1.0

- Updated with Pollfish iOS SDK v6.0.1

v6.0.0.0

- Updated with Pollfish iOS SDK v6.0.0.0

v5.5.2.0

- New PollfishMoPubAdapter

</div>

This guide is for publishers looking to use MoPub mediation to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

## Prerequisites

* iOS 10.0 or later
* [Pollfish Publisher Account](https://www.pollfish.com/dashboard/dev/)
* [MoPub Developer Account](https://app.mopub.com/login)
* [Pollfish SDK](https://www.pollfish.com/docs/ios)
* [MoPub SDK](https://github.com/mopub/mopub-ios-sdk#manual-integration-with-dynamic-framework)

> **Note:** Pollfish iOS SDK utilizes Apple's Advertising ID (IDFA) to identify and retarget users with Pollfish surveys. As of iOS 14 you should initialize Pollfish iOS MoPub Adapter only if the relevant IDFA permission was granted by the user

</br>

Below you can find a step by step guide on how to incorporate Pollfish surveys with MoPub mediation:

## Step 1: Add MoPub Rewarded Ads in your app 

If you have not implemented [Rewarded Ads](https://developers.mopub.com/publishers/ios/rewarded-ad/) in your app yet, you can follow the documentation implementation as described by MoPub. 

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

## Step 2: Configure Ad Sources for your Rewarded Ad unit

You need to add Pollfish Network as a **Custom Native Network**
line item and link it with your Rewarded Ad unit. 

Log in to your MoPub account. On the top, click on the **Orders** tab and then select **Create Order**. If you already have an existing **Order** item you will need to modify it by clicking on it.

In the **Create Order** form, fill the required fields and press **Save & Create line item**

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-new-order.png"/>

<br/>

Next you will be prompted to create a **New Line Item**

Please make sure the correct order item is selected. Then set **Pollfish Network** as the line item name and **Network line item** as the Line item type.

On the **Network** field select **Custom SDK Network**. Set **PollfishMoPubAdapter** in the **Custom event class** field and optionally provide a JSON formatted text with your Pollfish confiiguration (alternatively you can pass those params in code as described in Step 6) in the **Custom event data** field. 

> **Note:** In order for **PollfishMoPubAdapter** to work, you need to provide the configuration at least one time. If you skip please make sure you provide this configuration during the **RewardedAd** request in code (Step 6). Configuration parameters in code will override Web UI parameters if provided in both places.

Field | Value 
--- | ---
**Custom event class** | PollfishMoPubAdapter<br/>
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

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-new-line-item-1.png"/>

<br/>

Next head to the **Budget & Schedule** section and fill the **Rate** field with a value ranging between $70-$80 since Pollfish rewarded surveys eCPMs usually fluctuates in that range.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-new-line-item-1-budget.png"/>

<br/>

Click next to proceed on the next step where you will select the Ad Unit on which this line item will apply. Please select iOS only Ad Units.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-new-line-item-2.png"/>

<br/>

Click next to proceed on the next step where you will select the audience targeting of this Netwrok line item. Fill those fields as you wish or proceed with the default values.

<br/>

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mopub-new-line-item-3.png"/>

<br/>

<br/>

## Step 3: Set Up Pollfish

## 3.1. Obtain a Publisher Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

### 3.2. Add new app on Pollfish Publisher Dashboard and copy the given API Key

Login at [www.pollfish.com](www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Publisher Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

## Step 4: Add PollfishMoPubAdapter to your project

### **Manually import PollfishMoPubAdapter**

Download the following frameworks

* [Pollfish SDK](https://www.pollfish.com/docs/ios)
* [MoPub SDK](https://github.com/mopub/mopub-ios-sdk#manual-integration-with-dynamic-framework)
* [PollfishMoPubAdapter](https://github.com/pollfish/ios-mopub-adapter)

and add them in your App's target dependecies 

1. Navigate to your project
2. Select your App's target and go to the **General** tab section **Frameworks, Libraries and Embedded Content**
3. Add all three dependent framewokrs one by one by pressing the + button -> Add other and selecting the appropriate framework

Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework
- SystemConfiguration.framework 
- WebKit.framework (added in Pollfish v4.4.0)

**OR**

### **Retrieve Pollfish MoPub Adapter through CocoaPods**

Add a Podfile with PollfishMoPubAdapter pod reference:

```ruby
pod 'PollfishMoPubAdapter'
```

You can find the latest PollfishMoPubAdapter version on CocoaPods [here](https://cocoapods.org/pods/PollfishMoPubAdapter)

Run pod install on the command line to install PollfishMoPub pod.

<br/>

## Important step Objective-C based projects

For Objective-C based projects you will need to create an empty Swift file including Foundation framework and a bridging header file named `YourProjectName-Bridging-Header.h`. Skipping this step will result to compilation failure.

<!-- Add link to objc example project -->
You can see an example [here]()

<br/>

## Step 5: Request for a RewardedAd

Import `PollfishMoPubAdapter` and `MoPubSDK`

<span style="text-decoration:underline">Swift</span>

```swift
import PollfishMoPubAdapter
import MoPubSDK
```

<span style="text-decoration:underline">Objective C</span>

```objc
@import PollfishMoPubAdapter;
#import <MoPubSDK/MoPub.h>
```

Initialize MoPub SDK and pass `PollfishAdapterConfiguration` during the initialisation configuration.

<span style="text-decoration:underline">Swift</span>

```swift
let config = MPMoPubConfiguration(adUnitIdForAppInitialization: "AD_UNIT_ID")

config.additionalNetworks = [PollfishAdapterConfiguration.self]

MoPub.sharedInstance().initializeSdk(with: config) {
    // Load Ad
}
```

<span style="text-decoration:underline">Objective C</span>

```objc
MPMoPubConfiguration *config = [[MPMoPubConfiguration alloc] 
    initWithAdUnitIdForAppInitialization:@"AD_UNIT_ID"];
[config setAdditionalNetworks:@[PollfishAdapterConfiguration.class]];

[[MoPub sharedInstance] initializeSdkWithConfiguration: config 
                        completion:^(void) {
    // Load Ad
}];
```

> **Note:** For iOS 14+ targeting please request for IDFA usage permission using the AppTrackingTransparency framework prior MoPub initialisation. See example [here](https://github.com/pollfish/ios-mopub-adapter)

<br/>

Request a RewardedAd from MoPub using the Pollfish configuration params that you provided on MoPub's Web UI (step 2). If no configuration is provided or if you want to override any of those params provided in the Web UI please see step 6.

<span style="text-decoration:underline">Swift</span>

```swift
MPRewardedAds.setDelegate(self, forAdUnitId: "AD_UNIT_ID")
        
MPRewardedAds.loadRewardedAd(withAdUnitID: "AD_UNIT_ID", 
                             withMediationSettings: nil)
```

<span style="text-decoration:underline">Objective C</span>

```objc
[MPRewardedAds setDelegate:self forAdUnitId:@"AD_UNIT_ID"];
    
[MPRewardedAds loadRewardedAdWithAdUnitID:@"AD_UNIT_ID" withMediationSettings:@[]];
```

Comform to `MPRewardedAdsDelegate` to get notified when the rewarded ad is ready to be shown

<span style="text-decoration:underline">Swift</span>

```swift
extension ViewController: MPRewardedAdsDelegate {
    
    func rewardedAdDidLoad(forAdUnitID adUnitID: String!) {}
    
    func rewardedAdDidFailToLoad(forAdUnitID adUnitID: String!, error: Error!) {}
    
}
```

<span style="text-decoration:underline">Objective C</span>

```objc
// ViewController.h

@interface ViewController : UIViewController<MPRewardedAdsDelegate>

...

@end

// ViewController.m
@implementation ViewController

...

- (void) rewardedAdDidLoadForAdUnitID:(NSString *)adUnitID {}

- (void) rewardedAdDidFailToLoadForAdUnitID:(NSString *)adUnitID error:(NSError *)error {}

@end
```

When the Rewarded Ad is ready to present the ad by invoking `presentRewardedAd`

<span style="text-decoration:underline">Swift</span>

```swift
MPRewardedAds.presentRewardedAd(forAdUnitID: unitId,
                                from: self,
                                with: nil)
```

<span style="text-decoration:underline">Objective C</span>

```objc
[MPRewardedAds presentRewardedAdForAdUnitID:@"AD_UNIT_ID" 
               fromViewController:self 
               withReward:NULL];
```

<br/>

## Step 6: Create Pollfish Params configuration Dictionary (Optional)

Pollfish MoPub Adapter provides different options that you can use to control the behaviour of Pollfish SDK overriding those set on the Web UI.

Below you can see all the key-value available options of that you can use to configure the behaviour of Pollfish SDK.

No | Description
------------ | -------------
6.1 | **`api_key: String`** <br/> Sets Pollfish SDK API key as provided by Pollfish
6.2 | **`request_uuid: Bool`** <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks
6.3 | **`release_mode: Bool`** <br/> Sets Pollfish SDK to Developer or Release mode
6.4 | **`offerwall_mode: Bool`** <br/> Sets Pollfish SDK to Oferwall Mode  

<br/>

#### **6.1 `api_key`**

Pollfish API Key as provided by Pollfish on [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign up to the platform.  If you have already specified Pollfish API Key on MoPub's Web UI, this param will be ignored.

#### **6.2 `request_uuid`**

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

#### **6.3 `release_mode`**

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

> **Note:** Pollfish MoPub Adapter runs Pollfish SDK in release mode by default. If you would like to test with Test survey, you should set release mode to fasle.

### **6.4 `offerwall_mode`**

Enables offerwall mode. If not set, one single survey is shown each time.

<br>

Below you can see an example on how you can pass info to Pollfish MoPub Adapter connfiguration:

```swift
let localExtras: [AnyHashable: Any] = [
    "api_key": "API_KEY",
    "release_mode": true,
    "offerwall_mode": true,
    "request_uuid": "USER_ID"]

MPRewardedAds.loadRewardedAd(
    withAdUnitID: "UNIT_ID",
    keywords: nil,
    userDataKeywords: nil,
    customerId: nil,
    mediationSettings: nil,
    localExtras: localExtras)
```

```objc
NSDictionary *localExtras = @{
    @"api_key": @"API_KEY",
    @"offerwall_mode": @true,
    @"release_mode": @true,
    @"request_uuid": @"USER_ID"};

[MPRewardedAds loadRewardedAdWithAdUnitID:adUnitid 
               keywords:NULL 
               userDataKeywords:NULL 
               customerId:NULL 
               mediationSettings:NULL 
               localExtras:localExtras];
```

## Step 7: Publish your app on the store

If you everything worked fine during the previous steps, you should turn Pollfish to release mode and publish your app.

> **Note:** After you take your app live, you should request your account to get verified through Pollfish Dashboard in the App Settings area.

> **Note:** There is an option to show **Standalone Demographic Questions** needed for Pollfish to target users with surveys even when no actually surveys are available. Those surveys do not deliver any revenue to the publisher (but they can increase fill rate) and therefore if you do not want to show such surveys in the Waterfall you should visit your **App Settings** are and disable that option. You can read more [here](https://www.pollfish.com/docs/demographic-surveys)

> **Note:** If you would like help on filling the App's privacy questionnaire please have a look at section 7 [here](https://www.pollfish.com/docs/ios)


## Step 8: Payouts on Screenouts (optional)

In Market Research monetization users can get screened out within the survey since the Researcher might be looking a different user based on the provided answers. Screenouts do not deliver any revenue for the publisher nor any reward for the users. If you would like to activate payouts on screenouts too please follow the steps as described <a href="https://www.pollfish.com/docs/pay-on-screenouts">here</a>. 
