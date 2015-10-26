## Quick Guide

1.  Create the pollfishConfig object to setup Pollfish library
2.  Include jQuery library to your website (version 1.4.3 and above)
3.  Include Pollfish library to your website

Pollfish library works with IE 10 and above, Chrome 16 and above, Firefox 20 and above.
You can checkout the Pollfish Webplugin experience by visiting this page [here](/webplugin).

## Requirements

- jQuery version 1.4.3 and above

### Developer Vs Release Mode

You can use Pollfish either in Developer or in Release mode.  

*   Developer mode is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
*   Release mode is the mode to be used for a released app in a live online website(start receiving paid surveys).

If you **do not set the debug parameter in your Pollfish config object**, Pollfish runs in release mode by default so it is **IMPORTANT** when you are in development that **YOU MUST** set debug to true in order to be able to receive development surveys.  

**Note: Be careful to turn the debug parameter to false when you put your website online!!**

## Steps Analytically

### 1\. Obtain a Developer Account in Pollfish

Register at [www.pollfish.com](//www.pollfish.com) as a Developer.

### 2\. Add new app in Pollfish panel and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com) and add a new app at Pollfish panel in section My Apps and copy the given API key for this app to use later in your pollfishConfig object in your app.

### 3\. Set up the pollfishConfig object

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  debug: true
};
```

**IMPORTANT: Pollfish will autostart serving surveys once the polfishConfig object is set, with a valid api key.**

#### pollfishConfig object takes the following parameters:

1.  <span class="params">api_key (required)</span>  
    Your API Key (from step 2)
2.  <span class="params">indicator_position (optional)</span>  
    The Position where you wish to place the Pollfish indicator.  
    There are four different positions: {TOP_LEFT, BOTTOM_LEFT, TOP_RIGHT, BOTTOM_RIGHT}  
    Defaults to BOTTOM_RIGHT
3.  <span class="params">debug (optional)</span>  
    Sets Pollfish in debug mode  
    Set true to enable debug mode (for development), set false to set Pollfish in release mode.  
    Defaults to false
4.  <span class="params">uuid (optional)</span>  
    Uuid for callback to your server

Below you can see an example of the pollfishConfig object:  

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  indicator_position: "BOTTOM_RIGHT",
  debug: true,
  uuid: "string_uuid"
};
```

### Other pollfishConfig object callback options (optional)

Pollfish Webplugin provides some callback functions to call when specific actions are executed in the Pollfish survey.

#### pollfishConfig object takes the following optional callback function parameters:

1.  <span class="params">closeCallback</span>  
    Called when user clicks or touches outside the Pollfish survey container, or if he clicks or touches the close icon
2.  <span class="params">userNotEligibleCallback</span>  
    Called when the user is not eligible for surveys
3.  <span class="params">closeAndNoShowCallback</span>  
    Called when the survey is closed and the indicator hides permanently (e.g. when finishing the survey)
4.  <span class="params">surveyCompletedCallback</span>  
    Called when the user finishes the survey
5.  <span class="params">surveyAvailable</span>  
    Called when there is an availble survey for the user

Below you can see an example of the pollfishConfig object with all possible callbacks:  

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  indicator_position: "BOTTOM_RIGHT",
  debug: true,
  uuid: "string_uuid"
  closeCallback: surveyClosed,
  userNotEligibleCallback: customUserNotEligible,
  closeAndNoShowCallback: customCloseAndNoShow,
  surveyCompletedCallback: customSurveyFinished,
  surveyAvailable: surveyAvailable
};

function customSurveyClosed(){
  console.log("user closed the survey");
}

function customUserNotEligible(){
  console.log("user is not eligible");
}

function customSurveyFinished(){
  console.log("user finished the survey");
}

function customCloseAndNoShow(){
  console.log("close and hide the indicator");
}

function surveyAvailable(){
  console.log("there is an available survey");
}
```

### 4\. Include the necessary files in your website

Include the jQuery library with version greater or equal than 1.4.3 if it's not already included, as the example below:

```html
<!-- Include jQuery library >= 1.4.3 version -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
```

Then include the Pollfish Webplugin, as the example below:

```html
<!-- Include Pollfish Webplugin -->
<script src="https://storage.googleapis.com/pollfish_production/sdk/webplugin/pollfish.min.js"></script>
```

**IMPORTANT: Keep in mind that you should include the Pollfish Webplugin after the pollfishConfig object, like the example below:**

```html
<!-- Initialize your pollfishConfig object first -->
<script>
  var pollfishConfig = {
    api_key: "api_key_goes_here",
    debug: true
  };
</script>

<!-- Then include Pollfish Webplugin -->
<script src="https://storage.googleapis.com/pollfish_production/sdk/webplugin/pollfish.min.js"></script>
```

### 5\. Launch Pollfish Webplugin explicitly

You can trigger Pollfish Webplugin explicitly at any given moment and ignore the autostart functionality. In order to ignore autostart, you need to set the ready optional callback function on the pollfishConfig object, as the example below:

```js
var pollfishConfig = {
  api_key: "api_key_goes_here",
  debug: true,
  ready: pollfishReady
};

function pollfishReady(){
  //Pollfish Webplugin is ready, so you can call it excplicitly using the Pollfish.showIndicator or Pollfish.showFullSurvey functions
}
```

After the ready callback is called, you can either show the indicator or open the full survey panel, as described in the next section.

### 6\. Show & hide Pollfish Webplugin explicitly

**Show the Pollfish Indicator that the user has to click in order to see the full survey**  

```js
Pollfish.showIndicator();
```

**Show the full survey so that the user can respond immediately**  

```js
Pollfish.showFullSurvey();
```

_If you call Pollfish.showIndicator or Pollfish.showFullSurvey and there is no available survey, they will return false._

**Hide the indicator and the full survey**  

```js
Pollfish.hide();
```

## Update your Privacy Policy

### Add the following paragraph to your app's privacy policy

“This website uses Pollfish web plugin. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones and website owners in order to have access to users of such applications/websites and address survey questionnaires to them. This website uses and enables Pollfish cookies. When a user connects to this website, Pollfish detects whether the user is eligible for a survey. Data collected by Pollfish will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. For a full list of data received by Pollfish through this website, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. By using this website you accept this privacy policy document and you hereby give your explicit consent for the placement of a Pollfish cookie in your system and the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website or by disabling “third party cookies” from your browser’s settings. We once more invite you to check the Pollfish respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works works.  

APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”

## Privacy Policy

“We invite you to check and comply with the respondent’s terms of use. Pollfish webplugin uses cookies to uniquely and anonymously identify users.  

APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THE DRAWS. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”

