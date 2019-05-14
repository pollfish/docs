Pollfish allows publishers to incentivize/reward their app's users for completing a survey. Rewarding users for completing surveys is a great approach since it increases engagemenent and retention in an app.

<br/>
<h1>Why use Pollfish Rewarded Surveys?</h1>

<br/>
**a) High Payouts** - Pollfish surveys follow a CPA model where action is completed survey. Payments on Pollfish Basic survey format, start from $0.30 per completed survey and can end up to several dollars. 

**b) Users stay always within the app** - Users are incentivized to complete a survey from within the app. Survey procedure is executed through the app enviroment (Since everything is displayed as an overlay) and users never engage outside the app (like for example when user are incentivized to download an app). Once a survey is completed, surveys dissapear from the app and user continues with current flow of the app.

**c) Full transparency** - Pollfish SDK provides all necessary notifications from within the SDK to inform the publisher, in code, when a survey is received and how much money to be earned, upon survey completion, prior the publisher prompts the user. This way a publisher can make a decision if it worths to bother users based on money to be earned. Pollfish notifications provide the exact pricing avoiding  estimations or assumptions on pricing by the publisher. Furhtermore, Pollfish SDK provides notifications on survey completion to inform a publisher on how much monery were earned in order to credit a user.

**d) Enchanced security** - Pollfish provides secured server-to-server callbacks on survey completion to inform instantly a publisher if a survey was completed through an app.

**e) Users love them** - Users prefer completing a survey instead of watching a video or installing an app, in exchange for a virtual reward. You can read more on this
[here](https://www.pollfish.com/blog/2016/05/18/rewarded-surveys-monetize-mobile-apps/), on Pollfish Blog.

</br>

> Below you can see an example implementation of using Pollfish rewarded surveys in order to unlock a feature in an app.
<p></p>  

<p align="center"><img style="margin: 0 auto; display: block; border: 1px solid #000;" src="https://storage.googleapis.com/pollfish-images/incentivized1.gif" width="200" height="auto"/>
</p>

<br/>
<br/>

<h1>Implementing rewarded surveys - Step by Step</h1>

Below, you can see a list of all logical steps needed, in order to archieve the rewarded approach with Pollfish surveys.

<h3>1. Initialize Pollfish in reward mode (skip Pollfish Indicator)</h3>

You should initialize Pollfish SDK in custom mode. With this mode, Pollfish indicator ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png) will be skipped. Pollfish in custom mode ignores Pollfish panel behaviour from Pollfish Developer Dashboard (you can read more on Pollfish panel behaviour settings on Pollfish [FAQ page](https://pollfish.zendesk.com/hc/en-us/articles/205355891--What-do-different-PollFish-Indicator-Settings-mean-])). Custom mode always skips showing Pollfish indicator and hides Pollfish survey panel view from app users.

<h3>2. Register & listen to Pollfish survey received notification</h3>

You should register and listen for Pollfish survey received notification/listener. If you receive a survey received notification you can prompt your users with a custom prompt in order to complete a survey. 

In survey received notification you can easily find information on survey format (Basic or Playful) and money to be earned, if survey is completed, in USD cents.

<h3>3. Show custom prompt or OfferWall entry</h3>

When you receive a notification that a survey was received on the device you can show a custom prompt, or a button or add an offerwall entry to prompt your users to take a survey in exchange for a reward.

> Below you can see an example of a custom prompt created by a publisher of the platform:

<p align="center"><img style="margin: 0 auto; display: block;" src="https://i1.wp.com/www.pollfish.com/wp-content/uploads/2016/05/earn.png?resize=768%2C460&ssl=1" width="320" height="auto"/>


or you can find more examples [here](https://www.pollfish.com/blog/2016/05/18/rewarded-surveys-monetize-mobile-apps/)


<h3>4. Show Pollfish survey</h3>

If a user chose to take a survey (though your custom prompt for example) you should call Pollfish show function in order to open Pollfish survey panel to the user, to complete the survey. 

> **Note:** On Android and iOS there is also an optional function that you can call in order to see if a survey is present/available on the device (did not expire), prior calling Pollfish show.

<h3>5. Register & Listen for Pollfish survey completed notification</h3>

You should register and listen for Pollfish survey completed notification/listener. In survey completed notification you can easily find information on survey completed format (Basic or Playful) and money earned in USD cents.

> **Note:** It is strongly adviced that you do not reward users directly on survey completion notification within the SDK. You should register on Pollfish Dashboard a server-to-server callback as described in step 7 and reward your users upon the receiveal of that callback


<h3>6. Register for server-to-server (s2s) callbacks on survey completion</h3>

In order to avoid user fraud it is strongly adviced to register a server-to-server callback on Pollfish Developer Dashboard in order to receive a relevant notification on your server side upon survey completion. Once this notification is receivedm you can reward your users.

You can find detailed information on how to set up server-to-server callbacks [here](https://www.pollfish.com/docs/s2s)


<h3>7. Register & Listen for Pollfish user not eligible notification</h3>

Since Pollfish is a survey platform, some times users maybe screened out once a survey is started. Having that said, you should register and listen for Pollfish user not eligible notification/listener.  If this event is fired you will not earn any money from that survey and you should not reward your users either. The best approach to handle this case is to inform your users with a custom prompt. 


> Below you can see an example of handling user not eligible event by a Pollfish partner

<p align="center"><img style="margin: 0 auto; display: block; border: 1px solid #000;" src="https://storage.googleapis.com/pollfish-images/eligible_not.png" width="250" height="auto"/>


<h3>8. Passing custom user params on survey completion to server side (optional)</h3>

If you want to pass custom params on your server side during survey completion you should follow the steps below:

a) Pass your custom param during Pollfish initialization (check for requestUUID param in docs)

b) Set your server-to-server callback as described in step 7

c) Receive custom param on your server side during a survey completion

This approach is usually followed by publishers when looking to send over a unique identification of a user (as it is saved on publisher side) to server side through Pollfish SDK to associate that completion with a specific user.

<br/>
<br/>
<h1>Examples of integrations</h1>

Below, you can see some examples of implementations of the rewarded approach by Pollfish partners:

<u>Animated</u>
<p align="center"><img style="border: 1px solid #000;" src="https://i0.wp.com/www.pollfish.com/wp-content/uploads/2016/08/textme.gif?resize=638%2C1024&ssl=1" width="250" height="auto"/>        <img style="border: 1px solid #000;" src="https://i0.wp.com/www.pollfish.com/wp-content/uploads/2016/08/ufl_survey-1.gif?resize=639%2C1024&ssl=1" width="250" height="auto"/></p>

<u>Screenshots</u>
<p align="center"><img src="https://i0.wp.com/www.pollfish.com/wp-content/uploads/2016/05/survey1.png?zoom=2&resize=416%2C251&ssl=1" width="300" height="auto"/>        <img  src="https://i1.wp.com/www.pollfish.com/wp-content/uploads/2016/05/Screen-Shot-2016-05-18-at-15.06.17.png?resize=1024%2C617&ssl=1" width="300" height="auto"/></p>


You can always see more examples of implementations at the following blog posts [here](https://www.pollfish.com/blog/2016/05/18/rewarded-surveys-monetize-mobile-apps/) and [here](https://www.pollfish.com/blog/2016/08/03/rewarded-surveys-in-mobile-apps/)
<br/>
You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a>
<br/>
<br/>
<h1>Sample projects (Show me some code!)</h1>

You can find examples in code on how to implement the rewarded approach in the links below:


- [Android Sample Project](https://github.com/pollfish/android-sdk-pollfish/blob/master/sample-project/app/src/main/java/pollfish/com/sampleproject/RewardedSurveyActivity.java)

- [iOS Sample Project](https://github.com/pollfish/ios-sdk-pollfish/blob/master/SampleProject/SampleProject/SecondViewController.m)

- [Web Plugin Sample Project](https://github.com/pollfish/webplugin-rewarded-example)

- [Api Documentation Sample Project](https://github.com/pollfish/api-pollfish)

If you are using a different platform or engine please follow the logical steps as described above in order to archieve the desired behaviour.



