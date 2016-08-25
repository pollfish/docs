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
<br/>

<h1>Implementing rewarded surveys - Step by Step</h1>

Below, you can see a list of all logical steps in order to archieve the rewarded approach with Pollfish surveys.

<h3>1. Initialize Pollfish in custom mode (skip Pollfish Indicator)</h3>

You should initialize Pollfish SDK in custom mode. With this mode, Pollfish indicator (small red rectangle ![alt text](https://storage.googleapis.com/pollfish-images/indicator.png)  ) will be skipped. Pollfish in custom mode ignores Pollfish panel behavior from Pollfish Developer Dashboard (you can read more on Pollfish panel behavior settings on our [FAQ page](https://pollfish.zendesk.com/hc/en-us/articles/205355891--What-do-different-PollFish-Indicator-Settings-mean-])). Custom mode always skips showing Pollfish indicator and always force open Pollfish survey panel view to app users.

<h3>2. Hide Pollfish survey panel</h3>

Immediately after Pollfish initialisationm you should call Pollfish hide function. This way you will ensure that Pollfish survey panel will not force slide if a survey is received on the device and therefore you will have full control on when to show Pollfish survey panel (for example with the click of a button or with a custom prompt you will make)

<h3>3. Register & listen to Pollfish survey received notification</h3>

You should register and listen for Pollfish survey received notification/listener. If you receive a survey received notification you can prompt your users with a custom prompt in order to complete a survey. 

In survey received notification you can easily find information on survey format (Basic or Playful) and money to be earned, if survey is completed, in USD cents.

## 4. Show custom prompt or offerwall entry

When you receive a notification that a survey was received on the device you can show a custom prompt, or a button or add an offerwall entry to prompt your users to take a survey in exchange for a reward.

> Below you can see an example of a custom prompt created by a publisher of the platform:

<p align="center"><img style="margin: 0 auto; display: block;" src="https://i1.wp.com/www.pollfish.com/wp-content/uploads/2016/05/earn.png?resize=768%2C460&ssl=1" width="320" height="auto"/>


or you can find more examples [here](https://www.pollfish.com/blog/2016/05/18/rewarded-surveys-monetize-mobile-apps/)


## 5. Show Pollfish survey panel

## 6. Listen for Pollfish survey completed or user not eligible notification

## 6. Listen for Pollfish survey completed or user not eligible notification





