<div class="changelog" data-version="6.2.5.0">
v6.2.5.0

- Initial release

</div>

This guide is for publishers looking to use ironSource LevelPlay to load and show Rewarded Surveys from Pollfish in the same waterfall with other Rewarded Ads.

<br/>

# Prerequisites

- [Pollfish Developer Account](https://www.pollfish.com/dashboard/dev/)
- [IronSource Developer Account](https://platform.ironsrc.com/partners)
- iOS 10.0 or later
- XCode 12

> **Note:** Pollfish surveys can work with or without the IDFA permission on iOS 14+. If no permission is granted in the ATT popup, the SDK will serve non personalized surveys to the user. In that scenario the conversion is expected to be lower. Offerwall integrations perform better compared to single survey integrations when no IDFA permission is given

</br>

# Quick Guide

- Set up IronSource Rewarded Ads
- Set up Pollfish
- Add Pollfish IronSource Adapter to your project
- Publish your app

<br/>

# Analytical Steps

Below you can find a step by step guide on how to incorporate Pollfish surveys with ironSource LevelPlay:

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

<img style="margin: 0 auto; display: block; max-height: 300px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_ios_network_list.png"/>

<br/>

Configure Pollfish Network by clicking on the **Setup** button on the **Pollfish** network row from your App's Network list.

Fill the following input fields.

Key | Type
-------------| -------------
**1.1.1. `api_key`** <br/> Sets Pollfish SDK API key as provided by Pollfish | String
**1.1.2. `request_uuid`** <br/> Sets a unique id to identify a user and be passed through server-to-server callbacks | String
**1.1.3. `release_mode`** <br/> Sets Pollfish SDK to Developer or Release mode | Boolean
**1.1.4. `oferrwall_mode`** <br/> Sets Pollfish SDK to Oferwall Mode | Boolean

<br/>

### 1.1.1 `api_key`

Pollfish API Key as provided by Pollfish on [Pollfish Dashboard](https://www.pollfish.com/publisher/) after you sign up to the platform.

### 1.1.2 `request_uuid` or `null`

Sets a unique id to identify a user and be passed through server-to-server callbacks on survey completion. 

In order to register for such callbacks you can set up your server URL on your app's page on Pollfish Developer Dashboard and then pass your requestUUID through ParamsBuilder object during initialization. On each survey completion you will receive a callback to your server including the requestUUID param passed.

If you would like to read more on Pollfish s2s callbacks you can read the documentation [here](https://www.pollfish.com/docs/s2s)

### 1.1.3. `release_mode`

Sets Pollfish SDK to Developer or Release mode.

*   **Developer mode** is used to show to the developer how Pollfish surveys will be shown through an app (useful during development and testing).
*   **Release mode** is the mode to be used for a released app in any app store (start receiving paid surveys).

### 1.1.4 `oferrwall_mode`

Enables offerwall mode. If not set, one single survey is shown each time.

<br/>

<img style="margin: 0 auto; display: block; max-height: 450px;" src="https://storage.googleapis.com/pollfish_production/doc_images/ironsource_ios_network_config.png"/>

<br/>

After adding the above required info click **Save**

<br/>

## 2. Set Up Pollfish

### 2.1. Obtain a Developer Account

Register as a Publisher at [www.pollfish.com](https://www.pollfish.com/signup/publisher)

<br/>

### 2.2. Add new app on Pollfish Publisher Dashboard and copy the given API Key

Login at [www.pollfish.com](www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Publisher Dashboard. Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.

<br/>

## 3. Add Pollfish IronSource Adapter to your project

### **Manually import PollfishIronSourceAdapter**

Download the following frameworks

* [Pollfish SDK](https://www.pollfish.com/docs/ios)
* [IronSource SDK](https://developers.is.com/ironsource-mobile/ios/ios-sdk)
* [PollfishIronSourceAdapter](https://pollfish.com/docs/ios-ironsource-adapter)

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

### **Retrieve Pollfish IronSource Adapter through CocoaPods**

Add a Podfile with PollfishIronSourceAdapter pod reference:

```ruby
pod 'PollfishIronSourceAdapter'
```

You can find the latest PollfishIronSourceAdapter version on CocoaPods [here](https://cocoapods.org/pods/PollfishIronSourceAdapter)

Run pod install on the command line to install PollfishIronSourceAdapter pod.

<br/>

## Important step Objective-C based projects

For Objective-C based projects you will need to create an empty Swift file including Foundation framework and a bridging header file named `YourProjectName-Bridging-Header.h`. Skipping this step will result to compilation failure.

<!-- Add link to objc example project -->
You can see an example [here]()

<br/>

## 4. Request for a RewardedAd

<br/>

> **Note:** If you have already implemented Rewarded Ads in your app you can skip this step

<br/>

Import `IronSourceSDK`

<span style="text-decoration:underline">Swift</span>

If you are using swift, you need to make sure your application is pointing to `IronSource.h` file to include the bridge you need.

Select your Project from the project navigator and navigate to Build Settings -> Swift Compiler - General and add the following path to the Objective-C Bridging Header setting.

The path to the bridging header varies according to the way the integration was done

<span style="text-decoration:underline">**CocoaPods**</span>

```
${PODS_ROOT}/IronSourceSDK/IronSource/IronSource.xcframework/ios-arm64_armv7/IronSource.framework/Versions/A/Headers/IronSource.h
```

<span style="text-decoration:underline">**Manual**</span>

```
Frameworks/IronSource.framework/Headers/IronSource.h
```

Once you’ve completed the above step, you can use Swift seamlessly within the ironSource SDK, without importing any additional Header Files.

<span style="text-decoration:underline">Objective C</span>

```objc
#import <IronSource/IronSource.h>
```

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
        createAndLoadRewardedAd()
    }
}

@available(iOS 14, *)
func requestIDFAPermission() {
    #if canImport(AppTrackingTransparency)
    ATTrackingManager.requestTrackingAuthorization { status in
        DispatchQueue.main.async {
            self.createAndLoadRewardedAd()
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
        [self createAndLoadRewardedAd];
    }
}

- (void)requestIDFAPermission {
#if __has_include(<AppTrackingTransparency/AppTrackingTransparency.h>)
    if (@available(iOS 14, *)) {
        [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
            dispatch_async(dispatch_get_main_queue(), ^{
                [self createAndLoadRewardedAd];
            });
        }];
    } else {
        // Fallback on earlier versions
    }
#endif
}
```

<br/>

Initialize the IronSource SDK in your ViewController's `viewDidLoad`, `viewWillAppear` methods or after the IDFA permission response, passing your App Key as provided by the IronSource dashboard.

<span style="text-decoration:underline">Swift</span>

```swift
func createAndLoadRewardedAd() {
    ...

    ISIntegrationHelper.validateIntegration()   
    IronSource.setRewardedVideoDelegate(self)
    IronSource.initWithAppKey("APP_KEY")
}
```

<span style="text-decoration:underline">Objective C</span>

```objc
- (void)createAndLoadRewardedAd {
    ...
    
    [ISIntegrationHelper validateIntegration];
    [IronSource initWithAppKey:@"APP_KEY"];
    [IronSource setRewardedVideoDelegate:self];
}
```

<br/>

Comform to `ISRewardedVideoDelegate` so that you are notified when your ad is ready and of other ad-related events.

<span style="text-decoration:underline">Swift</span>

```swift
class ViewController: UIViewController, ISRewardedVideoDelegate
```

<span style="text-decoration:underline">Objective C</span>

```objc
@interface ViewController ()<MARewardedAdDelegate>
```

<br/>

When the Rewarded Ad is ready, present the ad by invoking `IronSource.showRewardedVideo`.

<span style="text-decoration:underline">Swift</span>

```swift
IronSource.showRewardedVideo(with: self)
```

<span style="text-decoration:underline">Objective C</span>

```objc
[IronSource showRewardedVideoWithViewController:self];
```

<br/>

You can view a short example on how to intergate rewarded ads below

<span style="text-decoration:underline">Swift</span>

```swift
import ObjectiveC.runtime
import AppTrackingTransparency

class ViewController: UIViewController, ISRewardedVideoDelegate {

    ...

    @IBOutlet weak var showRewardedAdButton: UIButton!

    override func viewDidLoad() {
        super.viewDidLoad()
        
        ATTrackingManager.requestTrackingAuthorization { status in
            self.createRewardedAd()
        }
    }

    private func createRewardedAd() {
        ISIntegrationHelper.validateIntegration()
        
        IronSource.setRewardedVideoDelegate(self)
        IronSource.initWithAppKey(appKey)
    }
    
    @IBAction func showRewardedAd(_ sender: Any) {
        IronSource.showRewardedVideo(with: self)
    }

    #pragma mark - ISRewardedVideoDelegate Protocol

    public func didReceiveReward(forPlacement placementInfo: ISPlacementInfo!) {}
    
    func rewardedVideoDidFailToShowWithError(_ error: Error!) {}
    
    func rewardedVideoDidOpen() {}
    
    func rewardedVideoDidClose() {}
    
    func rewardedVideoDidEnd() {}
    
    func rewardedVideoDidStart() {}
    
    func rewardedVideoHasChangedAvailability(_ available: Bool) {
        showRewardedAdButton.isEnabled = available
    }
    
    func didClickRewardedVideo(_ placementInfo: ISPlacementInfo!) {}

}
```

<span style="text-decoration:underline">Objective C</span>

```objc
#import <IronSource/IronSource.h>
#import <AppTrackingTransparency/AppTrackingTransparency.h>

@interface ViewController()<ISRewardedVideoDelegate>
@property (weak, nonatomic) IBOutlet UIButton *showRewardedAdBtn;
@end

@implementation ViewController

...

- (void)viewDidLoad {
    [super viewDidLoad];
    
    [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
        [self createRewardedAd];
    }];
}

- (void)createRewardedAd
{
    [ISIntegrationHelper validateIntegration];
    [IronSource initWithAppKey:@"APP_KEY"];
    [IronSource setRewardedVideoDelegate:self];
}

- (IBAction)showRewardedAd:(id)sender {
    [IronSource showRewardedVideoWithViewController:self];
}

#pragma mark - ISRewardedVideoDelegate Protocol

- (void)rewardedVideoHasChangedAvailability:(BOOL)available {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self.showRewardedAdBtn setEnabled:available];
    });
}

- (void)didReceiveRewardForPlacement:(ISPlacementInfo *)placementInfo {}

- (void)rewardedVideoDidFailToShowWithError:(NSError *)error {}

- (void)rewardedVideoDidOpen {}

- (void)rewardedVideoDidClose {}

- (void)rewardedVideoDidStart {}

- (void)rewardedVideoDidEnd {}

- (void)didClickRewardedVideo:(ISPlacementInfo *)placementInfo {}

@end
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

# More info

You can read more info on how the Pollfish SDKs work or how to get started with IronSource at the following links:

[Pollfish iOS SDK](https://pollfish.com/docs/ios)

[IronSource iOS SDK](https://developers.is.com/ironsource-mobile/ios/ios-sdk)
