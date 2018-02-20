# App deployment for the iOS platform

Apple has strict constraints related to the deployment of mobile apps: an app can be either public \(B2C app\) or private \(B2B app\).

The first type of app must be published in the Apple AppStore and has to follow the deployment process provided by Apple.  
Typically, a deployment in the AppStore requires 1-2 weeks to be completed.  
To make it more difficult, Apple can deny the deployment of an app which does not fit the requirements defined by Apple, so not only there is not a clear time-to-market time, but it is not sure that the app will be accepted by Apple.  
This kind of app requires an Apple Developer Program agreement \(about 99$ per year\); through it a customer can create any number of apps and \(try to\) publish them to the AppStore.  
See [https://developer.apple.com/programs/enroll/](https://developer.apple.com/programs/enroll/) for more details.

The second type of app requires an Apple Enterprise Program agreement \(about 299$ per year\) and it is used by organizations to create any number of apps which are not public and that can be published internally in any organization service. That means that there is not neither a checking by Apple related to the content of the app, nor the wait time required by Apple to carry out that checking.  
The only constraint the organization has to respect is the target of users: only users beloning to the organization can use the app.

Because of all these constraints defined by Apple, the customer has to buy on its own one of the two Programs available with Apple. Once the program has been purchased, the app creation task can start.  
4WS.Platform provides a form named "Create an iOS App", used to gather all data required to create a provisional mobile app.  
Required data are:

* app id
* app title

all icons required to correctly install the app in all iOS devices, with all the resolution required by these devices; this set of icons must be included in a .zip file to upload through the form; see [https://developer.apple.com/library/ios/qa/qa1686/\_index.html](https://developer.apple.com/library/ios/qa/qa1686/_index.html) for more details about the right resolutions to provide  
account \(username+password\) to use to access the Apple Developer/Enterprise Program  
This data is then internally sent to Sinesy where the provisional app will be created and sent back to the email address provided in the form.  
Only in case of a public app, once the app has been completely configured and it is ready to be published, Sinesy will use the Apple Developer Program account provided by the customer to sign the final version of the app and deploy it in the AppStore. This stage is out of control of Sinesy: only Apple will decide if the app is eligible to be published in the AppStore.

In the following schemas, the two deployment scenarios are reported:

**public App to deploy in AppStore**   
the customer has to buy an Apple Developer Program  
the customer has to fill in the form provided by 4WS.Platform every time a new app must be configured  
Sinesy will send back a provisional app, which can be used only for testing activities, during the configuration of the app using 4WS.Platform  
the customer is ready to make the app public on the AppStore: Sinesy will manage the deployment task, using the customer account  
Apple decides if the app is eligible to the AppStore and makes it public if approved.

**private App to deploy in the customer server**   
the customer has to buy an Apple Enteprise Program  
the customer has to fill in the form provided by 4WS.Platform every time a new app must be configured  
Sinesy will send back the final app, which can be used both for testing activities and as the final app; the customer account will be used to produce the empty app  
the customer is ready to make the app public on its own server: the same .ipa file can be published on that server

---



