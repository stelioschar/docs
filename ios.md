<div class="changelog" data-version="4.4.0">
v4.4.0

- Added support for iOS 12
- New iOS minimum is 9.0
- Added dependency on WebKit.framework
- Added the ability to render surveys from Mediation within the app
- Added notification for user rejecting a survey
- Improved performance
- Fixed bugs


v4.3.5

- Added ability to test survey formats in debug mode

v4.3.4

- Deprecated destroy function
- Added dynamic caching
- Drastically decreased sdk size
- Updated Pollfish indicator
- Improved performance
- Fixed memory leaks
- XCode 9 support (required)

v4.2.4

- Fixed bitcode issue

v4.2.3

- Added support for sending user attributes during init
- Deprecated setAttributeDictionary function
- Fixed bug for multiple notifications and url encoding
- Fixed isPollfishPresent bug

v4.2.2

- Fixed bug on survey view

v4.2.1

- ATS compliance
- improved performance

v4.2.0

- Fixed bitcode issue
- New API functions to support beacon and location relevant surveys 
- Added support for new type of questions in surveys, including video surveys
- Added new framework dependency (SystemConfiguration.framework)

v4.1.2

- Fixed ARM64 issue


v4.1.1

- support Bitcode
- support Xcode 7

v4.1.0

- Fixed bug on orientation changes
- Converted lib to ARC

v4.0.3

- Fixed bug in init function with Request UUID in release mode

v4.0.2

- Weak link of AdSupport framework
- Added init function with option to pass a custom param and receive it on server-to-server callback
- Added UserAttributesDictionary class for passing attributes around user
- Added various bug fixes and optimizations

v4.0.1

- Added support of circle questions
- Added various bug fixes and optimizations

v4.0.0

- Added various bug fixes and optimizations
</div>

## Quick Guide

1.  Download Pollfish iOS SDK and unzip it
2.  Import pollfish.framework to your project
3.  Import AdSupport.framework, SystemConfiguration.framework, WebKit.framework and CoreTelephony.framework to your project
4.  Call init function of Pollfish in the App’s Delegate
5.  Set to **Release mode** and release in AppStore
6.  Update your privacy policy
7.  Request your account to get verified from Pollfish Dashboard

**or** 

Through CocoaPods:
---

1.  Add a Podfile with Pollfish framework as a pod reference:

```
platform :ios, '9.0'
pod 'Pollfish'
```

You can find latest Pollfish iOS SDK version on CocoaPods [here](https://cocoapods.org/pods/Pollfish)  

2. Run **pod install** on the command line to install  Pollfish cocoapod.
3. Call init function of Pollfish in the App’s Delegate
4. Set to **Release mode** and release in AppStore
5. Update your privacy policy
6. Request your account to get verified from Pollfish Dashboard
<br/>
> **Requirements:** Pollfish framework works with iOS version 9.0 and above and XCode9.  

<br/><br/>

## Steps Analytically

### 1. Obtain a Developer Account

Register at [www.pollfish.com](//www.pollfish.com/login/publisher)

### 2. Add new app on Pollfish Developer Dashboard and copy the given API Key

Login at [www.pollfish.com](//www.pollfish.com/login/publisher) and click "Add a new app" on Pollfish Developer Dashboard in section "My Apps". Copy then the given API key for this app in order to use later on, when initializing Pollfish within your code.


### 3\. Add Pollfish framework to your project

Download Pollfish iOS SDK from the website and then in Xcode, select the target that you want to use and in the Build Phases tab expand the Link Binary With Libraries section. Press the + button, and press Add other… In the dialog box that appears, go to the Pollfish framework’s location and select it.  

The project will appear at the top of the Link Binary With Libraries section and will also be added to your project files (left-hand pane).  

**Note: The framework is a folder and you should add the whole folder into your project.**

### 4\. Add the following frameworks (if you don’t already have them) in your project

- AdSupport.framework  
- CoreTelephony.framework
- SystemConfiguration.framework 
- WebKit.framework (added in Pollfish v4.4.0)

**Note: If your deployment target is less than iOS 7.0, change the AdSupport.framework from Required to Optional.**

<br/>

### or skip steps 3\. and 4\. and go through CocoaPods

Add a Podfile with Pollfish framework as a pod reference:

```
platform :ios, '9.0'
pod 'Pollfish'
```

You can find latest Pollfish iOS SDK version on CocoaPods [here](https://cocoapods.org/pods/Pollfish)  

Run **pod install** on the command line to install  Pollfish cocoapod.

<br/>


### 5\. Embedding Pollfish into your code

<br/>

### 5.1 Import Pollfish header

You have to include Pollfish library headers in any file that you will use Pollfish.  

```
#import <Pollfish/Pollfish.h>
```



### or if you are using Pollfish in a Swift project follow the next steps to import Pollfish

 <span style="text-decoration: underline">Add a Bridging-Header file:</span>
 
**1\. Right-click your project and choose “New File…”** 

<img src="/homeassets/images/documentation/NewFile.png" width="220">

**2\. Choose iOS->Source->Header File->Next**

<img src="/homeassets/images/documentation/NewHeaderFile.png" width="220">


**3\. Name new file "\<Your-Product\>-Bridging-Header.h”**

<img src="/homeassets/images/documentation/BridgingHeader.png" width="220">

where <Your-Product> must be your "Product Name" as listed in your "Build Settings"

<img src="/homeassets/images/documentation/ProductName.png" width="600">

**4\. Declare your new Bridging Header File path in your project's "Build Settings" in row "Objective-C "Bridging Header" section**

<img src="/homeassets/images/documentation/Bridging.png" width="600">

**5\. Import in your Bridging Header file Pollfish header files:**

```
#import <Pollfish/Pollfish.h>
```
<br/>
### 5.2 Initializing Pollfish in App Delegate

The init function of Pollfish must be called in your application’s delegate applicationDidBecomeActive method. This way it is ensured that Pollfish surveys will be refreshed each time your application will become active.  



<span style="text-decoration: underline">Objective-C:</span>
 
```
- (void)applicationDidBecomeActive:(UIApplication *)application
{
  [Pollfish initAtPosition: (PollfishPosition)
               withPadding: (int)
	       andDeveloperKey: (NSString *)
             andDebuggable: (BOOL) 
	         andCustomMode: (BOOL)];
}
```

<span style="text-decoration: underline">Swift:</span>

```
func applicationDidBecomeActive(application: UIApplication) {

   Pollfish.initAtPosition( pos: Int32, 
       			    withPadding: Int32, 
       		    andDeveloperKey: String!, 
       		      andDebuggable: Bool, 
       		      andCustomMode: Bool)
}
```
<br/>

### Pollfish init function takes the following parameters:

**1\. initAtPosition** (PollfishPosition) - Sets Position where you wish to place  Pollfish indicator --> ![alt text](https://storage.googleapis.com/pollfish_production/multimedia/pollfish_indicator_small.png)

<span style="text-decoration: underline">There are six different options available: </span> 

*   **PollFishPositionBottomLeft**  
*   **PollFishPositionBottomRight**  
*   **PollFishPositionTopLeft**  
*   **PollFishPositionTopRight**  
*   **PollFishPositionMiddleLeft** 
*   **PollFishPositionMiddleRight**  

**2\. withPadding** (int) - The padding from top or bottom of the screen according to PollfishPosition of the indicator (small red rectangle) specified before (0 is the default value)  

> **Note:** if used in MIDDLE position, padding is calculating from top.**  

**3\. andDeveloperKey** (NSString *)- Your API Key. This is the key that allows you to use Pollfish in your app. You can find it on Pollfish website after your registration, when you create an app in “My apps” section in the panel.  

**4\. andDebuggable (BOOL)** – Debug or Release mode  

<span style="text-decoration: underline">You can use Pollfish either in Debug or in Release mode.</span>  

*   **Debug/Developer mode** is used to show to the developer how Pollfish will be shown through an app (useful during development and testing).  
*   **Release mode** is the mode to be used for a released app in AppStore (start receiving paid surveys).  

> **Note:** Be careful to set andDebuggable parameter to false prior releasing to AppStore!  

5\. **andCustomMode** (BOOL) – Initializes Pollfish in custom mode if set to true. By default this is set to false.

**true Vs false**

*   **true** -  ignores Pollfish panel behavior from Pollfish Developer Dashboard. It always skips showing Pollfish indicator (small red rectangle) and always force open Pollfish panel view to app users. This method is usually used when app developers want to incentivize first somehow their users. 
*   **false** - is the standard way of using Pollfish in your apps. This option enables controlling behavior (intrusiveness) of Pollfish panel in an app from Pollfish Developer Dashboard.

![alt text](https://storage.googleapis.com/pollfish_production/multimedia/dashboard_1.png)

Below you can see an example of the init function:  

<span style="text-decoration: underline">Objective-C:</span>

```
- (void)applicationDidBecomeActive:(UIApplication *)application {

  [Pollfish initAtPosition: PollFishPositionMiddleRight
             withPadding: 0
	     andDeveloperKey: @"2ae349ab-30b8-4100-bc4d-b33b82e76519" 
           andDebuggable: false 
           andCustomMode: false];
           
}
```

<span style="text-decoration: underline">Swift:</span>
 
```
func applicationDidBecomeActive(application: UIApplication) {

 Pollfish.initAtPosition(Int32(PollfishPosition.PollFishPositionMiddleRight.rawValue), 
       			    withPadding: 0, 
       		    andDeveloperKey: "2ae349ab-30b8-4100-bc4d-b33b82e76519" , 
       		      andDebuggable: false, 
       		      andCustomMode: false)
}
```
<br/>
**At this point you are ready to go live! Turn your app to Release mode by setting andDebuggable:false and submit your app to AppStore.**
<br/><br/>
### 6\. Distributing your app to AppStore

Pollfish uses Advertising Identifier (IDFA) for survey distribution and therefore when submitting your app to the App you should select the following options as seen in the image below:  

<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish-images/idfa_3.png"/>

<br/>

### 7\.  Update your Privacy Policy

Add the following paragraph to your app's privacy policy:

*“Survey Serving Technology*  

*This app uses Pollfish SDK. Pollfish is an on-line survey platform, through which, anyone may conduct surveys. Pollfish collaborates with Developers of applications for smartphones in order to have access to users of such applications and address survey questionnaires to them. When a user connects to this app, a specific set of user’s device data (including Advertising ID which will may be processed by Pollfish only in strict compliance with google play policies- and/or other device data) and response meta-data (including information about the apps which the user has installed in his mobile phone) is automatically sent to Pollfish servers, in order for Pollfish to discern whether the user is eligible for a survey. For a full list of data received by Pollfish through this app, please read carefully Pollfish respondent terms located at https://www.pollfish.com/terms/respondent. These data will be associated with your answers to the questionnaires whenever Pollfish sents such questionnaires to eligible users. By downloading the application you accept this privacy policy document and you hereby give your consent for the processing by Pollfish of the aforementioned data. Furthermore, you are informed that you may disable Pollfish operation at any time by using the Pollfish “opt out section” available on Pollfish website . We once more invite you to check the respondent’s terms of use, if you wish to have more detailed view of the way Pollfish works.*  

*APPLE, GOOGLE AND AMAZON ARE NOT A SPONSOR NOR ARE INVOLVED IN ANY WAY IN THIS CONTEST/DRAW. NO APPLE PRODUCTS ARE BEING USED AS PRIZES.”*

<br/><br/>

---
<br/>
<img style="margin: 0 auto; display: block;" src="https://storage.googleapis.com/pollfish_production/multimedia/basic-format.gif"/>
<br/>

You can have a look for some integration tips <a href="https://www.pollfish.com/blog/2017/08/22/10-facts-about-mobile-rewarded-surveys/">here</a> or if have any question, like why you do not see surveys on your own device in release mode, please have a look in our <a href="https://pollfish.zendesk.com/hc/en-us/sections/201328652-Publishers">FAQ page</a>
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


In our efforts to include publishers in this process and be as transparent as possible we provide full control over the process. We let publishers decide if their users are served these standalone surveys or not, in 2 different ways. Firstly by monitoring the process in code and excluding any users by listening to the relevant noitifications (Pollfish Survey Received, Pollfish Survey Completed) and checking the Pay Per Survey (PPS) field which will be 0 USD cents. Secondly, publishers can disable the standalone demographic surveys through the Pollfish Developer Dashboard in the Settings area of an app. You can read more on demographic surveys <a href="https://www.pollfish.com/docs/demographic-surveys">here</a>. 

If you know attributes about a user like gender, age and others, you can provide them during initialization as described in section 9 - "Passing user attributes to skip or shorten Pollfish Demographic surveys" and skip or shorten this way, Pollfish Demographic surveys.



<br/>

### 8\.  Request your account to get verified

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

### 9\. Handling changes in app’s view hierarchy after intialization (optional)

#### Call of init when changes in your app’s view hierarchy happen during app’s lifecycle or Pollfish is not shown on top view

When your app changes it’s view hierarchy during it’s lifecycle (e.g. through a storyboard), or when Pollfish is not shown on the top view of your application, you can call Pollfish init method again in your current’s ViewController viewWillAppear methos, in order to bring Pollfish back on the top of your views.  

For example:

<span style="text-decoration: underline">Objective-C:</span>

```
- (void)viewWillAppear:(BOOL)animated
{
    [super viewWillAppear:animated];
    
    [Pollfish initAtPosition: PollFishPositionMiddleRight
                 withPadding: 0
             andDeveloperKey: @"2ae349ab-30b8-4100-bc4d-b33b82e76519" 
               andDebuggable: false 
               andCustomMode: false];
}
```

<span style="text-decoration: underline">Swift:</span>
 
```
override func viewWillAppear(animated: Bool) 
{
    super.viewWillAppear(animated)
    
    Pollfish.initAtPosition(Int32(PollfishPosition.PollFishPositionMiddleRight.rawValue), 
       			    withPadding: 0, 
       		    andDeveloperKey: "2ae349ab-30b8-4100-bc4d-b33b82e76519" , 
       		      andDebuggable: false, 
       		      andCustomMode: false)
}
```

Another example of this case is when showing for example a modal view controller. This controller changes current view hierarchy in order to display modal view controller on top. Therefore, in that case you need to call init again to bring Pollfish back on top.  

For example:  

<span style="text-decoration: underline">Objective-C:</span>

```
- (IBAction)showModal:(id)sender {
						    
    	UIStoryboard *storyboard = [UIStoryboard storyboardWithName:@"Main_iPhone" bundle:nil];
 
	MyModalViewController  *myModalViewController = [storyboard instantiateViewControllerWithIdentifier:@"MyModalViewController"];
    	
    myModalViewController.modalPresentationStyle = UIModalPresentationFullScreen;
   
  	[self presentViewController: myModalViewController animated:YES completion:nil];
    
	[Pollfish initAtPosition: PollFishPositionMiddleRight
                 withPadding: 0
		     andDeveloperKey: @"2ae349ab-30b8-4100-bc4d-b33b82e76519" 
               andDebuggable: false 
               andCustomMode: false];
}

- (IBAction)dismissController:(id)sender {

    	[[self presentingViewController] dismissViewControllerAnimated:YES completion:^{
        
        [Pollfish initAtPosition: PollFishPositionMiddleLeft
                     withPadding: 0
                 andDeveloperKey: @"af89aaf1-b7d4-46c1-8e91-b2625c2d5dbe"
                   andDebuggable: false 
                   andCustomMode:false];
    	}];
}
```

<span style="text-decoration: underline">Swift:</span>

```
@IBAction func showModal(sender: AnyObject) {

    	self.presentViewController(myModalViewController, animated: true, completion: nil)
  
    	Pollfish.initAtPosition(Int32(PollfishPosition.PollFishPositionMiddleRight.rawValue), 
       			    withPadding: 0, 
       		    andDeveloperKey: "2ae349ab-30b8-4100-bc4d-b33b82e76519" , 
       		      andDebuggable: false, 
       		      andCustomMode: false)
}

@IBAction func dismissController(sender: AnyObject) {

	myModalViewController.dismissViewControllerAnimated(true, completion: {  
	
	Pollfish.initAtPosition(Int32(PollfishPosition.PollFishPositionMiddleRight.rawValue), 
       			    withPadding: 0, 
       		    andDeveloperKey: "2ae349ab-30b8-4100-bc4d-b33b82e76519" , 
       		      andDebuggable: false, 
       		      andCustomMode: false)});
}
```
 
 
Note:

• It is very important to call init function of Pollfish when the view hierarchy has already changed. Therefore in the example above you have to call init after the completion of the dismissal of the modal view controller.  

• Be careful to use the same arguments as the arguments you used in the init function in your app’s delegate.  

• Even if you call init in any ViewController somewhere within the app lifecycle you should still keep the init function in your App’s Delegate.  

If you still have questions regarding how to handle view hierarchy changes have a look in SampleApp in iOS SDK  

<br/>
### 10\. Other init methods (optional)

#### Passing custom parameter for server to server postback calls

If you need to pass a custom parameter (for example a UUID as registered in your system) through Pollfish init function within the SDK and receive it back with Server to Server, survey completed postback call you can use:  

<span style="text-decoration: underline">Objective-C:</span>

```
 [Pollfish initAtPosition: (PollfishPosition)
              withPadding: (int)
	      andDeveloperKey: (NSString *)
            andDebuggable: (BOOL) 
	        andCustomMode: (BOOL)
	       andRequestUUID: (NSString *)];
```

<span style="text-decoration: underline">Swift:</span>

```
func applicationDidBecomeActive(application: UIApplication) {

   Pollfish.initAtPosition( pos: Int32, 
       			    withPadding: Int32, 
       		    andDeveloperKey: String!, 
       		      andDebuggable: Bool, 
       		      andCustomMode: Bool
       		     andRequestUUID: String!)
}
```
<br/>

#### Passing user attributes to skip or shorten Pollfish Demographic surveys

If you know upfront some user attributes like gender, age, education and others you can pass them during initialization in order to shorten or skip entirely Pollfish Demographic surveys and also achieve a better fill rate and higher priced surveys.

| **Note:** You need to contact Pollfish live support on our website to request your account to be eligible for submitting demographic info through your app, otherwise values submitted will be ignored by default


<span style="text-decoration: underline">Objective-C:</span>

```
 [Pollfish initAtPosition: (PollfishPosition)
              withPadding: (int)
	      andDeveloperKey: (NSString *)
            andDebuggable: (BOOL) 
	        andCustomMode: (BOOL)
	    andUserAttributes: (NSMutableDictionary *)];
```

<span style="text-decoration: underline">Swift:</span>

```
func applicationDidBecomeActive(application: UIApplication) {

   Pollfish.initAtPosition( pos: Int32, 
       			    withPadding: Int32, 
       		    andDeveloperKey: String!, 
       		      andDebuggable: Bool, 
       		      andCustomMode: Bool
	          andUserAttributes: NSMutableDictionary!)
}
```
<br/>

an example of user attributes dictionary could be the following one:

<span style="text-decoration: underline">Objective-C:</span>
```
    UserAttributesDictionary *userAttributesDictionary = [[UserAttributesDictionary alloc] init];
    
    /*included in Demographic Surveys*/
    [userAttributesDictionary setGender: GENDER(MALE)];
    [userAttributesDictionary setRace:RACE(WHITE)];
    [userAttributesDictionary setYearOfBirth:YEAR_OF_BIRTH(_1984)];
    [userAttributesDictionary setMaritalStatus:MARITAL_STATUS(MARRIED)];
    [userAttributesDictionary setParentalStatus:PARENTAL_STATUS(THREE)];
    [userAttributesDictionary setEducation:EDUCATION_LEVEL(UNIVERSITY)];
    [userAttributesDictionary setEmployment:EMPLOYMENT_STATUS(EMPLOYED_FOR_WAGES)];
    [userAttributesDictionary setCareer:CAREER(TELECOMMUNICATIONS)];
    [userAttributesDictionary setIncome:INCOME(MIDDLE_I)];
    
    /*other user attributes*/
    [userAttributesDictionary setEmail:@"user@email.com"];
    [userAttributesDictionary setFacebookId:@"USER_FB"];
    [userAttributesDictionary setGoogleId:@"USER_GOOGLEID"];
    [userAttributesDictionary setTwitterId:@"USER_TWITTER"];
    [userAttributesDictionary setLinkedInId:@"USER_LINKEDIN"];
    [userAttributesDictionary setPhone:@"0030002221929"];
    [userAttributesDictionary setName:@"USER_NAME"];
    [userAttributesDictionary setSurname:@"USER_SURNAME"];
    [userAttributesDictionary setCustomAttributeWithKey:@"my_param" andValue:@"my_value"];
    
```
    

<span style="text-decoration: underline">Swift:</span>
```
    let userAttributesDictionary:UserAttributesDictionary = [:]
    
    /*included in Demographic Surveys*/
    userAttributesDictionary.setGender(GENDER(MALE));
    userAttributesDictionary.setRace(RACE(WHITE));
    userAttributesDictionary.setYearOfBirth(YEAR_OF_BIRTH(_1984));
    userAttributesDictionary.setMaritalStatus(MARITAL_STATUS(MARRIED));
    userAttributesDictionary.setParentalStatus(PARENTAL_STATUS(THREE));
    userAttributesDictionary.setEducation(EDUCATION_LEVEL(UNIVERSITY));
    userAttributesDictionary.setEmployment(EMPLOYMENT_STATUS(EMPLOYED_FOR_WAGES));
    userAttributesDictionary.setCareer(CAREER(TELECOMMUNICATIONS));
    userAttributesDictionary.setIncome(INCOME(MIDDLE_I));
    
    /*other user attributes*/
    userAttributesDictionary.setEmail(@"user@email.com");
    userAttributesDictionary.setFacebookId(@"USER_FB");
    userAttributesDictionary.setGoogleId(@"USER_GOOGLEID");
    userAttributesDictionary.setTwitterId(@"USER_TWITTER");
    userAttributesDictionary.setLinkedInId(@"USER_LINKEDIN");
    userAttributesDictionary.setPhone(@"0030002221929");
    userAttributesDictionary.setName(@"USER_NAME");
    userAttributesDictionary.setSurname(@"USER_SURNAME");
    userAttributesDictionary.setCustomAttributeWithKey(@"my_param" andValue:@"my_value");
    
```

#### Explicitly requesting a specific survey format for testing purposes

If you want to test Pollfish different available Survey Formats you can explicitly request a specific survey format during initialization

| **Note:** You can request and receive a specific survey format only in debug mode

There are four different options available: 

- SurveyFormatBasic
- SurveyFormatPlayful
- SurveyFormatRandom
- SurveyFormatThirdParty


Here is an example of how a user can explicitly request a specific survey format during initialization.
```
 [Pollfish initAtPosition: (PollfishPosition)
              withPadding: (int)
	      andDeveloperKey: (NSString *)
            andDebuggable: (BOOL) 
	        andCustomMode: (BOOL)
	       andRequestUUID: (NSString *)
	    andUserAttributes: (NSMutableDictionary *)
	    andSurveyFormat: (SurveyFormat *)];
```

<span style="text-decoration: underline">Swift:</span>

```
func applicationDidBecomeActive(application: UIApplication) {

   Pollfish.initAtPosition( pos: Int32, 
       			    withPadding: Int32, 
       		    andDeveloperKey: String!, 
       		      andDebuggable: Bool, 
       		      andCustomMode: Bool
		     andRequestUUID: String!
	          andUserAttributes: NSMutableDictionary!
		  andSurveyFormat: Int32)
}
```


### 11\. Manually show or hide Pollfish (optional)

You can manually hide and show Pollfish from your various UIVIewControllers. by calling anywhere after initialization:  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish show];
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.show()
```

or  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish hide];
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.hide()
```


For example:  

<span style="text-decoration: underline">Objective-C:</span>

```
// MyViewController1
- (void)viewWillAppear:(BOOL)animated
{
    // ...
    [Pollfish hide];
}

// MyViewController2
- (void)viewWillAppear:(BOOL)animated
{
    // ...
    [Pollfish show];
}
```

<span style="text-decoration: underline">Swift:</span>

```
// MyViewController1
override func viewWillAppear(animated: Bool) 
{
    super.viewWillAppear(animated)
  
    // ...
    Pollfish.hide()
}

// MyViewController2
override func viewWillAppear(animated: Bool) 
{
    super.viewWillAppear(animated)
    
    // ...
    Pollfish.hide()
}
```
<br/>

### 12\. Update user location (optional)

You can update user’s location anytime after initialization to get better fill rate on surveys by calling the following:  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish updateLocationWith:(CLocation *) location];
```

<span style="text-decoration: underline">Swift:</span>

```
 Pollfish.updateLocationWith(location: CLLocation!);
```
<br/>

### 13\. Send beacon information (optional)

You can send beacon information if available anytime after initialization to get to be eligible for receiveing beacon surveys by calling the following:  

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish sendBeaconInfo:(CLBeacon *)beacon];
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.sendBeaconInfo(beacon: CLBeacon!);
```
<br/>

### 14\.Implement Pollfish event listeners (optional)

> **Note:** Pollfish listeners/notifications fire in an asynchronous way. Having said that it's possible that you receive them while being in a background thread and not the main UI thread. If you want to make any prompts or custom changes on the view level when you receive those notifications, please be sure to make them on the main UI thread

### 14.1 Get notified when a survey is received


You can be notified when a survey is received via the iOS Notification Center. Note that the observer should be already registered when a survey is received in order to run the selector.  


<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(surveyReceived) name:@"PollfishSurveyReceived" object:nil];
```

```
- (void)surveyReceived
{
    NSLog(@"A survey was received!");
}
```

<span style="text-decoration: underline">Swift:</span>

```
 NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(YOUR_CONTROLLER.pollfishReceived) , name:
            "PollfishSurveyReceived", object: nil)
```

```
func pollfishReceived() 
{
   print("A survey was received!");
}
```

You can also get informed about the price and type of survey (playful or not) that was received by listening and reading the relevant notification object. Price is shown in USD (estimated based on daily exchange currency).

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishReceived:) name:@"PollfishSurveyReceived" object:nil];
```

```
- (void)pollfishReceived:(NSNotification *)notification
{
    BOOL playfulSurvey = [[[notification userInfo] valueForKey:@"playfulSurvey"] boolValue];
    int surveyPrice = [[[notification userInfo] valueForKey:@"surveyPrice"] intValue];
    
    NSLog(@"Pollfish Survey Received - Playful Survey: %@ with survey price: %d" , playfulSurvey?@"YES":@"NO", surveyPrice);
}
```

<span style="text-decoration: underline">Swift:</span>

```
 NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(FirstViewController.pollfishReceived(_:)) , name:
            "PollfishSurveyReceived", object: nil)
```

```
func pollfishReceived(_ notification:Notification) {
     
  let tmp : [AnyHashable: Any] = notification.userInfo!
        
  let playfulSurvey = tmp["playfulSurvey"]! as! Bool
  let surveyPrice = tmp["surveyPrice"]!
        
  print("Pollfish Survey Received - Playful Survey : \(playfulSurvey)  with survey price: \(surveyPrice)")

}
```
<br/>
### 14.2 Get notified when survey is completed

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(surveyCompleted) name:@"PollfishSurveyCompleted" object:nil];
```

```
- (void)surveyCompleted
{
    NSLog(@"Pollfish Survey Completed!");
}
```
<span style="text-decoration: underline">Swift:</span>

```
 NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(YOUR_CONTROLLER.pollfishCompleted) , name:
            "PollfishSurveyCompleted", object: nil)
```

```
func pollfishCompleted() 
{
   print("Pollfish Survey Completed!");
}
```

You can also get informed about the price and type of survey (playful or not) that was completed by listening and reading the relevant notification object. Price is shown in USD (estimated based on daily exchange currency).

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishCompleted:) name:@"PollfishSurveyCompleted" object:nil];
```

```
- (void)pollfishCompleted:(NSNotification *)notification
{
    BOOL playfulSurvey = [[[notification userInfo] valueForKey:@"playfulSurvey"] boolValue];
    int surveyPrice = [[[notification userInfo] valueForKey:@"surveyPrice"] intValue];
    
    NSLog(@"Pollfish Survey Completed - Playful Survey: %@ with survey price: %d" , playfulSurvey?@"YES":@"NO", surveyPrice);
}
```

<span style="text-decoration: underline">Swift:</span>

```
 NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(FirstViewController.pollfishCompleted(_:)) , name:
            "PollfishSurveyCompleted", object: nil)
```

```
func pollfishCompleted(_ notification:Notification) {
     
  let tmp : [AnyHashable: Any] = notification.userInfo!
        
  let playfulSurvey = tmp["playfulSurvey"]! as! Bool
  let surveyPrice = tmp["surveyPrice"]!
        
  print("Pollfish Survey Completed - Playful Survey : \(playfulSurvey)  with survey price: \(surveyPrice)")

}
```

<br/>
### 14.3 Get notified when a user is not eligible for a Pollfish survey


You can be notified when a user is not eligible for a Pollfish survey after accepting to take it via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishUsernotEligible) name:@"PollfishUserNotEligible" object:nil];
```

```
- (void)pollfishUsernotEligible
{
    NSLog(@"Pollfish User Not Eligible");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(YOUR_CONTROLLER.pollfishUsernotEligible), name:"PollfishUserNotEligible", object: nil)
```

```
func pollfishUsernotEligible() 
{
     print("Pollfish User Not Eligible")
}
```

<br/>
### 14.4 Get notified when survey is not available


You can be notified when a survey is not available for a user via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(surveyNotAvailable) name:@"PollfishSurveyNotAvailable" object:nil];
```

```
- (void) surveyNotAvailable
{
    NSLog(@"Pollfish Survey Not Available!");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(YOUR_CONTROLLER.pollfishNotAvailable)  , name:"PollfishSurveyNotAvailable", object: nil)
```

```
func pollfishNotAvailable() 
{
     print("Pollfish Survey Not Available!")
}
```

<br/>
### 14.5 Get notified when Pollfish is opened


You can be notified when a user opens Pollfish survey panel via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishOpened) name:@"PollfishOpened" object:nil];
```

```
- (void)pollfishOpened
{
    NSLog(@"Pollfish is opened!");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(YOUR_CONTROLLER.pollfishOpened), name:"PollfishOpened", object: nil)
```

```
func pollfishOpened() 
{
     print("Pollfish is opened!")
}
```

<br/>
### 14.6 Get notified when Pollfish is closed


You can be notified when a user closes Pollfish survey panel via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishClosed) name:@"PollfishClosed" object:nil];
```

```
- (void)pollfishClosed
{
    NSLog(@"Pollfish is closed!");
} 
```

<span style="text-decoration: underline">Swift:</span>

```
NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(YOUR_CONTROLLER.pollfishClosed) , name:"PollfishClosed", object: nil)
```

```
func pollfishClosed() 
{
     print("Pollfish is closed!")
}
```

<br/>

### 14.7 Get notified when a user rejected a survey (added in Pollfish v4.4.0)


You can be notified when a user rejected a survey via the iOS Notification Center.  

<span style="text-decoration: underline">Objective-C:</span>

```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(pollfishUserRejectedSurvey) name:@"PollfishUserRejectedSurvey" object:nil];
```

```
- (void)pollfishUserRejectedSurvey
{
    NSLog(@"Pollfish User Rejected Survey");
}
```

<span style="text-decoration: underline">Swift:</span>

```
NSNotificationCenter.defaultCenter().addObserver(self, selector:#selector(YOUR_CONTROLLER.pollfishUserRejectedSurvey), name:"PollfishUserRejectedSurvey", object: nil)
```

```
func pollfishUserRejectedSurvey() 
{
     print("Pollfish User Rejected Survey")
}
```

<br/>

### 15\. Check if Pollfish survey is still available on your device (optional)

It happens that time had past since you initialized Pollfish and a survey is received. If you want to check if survey is still avaialble on your device and has not expired you can check by calling:

<span style="text-decoration: underline">Objective-C:</span>

```
[Pollfish isPollfishPresent]
```

<span style="text-decoration: underline">Swift:</span>

```
Pollfish.isPollfishPresent()
```

<br/>

### 16\. Server-to-server callbacks on survey completion (optional)

If you want to reward your users for completing a survey it is common practise to verify this through server to server callbacks in order to introduce an enhanced security layer to your system. You can easily add your postback  url on your app's page on Pollfish Developer Dashboard. You can read more on how to set server to server callbacks in our FAQ page <a href="https://pollfish.zendesk.com/hc/en-us/articles/204106261">here</a>. 




