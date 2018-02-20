# App deployment for the Android platform

An Android app can be public, i.e. accessible through the Google Play store or can be deployed in an enterprise environment.  
In both cases, a digital certificate must be defined and used when signing \(creating\) the app.  
This task is automatically managed by 4WS.Platform, through the "Create Android App" menu item: the user can specify a custom .keystore \(a Java digital certificate\) or let 4WS.Platform create it, starting from the data provided in the form shown.  
Once provided all this data, the .apk file is created by 4WS.Platform and published in the subcontext of the 4WS.Platform server.  
An Android mobile device can then access it through a web browser \(such as Chrome\) and download and install the app.  
When running the app, a warning message is prompted in the mobile device, showing that the app has been downloaded by a third party server \(4WS.Platform server\).  
The only way to avoid this warning is to publish the .apk app in the Google Play store, starting from a specific Google account. This separate task is not covered by 4WS.Platform: in case the customer prefers to deploy the app in Google Play \(make it public\), he has to create an account in Google Play and use it to publich the .apk file provided by 4WS.Platform.

In the following schemas, the two deployment scenarios are reported:

**public App to deploy in Google Play**   
the customer has to buy a Google Play Developer account \(see [https://play.google.com/apps/publish/signup/](https://play.google.com/apps/publish/signup/)\)  
the customer has to fill in the form provided by 4WS.Platform every time a new app must be configured: the .apk file is ready to be used in a few minutes  
the customer is ready to make the app public on the Google Play: he has to use its Developer account to publish the .apk file on it

**private App to deploy in the customer server**   
the customer has to fill in the form provided by 4WS.Platform every time a new app must be configured: the .apk file is ready to be used in a few minutes  
the customer is ready to make the app public on its own server: the same .apk file can be published on that server

---



