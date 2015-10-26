<div class="changelog changelog-4.1.0">
v4.1.0

- Fixed bug on orientation changes
- Converted lib to ARC

v4.0.3

- Fixed bug in init function with Request UUID in release mode

v4.0.2

- Weak link of AdSupport framework
- Added init function with option to pass a custom param and receive it on server-to-server callback
- Added UserAttributesDictionary class for passing attributes around user
- Added various bug fixes and optimizations

v4.0.1

- Added support of circle questions
- Added various bug fixes and optimizations

v4.0.0

- Added various bug fixes and optimizations
</div>

## Quick Guide

1.  Download Pollfish iOS SDK and unzip it
2.  Import Pollfish.framework to your project
3.  Import AdSupport.framework and CoreTelephony.framework to your project
4.  Call init and destroy function of Pollfish in the App’s Delegate
5.  Set to Release mode and release in AppStore
6.  Update your privacy policy

**Note: Be careful to set andDebuggable parameter of the init function to false (Release mode) prior releasing to AppStore!**

## Requirements

- iOS version 6.0 +  
- Xcode 4.5 or later

## Steps Analytically

### 1\. Download Pollfish iOS SDK and unzip it

### 2\. Add the pollfish framework in your project

In Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.  

The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane).  

**Note: The framework is a folder and you should add the whole folder into your project.**

### 3\. Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework  

**Note: If your deployment target is less than iOS 6.0, change the AdSupport.framework from Required to Optional.**

### 4\. Embedding Pollfish into your code

#### Import Pollfish header

You have to include Pollfish library headers in every file that you will use Pollfish.  


```
#import <Pollfish/Pollfish.h>
```

#### Initializing Pollfish in App Delegate

The init function of Pollfish must be called in your application’s delegate applicationDidBecomeActive: method. This way it is ensured that Pollfish surveys will be refreshed each time your application will become active.  

```
- (void)applicationDidBecomeActive:(UIApplication *)application
{
  [Pollfish initAtPosition: (PollfishPosition)
               	withPadding: (int)
	    andDeveloperKey: (NSString *)
              andDebuggable: (BOOL) 
	      andCustomMode: (BOOL)];
}
```

#### Pollfish init function takes the following parameters:

**1\. initAtPosition** (PollfishPosition) - The Position where you wish to place the Pollfish indicator. There are six different options:  

- PollFishPositionBottomLeft  
- PollFishPositionBottomRight  
- PollFishPositionTopLeft  
- PollFishPositionTopRight  
- PollFishPositionMiddleLeft  
- PollFishPositionMiddleRight  

**2\. withPadding** (int) - The padding from top or bottom of the screen according to PollfishPosition of the indicator (small red rectangle) specified before (0 is the default value)  

**Note: *if used in MIDDLE position, padding is calculating from top.**  

**3\. andDeveloperKey** (NSString *)- Your API Key. This is the key that allows you to use Pollfish in your app. You can find it on Pollfish website after your registration, when you create an app in “My apps” section in the panel.  

**4\. andDebuggable (BOOL)** – Debug or Release mode  

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

• **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).  
• **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

**Note: Be careful to set andDebuggable parameter to false prior releasing to AppStore!**  

5\. **andCustomMode** (BOOL) – use Pollfish in the standard/recommended way or achieve a specific behavior (false is the default option you should use)  

<span style="text-decoration: underline">customMode – true or false?</span>  
**• false:** is the standard/recommended way of using Pollfish in your apps. It enables controlling the behavior of Pollfish indicator in an app from Pollfish panel on the website.  

**• true:** ignores Pollfish behavior from Pollfish panel on the website. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates.  

Below you can see an example of the init function:  

```
[Pollfish initAtPosition:PollFishPositionMiddleRight
		withPadding: 0
	    andDeveloperKey: @"2ae349ab-30b8-4100-bc4d-b33b82e76519" 
              andDebuggable: false 
              andCustomMode: false];
```

### Destroying Pollfish

You have to release all the resources Pollfish kept during the termination of your application. This should be done in your application’s delegate applicationWillTerminate: method.  

```
- (void)applicationWillTerminate:(UIApplication *)application
{
    // ...
    [Pollfish destroy];
}
```

### Call of init when changes in your app’s view hierarchy happen during app’s lifecycle or Pollfish is not shown on top view (optional)

When your app changes it’s view hierarchy during it’s lifecycle eg through a storyboard, or when Pollfish is not shown on the top view, you can call Pollfish init again in your current’s ViewController viewDidLoad that is on super view to bring Pollfish back on the top of your views.  

For example:

```
- (void)viewDidLoad
{
    [super viewDidLoad];
    
    [Pollfish initAtPosition: PollFishPositionMiddleRight
                 withPadding: 0
             andDeveloperKey: @"2ae349ab-30b8-4100-bc4d-b33b82e76519" 
               andDebuggable: false 
               andCustomMode: false];
}
```

Another example is when showing for example a modal view controller. This controller changes current view hierarchy since it is displayed on the top. Therefore, in that case you need to call init again to bring Pollfish back on the top.  

For example:  

```
- (IBAction)showModal:(id)sender {
						    
    	UIStoryboard *storyboard = [UIStoryboard storyboardWithName:@"Main_iPhone" bundle:nil];
 

	MyModalViewController  *myModalViewController = [storyboard instantiateViewControllerWithIdentifier:@"MyModalViewController"];
    	myModalViewController.modalPresentationStyle = UIModalPresentationFullScreen;
   
  	[self presentViewController: myModalViewController animated:YES completion:nil];
    
	[Pollfish initAtPosition: PollFishPositionMiddleRight
                     withPadding: 0
		 andDeveloperKey: @"2ae349ab-30b8-4100-bc4d-b33b82e76519" 
                   andDebuggable: false 
                   andCustomMode: false];

}



- (IBAction)dismissController:(id)sender {

    
    	[[self presentingViewController] dismissViewControllerAnimated:YES completion:^{
        
        [Pollfish initAtPosition: PollFishPositionMiddleLeft
                     withPadding: 0
                 andDeveloperKey: @"af89aaf1-b7d4-46c1-8e91-b2625c2d5dbe"
                   andDebuggable: true andCustomMode:false];
        
    	}];
    

}
```

Note:

• It is very important to call init function of Pollfish when the view hierarchy has already changed. Therefore in the example above you have to call init after the completion of the dismissal of the modal view controller.  

• Be careful to use the same arguments as the arguments you used in the init function in your app’s delegate.  

• Even if you call init in any ViewController somewhere within the app lifecycle you should still keep the init and destroy function in your App’s Delegate.  

If you still have questions regarding how to handle view hierarchy changes have a look in the SampleApp in the iOS SDK  

## Other init methods (optional)

### Passing custom parameter for server to server postback calls

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function within the SDK and receive it back with Server to Server, survey completed postback call you can use:  

```
 [Pollfish initAtPosition: (PollfishPosition)
               	withPadding: (int)
	    andDeveloperKey: (NSString *)
              andDebuggable: (BOOL) 
	      andCustomMode: (BOOL)
	     andRequestUUID: (NSString *)];
```

## Update your Privacy Policy

### Add the following paragraph to your app's privacy policy

“Survey Serving Technology  

This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone) is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.  

APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”

## Distributing your app to AppStore

Pollfish uses Advertising Identifier (IDFA) for survey distribution and therefore when submitting your app to the App you should select the following options as seen in the image below:  

![](/img/documentation/idfa_2.jpg)

## Other actions

### Manually show or hide Pollfish (optional)

You can manually hide and show Pollfish from your various UIVIewControllers. by calling anywhere after initialization:  

```
Pollfish.show();
```

or  

```
Pollfish.hide();
```

For example:  

```
// MyViewController1
- (void)viewWillAppear:(BOOL)animated
{
    // ...
    [Pollfish hide];
}

// MyViewController2
- (void)viewWillAppear:(BOOL)animated
{
    // ...
    [Pollfish show];
}
```

### Update user location (optional)

You can update user’s location anytime after initialization to get better fill rate on surveys by calling the following:  

```
[Pollfish updateLocationWithLatitude:(double)lat andLongitude:(double)lon andHorizontalAccuracy:(double)acc];
```

For example:

```
[Pollfish updateLocationWithLatitude:42.682435 andLongitude:-76.376953 andHorizontalAccuracy:2.0];
```

### Set custom user attributes (optional)

You can set attributes that you receive from your app regarding a user in order to receive a better fill rate and higher priced surveys.  

Create a UserAttributesDictionary object and then you can use that object to set different user attributes by calling the following function:  

```
[Pollfish setAttributeDictionary:(UserAttributesDictionary *) dict];
```

For example:

```
UserAttributesDictionary *userAttributesDictionary = [[UserAttributesDictionary alloc] init];

[userAttributesDictionary setAge:AGE(_36)];
[userAttributesDictionary setGender: GENDER(MALE)];
[userAttributesDictionary setAgeGroup: AGE_GROUP(_35_44)];
[userAttributesDictionary setFacebookId:@"facebookId"];
[userAttributesDictionary setTwitterId:@"twitterId"];
[userAttributesDictionary setMaritalStatus:MARITAL_STATUS(DIVORCED)];
 
[userAttributesDictionary setCustomAtributesWithKey:@"PARAM_KEY" andAttrValue: @"PARAM_VALUE"];

[Pollfish setAttributeDictionary:userAttributesDictionary];
```

## Implement Pollfish event listeners

### Get notified when a survey is received (optional)

You can be notified when a survey is received via the iOS Notification Center. Note that the observer should be already registered when a survey is received in order to run the selector.  

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(surveyReceived) name:@"PollfishSurveyReceived" object:nil];

- (void)surveyReceived
{
    NSLog(@"A survey was received!");
}
```

You can also get informed about the price and type of survey (playful or not) that was received by listening and reading the relevant notification object. Price is shown in USD (estimated based on daily exchange currency).

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishReceived:) name:@"PollfishSurveyReceived" object:nil];

- (void)pollfishReceived:(NSNotification *)notification
{
    BOOL playfulSurvey = [[[notification userInfo] valueForKey:@"playfulSurvey"] boolValue];
    int surveyPrice = [[[notification userInfo] valueForKey:@"surveyPrice"] intValue];
    
    NSLog(@"Pollfish Survey Received - Playful Survey: %@ with survey price: %d" , playfulSurvey?@"YES":@"NO", surveyPrice);
}
```

### Get notified when survey is completed (optional)

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(surveyCompleted) name:@"PollfishSurveyCompleted" object:nil];

- (void)surveyCompleted
{
    NSLog(@"Pollfish Survey Completed!");
}
```

### Get notified when a user is not eligible for a Pollfish survey (optional)

You can be notified when a user is not eligible for a Pollfish survey after accepting to take it via the iOS Notification Center.  

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishUsernotEligible) name:@"PollfishUserNotEligible" object:nil];

- (void)pollfishUsernotEligible
{
    NSLog(@"Pollfish User Not Eligible");
}
```

### Get notified when survey is not available (optional)

You can be notified when a survey is not available for a user via the iOS Notification Center.  

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(surveyNotAvailable) name:@"PollfishSurveyNotAvailable" object:nil];

- (void) surveyNotAvailable
{
    NSLog(@"Pollfish Survey Not Available!");
}
```

### Get notified when Pollfish is opened (optional)

You can be notified when a user opens Pollfish survey panel via the iOS Notification Center.  

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishOpened) name:@"PollfishOpened" object:nil];

- (void)pollfishOpened
{
    NSLog(@"Pollfish is opened!");
}
```

### Get notified when Pollfish is closed (optional)

You can be notified when a user closes Pollfish survey panel via the iOS Notification Center.  

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishClosed) name:@"PollfishClosed" object:nil];

- (void)pollfishClosed
{
    NSLog(@"Pollfish is closed!");
} 
```

