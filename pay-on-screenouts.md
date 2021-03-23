<h1>Pay on Screenouts</h1>


Pay on Screenouts is a feature provided by Pollfish in order to allow our partners to have more predictable revenue. This feature aims to overcome Market Research monetization limitations where users can get screened out from a survey and not get a reward even if they are looking to complete one. 

With focus on providing an optimal user experience and ensuring revenue in every session, partners can enable Pay on Screenouts feature per mediation network through their Dashboard. Pay on Screenouts feature distributes in a more fair way, revenue from surveys in every session with a compromise in the payout in survey completion. Therefore no minimum payouts or price floors are applied in that case.

**Note:** <i>Payable screenouts are screenouts that happened because the user got screened out for different reasons such as Profiling, Screen Out on a screening question, Quota full, survey closed and others. Screen-outs due to fraud, quality, vpn or security are not payable. </i>

**Note:** <i>Payable screenouts are disabled by default in all new apps.</i>

<h2>Activating Pay on Screenouts</h2>

Publishers can visit their Dashboard in the Settings-Mediation Settings area and enable or disable “Pay on Screenouts” feature per Mediation Network per App and clicking Apply. 



In the same section the publisher can  review the current rates on payments for completes or screenouts if the relevant feature is enabled. 

Note: Keep in mind that prices shared in this section are just informative and reflect the prices seen on the platform the previous minutes.

Note: Activating pay on screenouts might result to lower inventory due to limitations
User Experience

If you would like to deliver a reward for your users on screenouts and prompt them within the survey you should enable Reward Settings depending on your integration approach in the Settings-App Settings area of your app.



In that section you can specify the reward name and a relevant exchange rate. When you enable those if a user gets screened out with a payable reason he will see a screen similar to the one below, referencing the partial reward provided.




Note: Publishers can also specify a minimum Reward in case that they have a minimum reward in place to round up if a price falls below a specific price point
Performance

Publishers can review the performance of Payable Screenouts through their Dashboard in the Mediation-Settings area. When payable screenouts happen in the relevant filters applied, can be seen in the funnel events in the relevant graph or table view


Monitoring
Publishers can monitor real time the conversions on payable screenouts to reward their users, through the s2s callbacks and local notifications.
S2S Callbacks

S2S callbacks are the only secure way for publishers to reward their users. If publishers would like to reward their users on screenouts with payable screenouts, they should enable to get notified on screen-outs too (notify me when the user is not eligible) through their Dashboards in the App Settings area.




When publishers do that they will be able to start receiving callbacks on screenouts too but with CPA>0 (which refer to payable screenouts)

An example of a callback of a payable screen-out can be seen below:

https://my-domain.com/my-path?device_id=test_device_id&cpa=2&request_uuid=test_id&timestamp=1614854263963&tx_id=bP7atzvMf1mNcWC3cHc6aAmuY3D&signature=FwAcnySqCUoAxymVaeGBSgXk2E&status=noteligible&reason=screenout&reward_name=Diamonds&reward_value=120

It is important to reward your users only when the relevant CPA and/or reward value are above zero since screenouts can happen also for other reasons (fraud, quality etc) which are not payable and their CPA will be zero

Local in-app callbacks

Pollfish provides different notifications/callbacks in-app to inform publishers on different events of the survey flow. Local notifications can be easily compromised so we strongly suggest publishers to trust only s2s callbacks to reward their users. Local in-app notifications are usually used to adjust the UI of the app while waiting for an s2s callback to verify a conversion.


When Pay on Screenouts feature is enabled on a successful complete the relevant Survey Completed notifications are fired. 

In case of a Payable Screen-out when the relevant feature is enabled, Survey completed local notification will fire with the relevant info. For other screenouts, User not Eligible callbacks will fire as expected.

Note: It’s important to have Reward Settings enabled on the dashboard for the feature to operate properly

Note: Firing Survey Completed local notifications on Payable Screenouts is not currently supported in the mobile SDKs.
