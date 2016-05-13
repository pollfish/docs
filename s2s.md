
##Server-to-Server postback call for survey completion

You can set a Server-to-Server postback call through Pollfish developer dashboard. This call will be fired on every survey completion. 

<img src="https://storage.googleapis.com/pollfish-images/s2s.png">

> **Note:** You should use this call to verify a survey completion if you reward your users. This is the only 100% accurate and secure way to monitor survey completion through an app.

Server-to-server callbacks can be used to retrieve several different params on publisher's server side.

<img src="https://pollfish.zendesk.com/hc/en-us/article_attachments/201860351/Screen_Shot_2015-08-19_at_1.30.21_PM.png">

###  Testing postback calls in developer mode 

You can test server-to-server callbacks in developer mode. On every survey completion a callback will fire. In that call a **debug=true** parameter will be appended to indicate that the callback is for a survey completed in developer mode. If testing in release mode no debug parameter will exist in the call.

### Uniquely identifying a survey completion (avoiding duplicates)

You can avoid doublicates in survey completion callbacks by appending and listeing to **tx_id** param. This id is calculated by user id and survey id and uniquely identifies a survey completion by a user. A user should not complete the same survey twice. Having that said you should never receive callbacks with the same **tx_id** param. Use this param to avoid crediting the user more than once for the same survey.   

### Passing a unique id of a user (as used in a third party system) in callback

You can pass a unique id for a user through the sdk during intiialization. You can retrieve this is through the server-to-server callback if you append **request_uuid** parameter

### Callback URL signatures

#### How to include a signature in the callback URLs

As with all callback URL parameters, in order to receive values for a parameter you have to include the corresponding parameter placeholder in the URL that you submit to Pollfish. For the **signature** parameter you have to include the **[[signature]]** parameter placeholder. If you do not included it then your callback URLs will not be signed. Because of this the following URL templates will result in not having your callback URLS signed.

```
http://www.example.com/pollfish-callback
http://www.example.com/pollfish-callback?cpa=[[cpa]]&uuid=[[request_uuid]]
```
In addition to the **[[signature]]** parameter in order to enable URL signatures you also need to include one more parameter. This is because the signature signs the parameter values and not the URL. So if you specify the below URL template your URLs will not include a signature.

```
http://www.example.com/pollfish-callback?sig=[[signature]]
```
To make sure that your callback URLs are signed include the **[[signature]]** parameter plus one other parameter.

**Valid examples:**

```
http://www.example.com/pollfish-callback?tx_id=[[tx_id]&sig=[[signature]]
http://www.example.com/pollfish-callback?tx_id=[[tx_id]&time=[[timestamp]]&sig=[[signature]]
http://www.example.com/pollfish-callback?tx_id=[[tx_id]&time=[[timestamp]]&cpa=[[cpa]]&device=[[device_id]]&request_uuid=[[request_uuid]]&sig=[[signature]]
```

#### Effective use of URL signatures

If you want to be protected by fake requests forged by malicious third parties then including the **[[signature]]** in your URL is not enough. You must make sure that you include at least one other parameter that varies a lot between requests or is unique between requests. We recommend using at least the **[[tx_id]]** parameter in combination with the **[[signature]]** parameter to protect against fake callback requests. 

**Bad URL template:**

```
http://www.example.com/pollfish-callback?cpa=[[cpa]]&sig=[[signature]]
```

This is bad because signature only uses **[[cpa]]** as input and **[[cpa]]** does not vary a lot between requests.

**Good URL template:**

```
http://www.example.com/pollfish-callback?id=[[tx_id]]&sig=[[signature]]
```

This is a good URL template because **[[tx_id]]** is unique for all the callback requests that you are going to receive.

**Very good URL template:**

```
http://www.example.com/pollfish-callback?id=[[tx_id]]time=[[timestamp]]&sig=[[signature]]
```

Includes both **[[tx_id]]** and **[[timestamp]]**.

#### How signatures are produced.

The **signature** of the callback URLs is the result of appling the HMAC-SHA1 hash function to the parameters that are included in the URL using your account's secret_key.

Your secret_key is an auto-generated key by Pollfish that serves as a shared secret between the publisher and Pollfish. You can find out more about your secret_key at the [Account Information](//www.pollfish.com/dashboard/account) page.

To sign the parameters they are assembled in alphabetical order using the parameter placeholder names in a string by concatenating them using the colon ':' character. For example if you have the follwing URL template:

```
https://www.example.com?device_id=[[device_id]]&cpa=[[cpa]]&timestamp=[[timespamp]]&tx_id=[[timestamp]]&signature=[[signature]]
```
Then the produced string, that will be the input to HMAC-SHA1, will have the pattern: **"[[cpa]]:[[device_id]]:[[timestamp]]:[[tx_id]]"**

Furthermore if we have the following values: **device_id=my-device-id, cpa=30,timestamp=1463152452308** and **tx_id=08f31d41d800cc7a0beb7eb4897639a8ba7fd7db** the string that will be the input to HMAC-SHA1 will be:

```
"30:my-device-id:1463152452308:08f31d41d800cc7a0beb7eb4897639a8ba7fd7db"
```

and the produced callback URL will be:

```
https://www.example.com?device_id=my-device-id&cpa=30&timestamp=1463152452308&tx_id=08f31d41d800cc7a0beb7eb4897639a8ba7fd7db&signature=3493ed0af36198c5c4a30ec531542b888cd84106
```

Please note that the string is created using the parameter values before they are URL encoded.
