## Demographic Surveys

When a user is first introduced to the platform, if no paying surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure to our clients' survey inventory. This survey returns no payment to app publishers, as it is part of the process users need to go through in order to join the platform. Bear in mind that if a paid survey is available at that point in time, the demographic questions will be inserted at the beginning of the paying survey, before the actual survey questions.

Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this new type of targeting.

 
You can see an example of how we use this info on our targeting page of the DIY survey tool below:

![alt text](https://pollfish.zendesk.com/hc/article_attachments/208100469/targeting.png)

and in our Results page:

![alt text](https://pollfish.zendesk.com/hc/article_attachments/208100489/results.png)

<b>Publishers have the power</b>

In our efforts to include publishers in this process and be as transparent as possible, we are providing full control over the process. We are letting publishers decide whether their users are served these standalone surveys or not in three ways:

1) By monitoring the process in code and excluding any users by listening to the relevant notifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Bear in mind that by filtering out all surveys with PPS 0 will also stop all free internal surveys, since they also have a PPS of 0.

2) By providing an option to disable Standalone Demographic Surveys through the Settings section of an app on Pollfish Developer Dashboard, without the need to make any changes in code. (Changes are effective immediately.)

![alt text](https://pollfish.zendesk.com/hc/en-us/article_attachments/208795189/receiving.png)

3) By submitting known user attributes like gender or age, during initialization in code, you may skip some or all of the questions in our Demographic surveys.  Bear in mind, that you need to contact our Support Department to ask them to acknowledge the information you have provided.


If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and also achieve a better fill rate and higher priced surveys.

Below you can find the list of demographic info you can send over along with the relevant keys and mappings

![alt text](https://storage.googleapis.com/pollfish-images/demographic.png)

| **Note:** Both key and values should be eventually converted to strings prior sending over through the relevant functions within the library

### Mappings

![alt text](https://storage.googleapis.com/pollfish-images/gender.png)


