Pollfish allows publishers to turn on Offerwall mode and allow their users to complete multiple survey offers within the same session. Pollfish Offerwall is similar to any other ad offerwall, however it focuses exclusively on surveys and market research

<br/>

<h1>Implementing Pollfish Offerwall - Step by Step</h1>

Below, you can see a list of all logical steps needed, in order to show Pollfish Offerwall undera rewarded placement

<h3>1. Initialize Pollfish in reward mode (skip Pollfish Indicator)</h3>

You should initialize Pollfish SDK in reward mode. With this mode, Pollfish indicator ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png) will be skipped. Pollfish in reward mode ignores Pollfish panel behaviour from Pollfish Developer Dashboard (you can read more on Pollfish panel behaviour settings on Pollfish [FAQ page](https://pollfish.zendesk.com/hc/en-us/articles/205355891--What-do-different-PollFish-Indicator-Settings-mean-])) and always hide Pollfish survey panel.

<h3>2. Register & listen to Pollfish survey received notification</h3>

You should register and listen for Pollfish survey received notification/listener. If you receive a survey received notification you can prompt your users with a custom prompt in order to enter the Offerwall. 

Survey received notification should be used in order to understand if the offerwall has is ready and has surveys. No further information are available through the notification and therefore no further parsing should be made to the notification object.

<h3>3. Show custom prompt for users to enter the Offerwall</h3>

When you receive a notification that a survey was received on the device you can show a custom prompt, or a button to prompt your users to to enter the Offerwall and earn some sort of a virtual currency.

> Below you can see an example of a custom prompt created by a publisher of the platform:

<p align="center"><img style="margin: 0 auto; display: block;" src="https://i1.wp.com/www.pollfish.com/wp-content/uploads/2016/05/earn.png?resize=768%2C460&ssl=1" width="320" height="auto"/>

