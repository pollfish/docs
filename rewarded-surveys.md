With Pollfish, you are allowed to incentivize/reward your app's users for completing a survey. Rewarding users for completing surveys is a great approach since it increases engagemenent and retention in an app.

<br/>
<h1>Why use Pollfish rewarded surveys?</h1>

<br/>
**a) High Payouts** - Pollfish surveys follow a CPA model where action is completed survey. Payments on Pollfish Basic survey format, start from $0.30 per completed survey and can end up to several dollars.

**b) Users stay always within the app** - Users are incentivized to complete a survey from within the app. Survey procedure is executed through the app enviroment (Since everything is displayed as an overlay) and users never engage outside the app (like for example when user are incentivized to download an app). Once a survey is completed, surveys dissapear from the app and user continues with current flow of the app.

**c) Full transparency** - Pollfish SDK provides all necessary notifications from within the SDK to inform the publisher, in code, when a survey is received and how much money to be earned, upon survey completion, prior the publisher prompts the user. This way a publisher can make a decision if it worths to bother users based on money to be earned. Pollfish notifications provide the exact pricing avoiding  estimations or assumptions on pricing by the publisher. Furhtermore, Pollfish SDK provides notifications on survey completion to inform a publisher on how much were earned in order to credit the user.

**d) Enchanced security** - Pollfish provides secured server-to-server callbacks on survey completion to inform instantly a publisher if a survey was completed through an app.

**e) Users love them** - Users prefer completing a survey, instead of watching a video or installing an app, in exchange for a virtual reward. You can read more on this
[post](https://www.pollfish.com/blog/2016/05/18/rewarded-surveys-monetize-mobile-apps/) on Pollfish Blog.

</br>

> Below you can see an example implementation of using Pollfish rewarded surveys in order to unlock a feature in an app.
<p></p>  

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/incentivized1.gif" width="200" height="auto"/>
</p>

<br/>

<h1>Implementing rewarded surveys - Step by Step</h1>

Below, you can see a list of all logical steps in order to archieve the rewarded approach with Pollfish surveys.

## 1. Initialize Pollfish in custom mode (skip Pollfish Indicator)

You should initialize Pollfish SDK in custom mode. With this mode, Pollfish indicator (small red rectangle ![alt text](https://storage.googleapis.com/pollfish-images/indicator.png)  ) will be skipped. Pollfish in custom mode ignores Pollfish panel behavior from Pollfish Developer Dashboard. It always skips showing Pollfish indicator and always force open Pollfish survey panel view to app users.

## 2. Hide Pollfish panel

Immediately after Pollfish intiialisation you should call Pollfish hide function. This way you will ensure that Pollfish survey panel will not force slide if a survey is received on the device and therefore you will have full control on when to show the panel (for example with the click of a button or a custom prompt you will make)

## 3. Register  & listen to Pollfish survey received notification

You should register and listen for Pollfish notifications, listeners in order to know when a survey was received on the device. In the relevant Survey Received notification you can see if a survey was either of Playful or Basic format


## 4. Show Button (or custom prompt)

## 5. Show Pollfish survey panel

## 6. Listen for Pollfish survey completed or user not eligible notification

## 6. Listen for Pollfish survey completed or user not eligible notification




