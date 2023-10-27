Pollfish provides an Offerwall mode where users are allowed to complete multiple survey offers within the same session. Pollfish Offerwall is similar to any other ad offerwall, however it focuses exclusively on surveys and market research.

<h1>Offerwall - How it works</h1>

With Pollfish Offerwall solution, users can choose and complete multiple surveys and get rewarded for their opinions. The flow that a user has to follow while using the Offerwall is as described below:

<h3>1. Unlocking Surveys</h3>

Users in order to be able to participate to surveys on the very first time the will get introduced to the platform they will have to answer a small set of Demographic questions to unlock surveys. After all demographic questions are filled users can start completing surveys. 

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/unlock_screens.png" width="750" height="auto"/>
  
  | **Note:** If a publisher knows the demographic info of the users upfront, he can pass them during initialization in code and skip those questions from being rendered to users

<h3>2. Choosing & Completing a Survey</h3>

Once a user ulocked surveys from the previous step, he can choose from a variety of different surveys to participate.   
If no surveys are available for that user, an empty state screen will be rendered to the user to inform him to check back later for survey opportunities.

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/flow.png" width="800" height="auto"/>

<h3>3. Getting Rewarded on Survey Completion</h3>

Users will get rewarded for every succesfully completed survey on the Offerwall after it passes validation from the real-time anti-fraud mechanism. Users can visit the history section of the Offerwall at any time to get more info on surveys succesfully completed or surveys that they got screened out and learn more about the reasons (this level of transparency can decrease complains from the users as they can check the status of their responses on their own)

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/history.png" width="260" height="auto"/>

<br/>

<h1>Implementing Pollfish Offerwall - Step by Step</h1>

Below, you can see a list of all the logical steps needed, in order to show Pollfish Offerwall under a rewarded placement:

<h3>1. Customize Offerwall Settings through Pollfish Dashboard</h3>

In the App Settings area of your Dashboard, you should create an Offerwall Placement and set your preferred settings.

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/dashboard_offerwall.png" width="460" height="auto"/>

You can customize the following settings:

**Reward Settings**

- Name of virtual reward shown on the wall
- Exhange rate. How much does your currency worth compared to one USD?

**Logo**

- You can upload your own logo that will be displayed on the top of the wall

**Theme**

- You can customize the primary colours of the wall and the background. 

<h3>2. Customize Mediation Network Settings</h3>

In the Survey settings of an Offerwall Placement you can customize the type of surveys you would like to see within the offerwall. You can enable or disable providers, set price floors per network, maxiumum length of survey, minimum aceptable conversion rate and even filter out surveys based on keywords!

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/mediation_latest.png" width="600" height="auto"/>


<h3>3. Initialize Pollfish in reward and offerwall mode </h3>

You should initialize Pollfish SDK in reward and offerwall mode. With this mode, Pollfish indicator will be skipped and Pollfish survey panel will stay hidden when the Offerwall is ready.

To sum up, initialize with the following in mind:

- rewardMode: true
- offerwallMode: true

<h3>4. Register & listen to Pollfish Survey Received notification</h3>

You should register and listen for Pollfish Survey Received notification/listener. If you receive a survey received notification you can prompt your users with a custom prompt in order to enter the Offerwall. 

Pollfish Survey Received notification should be used from publishers to check if the offerwall is available and has any surveys to be completed. No further information are available through the notification and therefore no further parsing should be made to the notification object.

<h3>5. Show custom prompt to users to enter the Offerwall</h3>

When you receive a notification that a survey was received on the device you can show a custom prompt, or a button to prompt your users to to enter the Offerwall and earn some sort of a virtual currency (As specified in step 1).

> Below you can see an example of a custom prompt created by a publisher of the platform:

<p align="center"><img style="margin: 0 auto; display: block;" src="https://i1.wp.com/www.pollfish.com/wp-content/uploads/2016/05/earn.png?resize=768%2C460&ssl=1" width="320" height="auto"/>

<h3>6. Open/Show the Offerwall</h3>

If a user chose to get into the Offerwall (by clicking on your custom prompt for example) you should call Pollfish show function in order to open Pollfish survey panel to the user, to start completing surveys.

<h3>7. Register & Listen for local Pollfish Survey Completed notifications (optional)</h3>

You can register and listen for Pollfish survey completed notifications/listener. Through the Survey Completed notification, you can easily find more detailed information on each survey completed including:

- Money to be earned in USD cents
- Survey Incidence Rate
- Survey Length of Interview
- Survey Class
- Reward Name
- Reward Value

> **Note:** It is strongly adviced that you do not reward users directly on survey completion notification within the SDK. You should register on Pollfish Dashboard to receive server-to-server callbacks as described in step 8 and reward your users upon the receival of that callbacks.


<h3>8. Register for server-to-server (s2s) callbacks on survey completion</h3>

In order to avoid user fraud it is strongly adviced to register a server-to-server callback on Pollfish Developer Dashboard in order to receive a relevant notification on your server side upon survey completion. Once this notification is received you can reward your users.

You can find detailed information on how to set up server-to-server callbacks [here](https://www.pollfish.com/docs/s2s)

<h3>9. Register & Listen for Pollfish User Not Eligible notification (optional)</h3>

Since Pollfish is a survey platform, some times users maybe screened out once a survey is started. Having that said, you can register and listen for Pollfish User Not Eligible notification/listener.  If this event is fired you will not earn any money from that survey and you should not reward your users either. 

<h3>10. Passing a custom user id upon survey completion to the server side (optional)</h3>

If you want to pass a custom user param on your server side during survey completion you should follow the steps below:

a) Pass your custom param during Pollfish initialization (check for requestUUID param in docs)

b) Set your server-to-server callback as described in step 8

c) Receive custom param on your server side during a survey completion

This approach is usually followed by publishers when looking to send over a unique identification of a user (as it is saved on publisher's side) to their server side through Pollfish SDK to associate that completion with a specific user.

<br/>

<h1>Sample projects (Show me some code!)</h1>

You can find examples in code on how to implement the Offerwall approach in the links below:


- [Android Sample Project](https://github.com/pollfish/android-sdk-pollfish/blob/master/sample-project/app/src/main/java/pollfish/com/sampleproject/OfferwallActivity.java)

- [iOS Sample Project](https://github.com/pollfish/ios-sdk-pollfish/blob/master/SampleProject/SampleProject/ThirdViewController.m)

- [Web Plugin Sample Project](https://github.com/pollfish/webplugin-offerwall-example)

- [Api Documentation Sample Project](https://github.com/pollfish/api-offerwall-example)

If you are using a different platform or engine please follow the logical steps as described above in order to archieve the desired behaviour.
