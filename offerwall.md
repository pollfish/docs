Pollfish allows publishers to turn on Offerwall mode and enable their users to complete multiple survey offers within the same session. Pollfish Offerwall is similar to any other ad offerwall, however it focuses exclusively on surveys and market research


<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/offerwall_landing.png" width="320" height="auto"/>



<br/>

<h1>Implementing Pollfish Offerwall - Step by Step</h1>

Below, you can see a list of all logical steps needed, in order to show Pollfish Offerwall under a rewarded placement

<h3>1. Customize Offerwall Settings through Pollfish Dashboard</h3>

In the App Settings are of the Dashboard you should visit the Offerwall settings are and set your preferred settings.

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/dashboard_offerwall.png" width="320" height="auto"/>

You can customize the following settings:

**Reward Settings**

- Name of virtual reward shown on the wall
- Exhange rate. How much of your currency does one USD ($) worth?

**Logo**

- You can upload your own logo that will be displayed on the top of the wall and give some sort of familiarity to the users

**Theme**

- You can customize the primary colour of the wall and the background. 


<h3>1. Initialize Pollfish in reward mode (skip Pollfish Indicator)</h3>

You should initialize Pollfish SDK in reward mode. With this mode, Pollfish indicator ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png) will be skipped. Pollfish in reward mode ignores Pollfish panel behaviour from Pollfish Developer Dashboard (you can read more on Pollfish panel behaviour settings on Pollfish [FAQ page](https://pollfish.zendesk.com/hc/en-us/articles/205355891--What-do-different-PollFish-Indicator-Settings-mean-])) and always hide Pollfish survey panel.

<h3>2. Register & listen to Pollfish survey received notification</h3>

You should register and listen for Pollfish survey received notification/listener. If you receive a survey received notification you can prompt your users with a custom prompt in order to enter the Offerwall. 

Survey received notification should be used in order to understand if the offerwall has is ready and has surveys. No further information are available through the notification and therefore no further parsing should be made to the notification object.

<h3>3. Show custom prompt for users to enter the Offerwall</h3>

When you receive a notification that a survey was received on the device you can show a custom prompt, or a button to prompt your users to to enter the Offerwall and earn some sort of a virtual currency.

> Below you can see an example of a custom prompt created by a publisher of the platform:

<p align="center"><img style="margin: 0 auto; display: block;" src="https://i1.wp.com/www.pollfish.com/wp-content/uploads/2016/05/earn.png?resize=768%2C460&ssl=1" width="320" height="auto"/>

<h3>4. Show Pollfish survey</h3>

If a user chose to get into the Offerwall (though your custom prompt for example) you should call Pollfish show function in order to open Pollfish survey panel to the user, to start completing surveys

<h3>5. User unlocking surveys</h3>

Users in order to be able to participate to surveys on the very first time the will get introduced to the platform they will have to answer a small set of Demographic questions to unlock surveys. After all demographic questions are filled users can start completing surveys from clients.

<h3>5. Register & Listen for local Pollfish survey completed notifications</h3>

You can register and listen for Pollfish survey completed notifications/listener. In survey completed notification you can easily find information on each survey completed like:

- Money to be earned in USD cents
- Survey Incidence Rate
- Survey Length of Interview
- Survey Class
- Reward Name
- Reward Value

> **Note:** It is strongly adviced that you do not reward users directly on survey completion notification within the SDK. You should register on Pollfish Dashboard a server-to-server callback as described in step 7 and reward your users upon the receiveal of that callback

<h3>6. Register for server-to-server (s2s) callbacks on survey completion</h3>

In order to avoid user fraud it is strongly adviced to register a server-to-server callback on Pollfish Developer Dashboard in order to receive a relevant notification on your server side upon survey completion. Once this notification is receivedm you can reward your users.

You can find detailed information on how to set up server-to-server callbacks [here](https://www.pollfish.com/docs/s2s)


<h3>7. Register & Listen for Pollfish user not eligible notification</h3>

Since Pollfish is a survey platform, some times users maybe screened out once a survey is started. Having that said, you can register and listen for Pollfish user not eligible notification/listener.  If this event is fired you will not earn any money from that survey and you should not reward your users either. 


<h3>8. Passing custom user params on survey completion to server side (optional)</h3>

If you want to pass custom params on your server side during survey completion you should follow the steps below:

a) Pass your custom param during Pollfish initialization (check for requestUUID param in docs)

b) Set your server-to-server callback as described in step 7

c) Receive custom param on your server side during a survey completion

This approach is usually followed by publishers when looking to send over a unique identification of a user (as it is saved on publisher side) to server side through Pollfish SDK to associate that completion with a specific user.

<br/>

<h1>Sample projects (Show me some code!)</h1>

You can find examples in code on how to implement the rewarded approach in the links below:


- [Android Sample Project](https://github.com/pollfish/android-sdk-pollfish/blob/master/sample-project/app/src/main/java/pollfish/com/sampleproject/OfferwallActivity.java)

- [iOS Sample Project](https://github.com/pollfish/ios-sdk-pollfish/blob/master/SampleProject/SampleProject/ThirdViewController.m)

- [Web Plugin Sample Project](https://github.com/pollfish/webplugin-offerwall-example)

- [Api Documentation Sample Project](https://github.com/pollfish/api-offerwall-example)

If you are using a different platform or engine please follow the logical steps as described above in order to archieve the desired behaviour.
