Corona plugin to allow integration of Pollfish surveys into Android and iOS apps. 

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.

## Prerequisites

*	Android 10+ using Google Play Services
*	iOS version 6.0+
*	Corona Entererise

## Quick Guide

* Create Pollfish developer account, create new app and grap it's API key
* Install Pollfish plugin and call init function
* Set to Release mode and release in Store
* Update your app's privacy policy



![alt tag](https://www.pollfish.com/img/rocketMobile.png)

## Steps Analytically

### 1. Obtain a Developer Account

Register as a Developer at [www.pollfish.com](http://www.pollfish.com)

### 2. Add new app in Pollfish panel and copy the given API Key

Login at [www.pollfish.com](http://www.pollfish.com) and add a new app at Pollfish panel in section My Apps and copy the given API key for this app to use later in your init function in your app.

### 3. Installing the plugin

Download [this repository](https://github.com/pollfish/corona-plugin-pollfish) band paste the contents over your Corona Enterprise project. If you want to read how to use plugins please read Corona guide [here](https://docs.coronalabs.com/daily/native/plugin/index.html).  Then:

#### 3.1 Download Pollfish latest SDKs from here:

*	Android: [https://www.pollfish.com/docs/android](https://www.pollfish.com/docs/android)
*	iOS: [https://www.pollfish.com/docs/ios](https://www.pollfish.com/docs/ios)

#### 3.2 Copy the relevant files from this repository in your project's structure:

##### 3.2.1 iOS 

1. Copy the files form the Plugin folder to your ios/Plugin folder in your project
2. Add the pollfish and other required framework in your project

In Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it. 

The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane). 

Note: The framework is a folder and you should add the whole folder into your project.

Finally add the following frameworks (if you don’t already have them) in your project

* AdSupport.framework
* CoreGraphics.framework
* CoreTelephony.framework 

Note: If your deployment target is less than iOS 6.0, change the AdSupport.framework from Required to Optional.

##### 3.2.2 Android

- Paste pollfish.jar file into android/libs
- Copy Pollfish plugin files into the project structure


### 4. Initialize Pollfish

Init function takes the following parameters:

1.	**debugMode**: - Choose Debug or Release Mode
2.	**customMode**: - Init or custom init
3.	**apiKey**: - Your API Key (from step 2)
4.	**pos**: - The Position where you wish to place the Pollfish indicator. There are four different options {PollFishPositionTopLeft, PollFishPositionBottomLeft,PollFishPositionTopRight,PollFishPositionBottomRight,PollFishPositionMiddleLeft,PollFishPositionMiddleRight}
5.	**indPadding**: - The padding (in dp) from top or bottom according to Position of the indicator specified before (0 is the default value – |*if used in MIDDLE position, padding is calculating from top).

For example:

```
pollfish.init(
{
    pos = PollFishPositionTopRight,
    indPadding = 50,
    apiKey = "YOUR_API_KEY",
    debugMode = true,
    customMode = false,
    listener = listenerFunc,
});
```

#### Debug Vs Release Mode

You can use Pollfish either in Debug or in Release mode. 

* **Debug mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
* **Release mode** is the mode to be used for a released app (start receiving paid surveys).


**Note: In Android debugMode parameter is ignored. Your app turns into debug mode once it is signed with a debug key. If you sign your app with a release key it automatically turns into Release mode.**

**Note: Be careful to turn the debugMode parameter to false when you release your app in a relevant app store!!**



#### init Vs custom init

*	**init function** is the standard way of using Pollfish in your apps. Using init function enables controlling the behavior of Pollfish in an app from Pollfish panel.

*	**custom init function** ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates. Both init and customInit functions have the same arguments.

#### 4.1 Other Init functions (optional)

##### Passing custom parameter for server to server postback calls

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function within the SDK and receive it back with Server to Server, survey completed postback call you can use

For example:

```
pollfish.init(
{
    pos = PollFishPositionTopRight,
    indPadding = 50,
    apiKey = "YOUR_API_KEY",
    debugMode = true,
    customMode = false,
    requestUUID = "my_uuid",
    listener = listenerFunc,
});
```

### 5. Update your Privacy Policy

#### Add the following paragraph to your app's privacy policy


*Survey Serving Technology*

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone)  is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*


*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THE DRAWS. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.*


### 6. Handling application entering to foreground (optional)

You should handle the event when your app is entering to foreground in order to initialise Pollfish again by listening to the relevant event.

For example:

```
Runtime:addEventListener( 'system', systemEvent );
```

```
local function systemEvent( event )

local phase = event.phase;

if event.type == 'applicationResume' then

print("applicationResume - call init here")

end

return true

end
```


### 7. Implement Pollfish event listeners (optional)

Get notified when a Pollfish survey is received,completed, user is not eligible, Pollfish survey panel is open or closes by listening to relevant events. 


For example:

```
local function listenerFunc(event)

print("[Pollfish] listenerFunc: " .. tostring(event.phase))

if event.phase == "onPollfishSurveyReceived" then

print("Pollfish - onPollfishSurveyReceived")
txt.text="onPollfishSurveyReceived";

elseif event.phase == "onPollfishSurveyCompleted" then

print("Pollfish - onPollfishSurveyCompleted")
txt.text="onPollfishSurveyCompleted";

elseif event.phase == "onPollfishSurveyNotAvailable" then

print("Pollfish - onPollfishSurveyNotAvailable")
txt.text="onPollfishSurveyNotAvailable";

elseif event.phase == "onUserNotEligible" then

print("Pollfish - onUserNotEligible")
txt.text="onUserNotEligible";

elseif event.phase == "onPollfishOpened" then

print("Pollfish - onPollfishOpened")
txt.text="onPollfishOpened";

elseif event.phase == "onPollfishClosed" then

print("Pollfish - onPollfishClosed")
txt.text="onPollfishClosed";

else

print("Pollfish - event not recognised: " .. tostring(event.phase))

end


end
```
### 9. Other actions (optional)

#### 9.1 Manually show Pollfish panel

You can manually hide and show Pollfish from your various UIVIewControllers. by calling anywhere after initialization: 

For example:

```
pollfish.show(listenerFunc)
```

or

```
pollfish.hide(listenerFunc)
```


## More Info

For more info about Pollfish please check [Pollfish Website](http://www.pollfish.com). For more info regarding releasing in different stores look at the documentation pages on the website.
