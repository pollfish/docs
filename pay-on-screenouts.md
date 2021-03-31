<h1>Pay on Screenouts</h1>


Pay on Screenouts is a feature provided by Pollfish in order to allow partners to have more predictable revenue. This feature aims to overcome Market Research monetization limitations where users can get screened out from a survey and not get a reward even if they intent to honestly fill one.

With focus on providing an optimal user experience, respecting users' time and ensuring revenue in every session, partners can enable Pay on Screenouts feature per Mediation Network per app through their Dashboard. Pay on Screenouts feature distributes in a more fair way, revenue from successful survey completes, in every session including on screenouts with a small compromise in the payout in survey completion. No minimum payouts or price floors are applied in that case.

> **Note:**  Payable screenouts are screenouts that happened because the user got screened out for different reasons such as profiling, screenout on a screening question, quota full, survey closed and other reasons that took time from the user who was trying to answer honestly but did not manage to successfully complete the survey. Screenouts due to fraud, quality, VPN or security are not payable. 

> **Note:**  Payable screenouts are disabled by default in all new apps.

<h2>Activating Pay on Screenouts</h2>

Publishers can visit their Dashboard in the <i>Settings-Mediation Settings</i> area and <b>Enable</b> or <b>Disable</b> Pay on Screenouts feature per Mediation Network per App. 

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/enable_pay.png" width="650" height="auto"/>

In the same section the publisher can  review the current rates on payments for completes or screenouts if the feature is enabled. 

> **Note:**  Keep in mind that prices shared in this section are just informative and reflect the prices seen on the platform the previous minutes

> **Note:**  Activating Pay on Screenouts might result to lower inventory due to limitations on low payouts 


<h2>User Experience</h2>

If publishers would like to deliver a reward to their users on screenouts and prompt them within the survey's UI, they should enable the <i>Reward Settings</i> setting, depending on their integration approach, in the <i>Settings-App Settings</i> area of their app.

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/reward_settings.png" width="320" height="auto"/>

In that section, the publishers can specify the Reward Name and a elevant Exchange Rate. 

When Reward Settings are enabled, if a user gets screened out with a payable screenout reason, the user will see a screen similar to the one below, referencing the partial reward awarded.

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/partial_reward.png" width="320" height="auto"/>

> **Note:**  Publishers can also specify a minimum Reward in case that they have a minimum reward in place to round up if a price falls below a specific price point

<h2>Performance</h2>

Publishers can review the performance of Payable Screenouts through their Dashboard in the <i>Mediation-Performance</i> area. When payable screenouts happen and are within the filters applied in that view, they can be seen in the funnel events of the relevant graph or table view in that section.

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/dash_pay.png" width="620" height="auto"/>

<h2>Monitoring</h2>

Publishers can monitor real time the conversions on payable screenouts, to reward their users, through the s2s callbacks and local notifications.

<h3>S2S Callbacks</h3>

S2S callbacks are the only secure way for publishers to reward their users. If publishers would like to reward their users on screenouts with payable screenouts, they should enable to get notified on screenouts too (<b>Notify me when the user is not eligible</b>) through their Dashboards in the App Settings area.

<p align="center"><img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/doc_images/s2s_settings_not_eligible.png" width="600" height="auto"/>

When publishers enable the setting to get notified when a user is not eligible, they will be able to start receiving s2s callbacks on screenouts too: 

<ul>
<li>Paybale screenouts will fire with <b>CPA>0</b> and <b>status=noteligible</b></li>
<li>Non payable screenouts (for example due to fraud) will fire with <b>CPA=0</b> and <b>status=noteligible</b></li>
</ul>
  
An example of a callback of a payable screenout can be seen below:

```
https://my-domain.com/my-path?device_id=test_device_id&cpa=2&request_uuid=test_id&timestamp=1614854263963&tx_id=bP7atzvMf1mNcWC3cHc6aAmuY3D&signature=FwAcnySqCUoAxymVaeGBSgXk2E&status=noteligible&reason=screenout&reward_name=Diamonds&reward_value=120
```

> **Note:**  It is important to reward your users only when the relevant CPA and/or reward value are above zero since screenouts can happen also for other reasons too (fraud, quality etc), which are not payable and their CPA will be zero

<h3>Local in-app Callbacks</h3>

Pollfish provides different notifications/callbacks in-app, to inform publishers on different events within the survey flow. 

> **Note:**  Local callbacks can be easily compromised so we strongly suggest publishers to trust only s2s callbacks to reward their users. Local in-app notifications are usually used to adjust the UI of the app while waiting for an s2s callback to verify a conversion.

When Pay on Screenouts feature is enabled:

<ul>
<li>On a successful complete, the relevant Survey Completed local callback will fire with the relevant info around the reward and earnings.</li>
<li>On a payable screenout, the relevant Survey Completed local callback will fire with the relevant info around the reward and earnings.</li>
<li>On a non payable screenout, User Not Eligible local callback will fire </li>
</ul>

> **Note:**  Firing Survey Completed local callbacks on payable screenouts, when the feature is enabled, is not currently supported in the old mobile SDKs. Publishers should update to the latest SDKs (v6) if they would like to rely on the Survey Completed callback on payable screenouts
