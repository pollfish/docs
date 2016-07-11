Step-by-step info to allow integration of Pollfish surveys into B4A apps with the help of inline Java

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.

## Prerequisites


*	Android 10+ using Google Play Services
*	B4A 4.30+


## Integration

* Please follow steps as described in Android Documentation section (Google Play or Universal) to register an account and download Pollfish SDK.
* Add Pollfish SDK and Google Play Services in your B4A project attributes

```
#AdditionalRes: YOUR_PATH\libproject\google-play-services_lib\res, com.google.android.gms
#AdditionalJar: YOUR_PATH\pollfish-googleplay-4.2.1.jar
```

* Call Pollfish relevant functions as described in Android Documentation using Inline Java:
 
```
#If JAVA
import com.pollfish.main.PollFish;
import com.pollfish.main.PollFish.ParamsBuilder;
import com.pollfish.constants.Position;

public void _onResume() {
    PollFish.initWith(this, new ParamsBuilder("YOUR API KEY").build());
}
#End If

```

* Add internet permission in your AndroidManifest.xml file

```
<uses-permission android:name="android.permission.INTERNET"/>
```

* If you need further customizations and options, please have a look at Android Documentation
