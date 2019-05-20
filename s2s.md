
## Server-to-Server postback call for survey completion

### 1. Introduction

#### Server-to-Server postback call for survey completion


You can set a Server-to-Server webhook URL through Pollfish developer dashboard, in your app's page. On every survey completion through your app an HTTP GET request will be made using that URL.

<img src="https://storage.googleapis.com/pollfish-images/s2s_dashboard_o.png">

> **Note:** You should use this call to verify a survey completion if you reward your users. This is the only 100% accurate and secure way to monitor survey completion through your app.

Server-to-server callbacks can be used to retrieve several different params on publisher's server side.

<img src="https://storage.googleapis.com/pollfish-images/s2s_status_form_o.png">

In general, we advice to monitor all these parameters on your server side.

### 2. Testing postback calls in developer mode 

You can test server-to-server callbacks in developer mode. On every survey completion a callback will be fired. In that call a **debug=true** parameter will be appended to indicate that the callback is for a survey completed in developer mode. If your app is turned in release mode, no debug parameter will exist in the call.

For example the following URL template:

```
http://www.example.com/pollfish/[[request_uuid]]?cpa=[[cpa]]
```

could produce a URL in developer mode like the following:

```
http://www.example.com/pollfish/CPMdQdgAzHoL6360iXY5qLp?cpa=30&debug=true
```

### 3. Uniquely identifying a survey completion (avoiding duplicates)

Every user can complete only once a specific survey. You can avoid dublicates in survey completion callbacks by appending and listening to **tx_id** param. This id is calculated by user id and survey id and uniquely identifies a survey completion by a user. A user should not complete the same survey twice. Having that said you should never receive callbacks with the same **tx_id** param. Use this param to avoid crediting a user more than once for the same survey.   


| **Note:** You should always check debug param when verifying a callback. Please ignore debug=true callbacks when rewarding your users in a live app since this can be an indication of a tampered app.

### 4. Passing and retrieving your own unique id of a user through the callback

You can pass a unique id for a user (as you may use it in your own system) through the SDK, during intiialization. You can retrieve this id through the server-to-server callback if you append **request_uuid** parameter to the call.

### 5. Retrieving info around cpa and rewards

#### 5.1 Retrieving CPA value for a given survey

You can easily retrieve through every callback how much money were earned in USD cents, by appending and reading param with name **cpa**.

#### 5.2 Retrieving Reward Name and Reward Value for a given survey

In every callback received, aside from money earned you can retrieve the Reward Name and Reward Value, by appending and reading params with name **reward_name** and/or **reward_value**.

| **Note:** You can set those values per app, through the Publisher Dashboard under section `Reward Settings`

### 6. Getting notified when a user is not eligible

You can register and receive callbacks when a user was not eligible for a survey. User not eligible in that case means that either the user was screened out from a particular survey or he/she was marked as fraud by our anti-fraud system.

If you want to register and receive not eligible/eligible info in your callbacks please select the checkbox as below

<img src="https://storage.googleapis.com/pollfish-images/not_eligible2.png">

Once you select to register for not eligible callbacks, you will need to add "status" in your url. This param will return two values 
```[eligible | noteligible]``` 

<img src="https://storage.googleapis.com/pollfish-images/not_eligible1.png">

For example:

```
 https://mybaseurl.com?device_id=[[device_id]]&cpa=[[cpa]]&request_uuid=[[request_uuid]]&timestamp=[[timestamp]]&tx_id=[[tx_id]]&signature=[[signature]]&status=[[status]]
```

> **Important:** If you have selected checkbox "Notify me when the user is not eligible" you should add "status" param in your url. If you uncheck this option you should remove "status" param from your url.


#### Get informed about the reason a user was not eligible (optional) 
As before, you will need to select the **Notify me when the user is not eligible** checkbox and provide a new parameter for the termination reason called **[[term_reason]]**

For example:

```
 https://mybaseurl.com?device_id=[[device_id]]&cpa=[[cpa]]&request_uuid=[[request_uuid]]&timestamp=[[timestamp]]&tx_id=[[tx_id]]&signature=[[signature]]&status=[[status]]&reason=[[term_reason]]
```
The **[[term_reason]]** value will contain **one** of these strings as the reason

Term reason | Description
------------|------------
quota_full | The quota that the respondent belongs was closed while the user was answering the survey
survey_closed | The survey collected all the desired responses while the user was answering the survey
profiling | The respondent did not match the target audience of the survey
screenout | The respondent choose a non-desired answer in a survey screening question
duplicate | The respondent attempted to answer the same survey twice
security | Generic reason for security and fraud checks
geomissmatch | We identified irregularities in the location data of the respondent
quality | The respondent failed in one of our trap questions or other quality checks
hasty_answers | The respondent completed the survey too fast or used straightlining
gibberish | The respondent answered with gibberish text in at least one open-ended question
captcha | The respondent failed one of our CAPTCHA tests
third_party_termination | Generic reason for terminations that happen in mediation survey providers
 
 > **Important:** These responses might change in the future

### 7. Securing your callback with signature

#### 7.1 How to include a signature in the callback URLs

As with all callback URL parameters, in order to receive values for a parameter you have to include the corresponding parameter placeholder in the URL that you submit to Pollfish. For the **signature** parameter you have to include the **[[signature]]** parameter placeholder. If you do not included it then your callback URLs will not be signed. Because of this the following URL templates will result in not having your callback URLs signed.

```
http://www.example.com/pollfish-callback
http://www.example.com/pollfish-callback?cpa=[[cpa]]&uuid=[[request_uuid]]
```
In addition to the **signature** parameter in order to enable URL signatures you also need to include one more parameter. This is because the signature signs the parameter values and not the URL. So if you specify the below URL template your URLs will not include a signature.

```
http://www.example.com/pollfish-callback?sig=[[signature]]
```
To make sure that your callback URLs are signed include the **signature** parameter plus one other parameter.

**Valid examples:**

```
http://www.example.com/pollfish-callback?tx_id=[[tx_id]]&sig=[[signature]]
http://www.example.com/pollfish-callback?tx_id=[[tx_id]]&time=[[timestamp]]&sig=[[signature]]
http://www.example.com/pollfish-callback?tx_id=[[tx_id]]&time=[[timestamp]]&cpa=[[cpa]]&device=[[device_id]]&request_uuid=[[request_uuid]]&sig=[[signature]]
```

#### 7.2 Effective use of URL signatures

If you want to be protected by fake requests forged by malicious third parties then including the **signature** in your URL is not enough. You must make sure that you include at least one other parameter that varies a lot between requests or is unique between requests. We recommend using at least the **tx_id** parameter in combination with the **signature** parameter to protect against fake callback requests. 

**Bad URL template:**

```
http://www.example.com/pollfish-callback?cpa=[[cpa]]&sig=[[signature]]
```

This is bad because signature only uses **cpa** as input and **cpa** does not vary a lot between requests.

**Good URL template:**

```
http://www.example.com/pollfish-callback?id=[[tx_id]]&sig=[[signature]]
```

This is a good URL template because **tx_id** is unique for all the callback requests that you are going to receive.

**Very good URL template:**

```
http://www.example.com/pollfish-callback?id=[[tx_id]]time=[[timestamp]]&sig=[[signature]]
```

Includes both **tx_id** and **timestamp**.

#### 7.3 How signatures are produced

The **signature** of the callback URLs is the result of appling the  [HMAC-SHA1](https://en.wikipedia.org/wiki/Hash-based_message_authentication_code) hash function to the **[[parameters]]** that are included in the URL using your account's secret_key.

We only sign the values that are substituted using the parameters placeholders (**[[cpa]]**, **[[device_id]]**, **[[request_uuid]]**, **[[status]]** **[[timestamp]]**, **[[tx_id]]** and **[[term_reason]]**). We do not sign any other part of the URL including any other *URL parameters* that the publisher might specify. For example in the below URL only the values that are going to be substituded in **[[request_uuid]]** and **[[tx_id]]** are used as input and not the values of the `bundle_id` and `source` URL parameters.

```
https://www.example.com?request_uuid=[[request_uuid]]&tx_id=[[tx_id]]&signature=[[signature]]&bundle_id=com.domain.app&source=pollfish
```

Your secret_key is an auto-generated key by Pollfish that serves as a shared secret between the publisher and Pollfish. You can find out more about your secret_key at the [Account Information](//www.pollfish.com/dashboard/dev/account/information) page.

To sign the parameters they are assembled in alphabetical order using the parameter placeholder names in a string by concatenating them using the colon ':' character. For example if you have the follwing URL template:

```
https://www.example.com?device_id=[[device_id]]&cpa=[[cpa]]&timestamp=[[timespamp]]&tx_id=[[tx_id]]&signature=[[signature]]
```
Then the produced string, that will be the input to HMAC-SHA1, will have the pattern: `cpa:device_id:timestamp:tx_id`

Furthermore if we have the following values: `device_id=my-device-id`, `cpa=30`, `timestamp=1463152452308` and `tx_id=08f31d41d800cc7a0beb7eb4897639a8ba7fd7db` the string that will be the input to HMAC-SHA1 will be:

```
30:my-device-id:1463152452308:08f31d41d800cc7a0beb7eb4897639a8ba7fd7db
```

and the produced callback URL will be:

```
https://www.example.com?device_id=my-device-id&cpa=30&timestamp=1463152452308&tx_id=08f31d41d800cc7a0beb7eb4897639a8ba7fd7db&signature=BbgBlH5HODk%2FSKw3MQuvqM%2BgTxQ%3D
```

Please note that the string is created using the parameter values before they are URL encoded.

#### 7.4 How to verify signatures

To verify the signature in server-to-server postback calls follow the below proceedure:

1. Extract the value of the **signature** parameter from the URL.
2. URL decode the value you extracted in (1) using [Percent encoding](https://en.wikipedia.org/wiki/Percent-encoding)
3. Extract the values of the rest of the parameters URL.
4. URL decode the values you extracted in (3) using Percent encoding.
5. Sort the values from (4) alphabeticaly using the names of the template parameters. The names of the template parameters in sorted order are: `cpa`, `device_id`, `request_uuid`, `status`, `term_reason`, `timestamp`, `tx_id` and not the names of any [URL parameters](https://en.wikipedia.org/wiki/Query_string) your URL may contain.
6. Produce a string by concatenating all non-empty parameter values as sorted in the previous step using the `:` character. The only parameter that when specified in the URL template can be empty is `request_uuid`. There is a special handling for `term_reason`: If the user is non-eligible then it has one of the values described in section 6 and with that value is included in the callback url and the signature calculation. If however the user is eligible the term is included but with an empty value and must participate in the signature calculation. An example of a callback url for an eligible user is `https://mybaseurl.com?device_id=my-device-id&term_reason=&cpa=30` which gives the string `my-device-id:30:` for signature calculation. The trailing `:` is because of the empty `term_reason`
7. Sign the string produced in (6) using the [HMAC-SHA1](https://en.wikipedia.org/wiki/Hash-based_message_authentication_code) algorithm and your account's **secret_key** that can be retrieved from the [Account Information](https://www.pollfish.com/dashboard/dev/account) page.
8. Encode the value produced in (7) using [Base64](https://en.wikipedia.org/wiki/Base64)
9. Compare the values produced in (2) and (8). If they are equal then the signature is valid.

Please note that during developer mode the `debug=true` parameter is *not included* in the input of the signature.

#### 7.5 Example code for signature verification

```php
<!DOCTYPE html>
<html>
<head>
  <title>Pollfish s2s signature validator example</title>
</head>
<body>

<h1>Validate signature</h1>

<p>Url pattern is: <code>https://example.com?device_id=[[device_id]]]&amp;cpa=[[cpa]]&amp;timestamp=[[timstamp]]&amp;tx_id=[[tx_id]]&amp;request_uuid=[[request_uuid]]&amp;status=[[status]]&amp;signature=[[signature]]</code></p>

<?php $secret_key = "my-secret"; ?>

<p>Will check signature using HMAC-SHA1 and secret_key = <br><?php echo($secret_key) ?></b></p>

<?php
  $cpa = rawurldecode($_GET["cpa"]);
  $device_id = rawurldecode($_GET["device_id"]);
  $request_uuid = rawurldecode($_GET["request_uuid"]);
  $status = rawurldecode($_GET["status"]);
  $timestamp = rawurldecode($_GET["timestamp"]);
  $tx_id = rawurldecode($_GET["tx_id"]);
  $url_signature = rawurldecode($_GET["signature"]);

  $data = $cpa . ":" . $device_id;
  if (!empty($request_uuid)) { // only added when non-empty
    $data = $data . ":" . $request_uuid;
  }
  $data = $data . ":" . $status . ":" . $timestamp . ":" . $tx_id;

  $computed_signature = base64_encode(hash_hmac("sha1" , $data, $secret_key, true));
  $is_valid = $url_signature == $computed_signature;
?>

<p>cpa = <?php echo($cpa); ?></p>
<p>device_id = <?php echo($device_id); ?></p>
<p>request_uuid = <?php echo($request_uuid); ?></p>
<p>status = <?php echo($status); ?></p>
<p>timestamp = <?php echo($timestamp); ?></p>
<p>tx_id = <?php echo($tx_id); ?></p>

<p>The signature is generated using the input string:<code><?php echo($data); ?></code></p>

<p>The generated signature is: <?php echo($computed_signature); ?></p>
<p>The URL signature is: <?php echo($url_signature); ?></p>
<p>The signature is valid: <?php echo($is_valid ? "true" : "false"); ?></p>

</body>
</html>
```

### 8. Checking callback logs

You can check logs from your s2s callbacks history simply by selecting the relevant button on your Dashboard.

<img src="https://storage.googleapis.com/pollfish-images/show_logs.png">

In that popup you will find all callbacks generated from Pollfish servers for your app, sorted by date. You can easily track the status of each call and response from you server side. Each call in the logs is clickable and you can also search for a specific callback based on specific params of your url structure.


