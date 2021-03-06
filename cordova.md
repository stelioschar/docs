Cordova/PhoneGap plugin to allow integration of Pollfish surveys into Android and iOS apps. 

Pollfish is a mobile monetization platform delivering surveys instead of ads through mobile apps. Developers get paid per completed surveys through their apps.

## Prerequisites


*	Android 10+ using Google Play Services
*	iOS version 9.0+
*	Apache Cordova v3.0.4+
* Android<7 (there is a known issue at the moment with android 7 so you will need to downgrade to use the plugin to android 6.4.0)

```sudo cordova platform add android@6.4.0```

## Quick Guide

* Create Pollfish developer account, create new app and grap it's API key
* Install Pollfish plugin and call init function
* Set to Release mode and release in Store
* Update your app's privacy policy
* Request your account to get verified from Pollfish Dashboard


![alt tag](https://www.pollfish.com/homeassets/images/rocketMobile.png)

## Steps Analytically

### 1. Obtain a Developer Account

Register as a Developer at [www.pollfish.com](http://www.pollfish.com)

### 2. Add new app in Pollfish panel and copy the given API Key

Login at [www.pollfish.com](http://www.pollfish.com) and add a new app at Pollfish panel in section My Apps and copy the given API key for this app to use later in your init function in your app.

### 3. Installing the plugin

To add Pollfish plugin just type:

```
cordova plugin add https://github.com/pollfish/cordova-plugin-pollfish.git
```

To remove Pollfish plugin type:

```
cordova plugin remove com.pollfish.cordova
```



*In iOS if pollfish framework is not added automatically you may need to add it manually to your XCode project. In Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location (located in /src/ios/framework) and select it. The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane). The framework is a folder and you should add the whole folder into your project.*




### 4. Initialize Pollfish

Init function takes the following parameters:

1.	**debugMode**: - Choose Debug or Release Mode
2.	**customMode**: - Init or custom init
3.	**api_key**: - Your API Key (from step 2)
4.	**pos**: - The Position where you wish to place the Pollfish indicator. There are four different options {Position.TOP_LEFT, Position.BOTTOM_LEFT, Position.MIDDLE_LEFT, Position.TOP_RIGHT, Position.BOTTOM_RIGHT, Position.MIDDLE_RIGHT}
5.	**padding**: - The padding (in dp) from top or bottom according to Position of the indicator specified before (0 is the default value – |*if used in MIDDLE position, padding is calculating from top).

For example:

```
var debugMode = true;
var customMode = false;
var api_key = "YOUR_API_KEY";
var pos=pollfishplugin.Position.TOP_LEFT;
var padding = 50;
 
pollfishplugin.init (debugMode,customMode,api_key,pos,padding);
```

#### Debug Vs Release Mode

You can use Pollfish either in Debug or in Release mode. 
  
* **Debug mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).
* **Release mode** is the mode to be used for a released app (start receiving paid surveys).


**Note: In Android debugMode parameter is ignored. Your app turns into debug mode once it is signed with a debug key. If you sign your app with a release key it automatically turns into Release mode.**

**Note: Be careful to turn the debugMode parameter to false when you release your app in a relevant app store!!**



#### init Vs custom init

*	**init function** is the standard way of using Pollfish in your apps. Using init function enables controlling the behavior of Pollfish in an app from Pollfish panel.

*	**custom init function** ignores Pollfish behavior from Pollfish panel. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish view to app users. This method is usually used when app developers want to incentivize first somehow their users before completing surveys to increase completion rates. Both init and customInit functions have the same arguments.

#### 4.1 Other Init functions (optional)

##### Passing custom parameter for server to server postback calls

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function within the SDK and receive it back with Server to Server, survey completed postback call you can use

For example:

```
var debugMode = true;
var customMode = false;
var api_key = "YOUR_API_KEY";
var pos=pollfishplugin.Position.TOP_LEFT;
var padding = 50;
var requestUUID = "my_uuid";

pollfishplugin.initWithRequestUUID (debugMode,customMode,api_key,pos,padding,requestUUID);
```

### 5. Update your Privacy Policy

#### Add the following paragraph to your app's privacy policy


*Survey Serving Technology*

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone)  is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*


*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THE DRAWS. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.*


---
<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

If you have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>
<br/><br/><br/>

| **Note:** Please bear in mind that the first time a user is introduced to the platform, when no paid surveys are available, a standalone demographic survey will be shown, as a way to increase the user's exposure in our clients' survey inventory. This survey returns no payment to app publishers, since it is part of the process users need to go through in order to join the platform. Bear in mind that if a paid survey is available at that point of time, the demographic questions will be inserted at the begining of the survey, before the actual survey questions. Our aim is to provide advanced targeting solutions to our customers and to do that we need to have this information on the available users. Targeting by marital status or education etc. are highly popular options in the survey world and we need to keep up with the market. A vast majority of our clients are looking for this option when using the platform. Based on previous data, over 80% of the surveys designed on the platform require this new type of targeting.

<br/>

<table style="border:0 !important;">
<tr>
<td><img src="https://storage.googleapis.com/pollfish-images/targeting.png" style="padding:4px"/></td>
<td><img src="https://storage.googleapis.com/pollfish-images/results.png" style="padding:4px"/></td>
</tr>
</table>
<br/>


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://pollfish.zendesk.com/hc/en-us/articles/213287545">here</a>. 


<br/>

### 6\.  Request your account to get verified

After your app is published on an app store you should request your account to get verified from your Pollfish Developer Dashboard.

<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/account.png"/>
<br/>

When your account is verified you will be able to start receiving paid surveys from Pollfish clients.
<br/>
<br/>
<br/>



## Optional section

In this section we will list several options that can be used to control Pollfish surveys behaviour, how to listen to several notifications or how be eligible to more targeted (high-paid) surveys. All these steps are optional.
<br/>
<br/>



### 7. Handling orientation changes (optional)

If your app supports both orientations you should listen for the orientation event and initialise Pollfish again.

For example:

```
document.addEventListener("orientationchange", app.updateOrientation,false);
```

```
updateOrientation: function () {
    pollfishplugin.init (debugmode,customMode,api_key,pos,padding);
}
```

### 8. Handling application entering to foreground (optional)

You should handle the event when your app is entering to foreground in order to initialise Pollfish again by listening to the relevant event.

For example:

```
document.addEventListener("resume", app.onResume, false);
```

```
onResume: function () {
    pollfishplugin.init (debugmode,customMode,api_key,pos,padding);
}
```


### 9. Implement Pollfish event listeners (optional)

#### 9.1 Get notified when a Pollfish survey is received (optional)

You can be notified when a Pollfish survey is received.

For example:

```
pollfishplugin.setEventCallback('onPollfishSurveyReceived',app.surveyReceivedEvent);
```

```
surveyReceivedEvent: function(id) {

try{
   console.log("Pollfish Survey Received - playfulSurveys: " + id.playfulSurveys + " surveyPrice: " + id.surveyPrice);
 }catch(e){}
}
```

#### 9.2 Get notified when a Pollfish survey is completed (optional)

You can be notified when a Pollfish survey is completed.

For example:

```
pollfishplugin.setEventCallback('onPollfishSurveyCompleted',app.surveyCompletedEvent);
```

```
surveyCompletedEvent: function(id) {

try{
   console.log("Pollfish Survey Completed - playfulSurveys: " + id.playfulSurveys + " surveyPrice: " + id.surveyPrice);
 }catch(e){}
}
```

#### 9.3 Get notified when a user is not eligible for a Pollfish survey (optional)

You can be notified when a user is not eligible for a Pollfish survey.

For example:

```
pollfishplugin.setEventCallback('onPollfishUserNotEligible',app.userNotEligibleEvent);
```

```
userNotEligibleEvent: function(id) {
 console.log("Pollfish User Not Eligible");
}
```

#### 9.4 Get notified when a Pollfish survey is not available (optional)

You can be notified when a Pollfish survey is not available

For example:

```
pollfishplugin.setEventCallback('onPollfishSurveyNotAvailable',app.surveyNotAvailableEvent);
```

```
surveyNotAvailableEvent: function(id) {
 console.log("Pollfish Survey not available");
}
```

#### 9.5 Get notified when a Pollfish survey panel is open (optional)

You can be notified when Pollfish survey panel is open

For example:

```
pollfishplugin.setEventCallback('onPollfishOpened',app.pollfishPanelOpenEvent);
```

```
pollfishPanelOpenEvent: function(id) {
 console.log("Pollfish Survey panel is open");
}
```

#### 9.6 Get notified when a Pollfish survey panel is closed (optional)

You can be notified when Pollfish survey panel is closed

For example:

```
pollfishplugin.setEventCallback('onPollfishOpened',app.pollfishPanelClosedEvent);
```

```
pollfishPanelClosedEvent: function(id) {
 console.log("Pollfish Survey panel is closed");
}
```

### 10. Manually show/hide Pollfish panel (optional)

You can manually hide and show Pollfish from your various UIVIewControllers. by calling anywhere after initialization: 

For example:

```
pollfishplugin.showPollfish();
```

or

```
pollfishplugin.hidePollfish();
```

### 11. Set user attributes (optional)

You can set attributes that you receive from your app regarding a user in order to receive a better fill rate and higher priced surveys. 

For example:

```
var userAttributes = {};

userAttributes['FacebookID'] = 'My Facebook';
userAttributes['LinkedInID'] = 'My LinkedIn';

pollfishplugin.setAttributesMap(userAttributes);

```


## Example

If you want to have a look at sample code on how you can call and use Pollfish plugin in your app, you can a review files located at test/index.js and test/index.html


## More Info

For more information on setting up Cordova see [the documentation](http://cordova.apache.org/docs/en/latest/guide/cli/index.html)

