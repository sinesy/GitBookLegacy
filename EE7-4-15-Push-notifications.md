# Push notifications

A push notification is a text message that a mobile device can receive and linked to a specific app installed in your device. That message can be received even when your app is not running.  
You can also interact with that message, by clicking on it and start your application in order to open a specific window, if needed.  
You can configure your Platform mobile app in order to listen to Push notifications, coming from a message generator, which is a server-side javascript action, executed on the Platform server.  
Behind the scenes, Platform is based on the Google Cloud Platform and on Firebase Push notification system, described below:

* the mobile app must first register on Firebase, in order to receive Push notifications
* through a server-side javascript action you can generate messages, sent to Firebase
* Firebase then sends these messages as Push notifications to all the mobile devices registered previously on the same project; a Push notification is sent to a set of phone numbers specified along with the message.

![](http://4wsplatform.org/wp-content/uploads/2017/10/firebase_push-1024x566.jpg)

In order to use the Push notification, a few settings must be defined before:

* define a  **Google Cloud Project in Firebase** , used to manage the Push notifications for your app; this activity can be carried out by Sinesy or managed on yourself, if you own a Google Cloud Platform account
* generate an  **Auth Key**  from within Firebase Admin Console, used on the server side to send messages which can be accepted by Firebase. This key must be set in Application -&gt; Application Detail -&gt; Folder “Application Parameters” -&gt; “ **Firebase Key used to send Push messages** “
* the mobile app must be configured in order to register itself on Firebase. This task is automatically performed by the app, if it has been configured with the Push notification setting enabled \(e.g. on iOS the main.m class must have “pushNotifications” set to true.

Once done that, a server-side js action can send a message through this method:

```js
utils.sendPushNotification(appId, usernamesList, title, body, actionIdToCall, valueObject, iOSBadgeCount);
```

where:

* **appId**  represents the application identifier for the mobile app
* **usernamesList**  – list of usernames \[“USERNAME1”, “USERNAME2”, …\] used to identify the mobile devices which will receive the Push notification. More precisely, the notification will be sent to all the devices which have done at least one synchronization having such username set in.
* **title**  is the main text to send
* **body**  is optional: it represents an additional text to include along with the title
* **actionIdToCall**  is the identifier for a javascript action to execute within the mobile app, which will be automatically invoked when the user click on the Push notification: it can be used to perform some actions for this event, like showing a window
* **valueObject** : a javascript object containing data to include with the message; this is helpful in case you want to pass to the action to invoke data needed to correctly perform some operations \(e.g. the primary key for a record to show\)
* **iOSBadgeCount** : the number of notifications sent; unfortunately, iOS mobile apps are not able to automatically manage the number of notifications to show per app, so you have to pass the number of notifications to show; that means you have to store this number somewhere!

## Example

```js
var usersEmails = ["email1@gmail.com","email2@gmail.com","emailN@gmail.com"]; //an array of registered user email accounts
var appMobileId = "MINION"; //the mobile application id
var notificationTitle = "Hello!"; //notification title
var notificationBody = "How did the cat get so fat?"; //notification body
var actionIdToCall = 123; //[optional] mobile actionId to call on the notification click if necessary
var valueObject = {"field1":"value1","field2":"value2","fieldN":"valueN"}; //[optional] map of &lt;String, String&gt; to use in the action id if necessary
var iOSBadgeCount = 1; //Total count of notification

utils.sendPushNotification(appMobileId, usersEmails , notificationTitle, notificationBody, 123, JSON.stringify(valueObject), iOSBadgeCount);
```

On the other side, in the mobile app, when the Push notification is received, it will be shown automatically by the mobile device.  
 **Only in case you have defined an action id** , the following events can happen:  
When the push notification reaches the mobile application, it calls the optional action defined in the **sendPushNotification** . The action will receive in input a javascript object containing the data sent from that method.  
In addition, the vo object also contains a status attribute, having different values:

* vo.notificationFieldStatus = “RECEIVED”

when the user clicks the notification, the mobile app call theoptional actionId defined in the **sendPushNotification** injecting in the valueObject a parameter with the status of the push:

* vo.notificationFieldStatus = “CLICKED”

This is an example of the optional actionIdToCall:

```js
if(vo.notificationStatus == "RECEIVED"){

    //For example this will update the "ideas" menu badge count with the count of unread notifications
    var unreadNotification = getUnreadNotificationsCount();
    setMenuBadges("ideas",unreadNotification);
} else if(vo.notificationStatus == "CLICKED"){
    //Reset the notification count
    resetUnreadNotifications();

    //update the "ideas" menu count
    setMenuBadges("ideas",0);

    //Open the window 39
    var args = {
       "param1":vo.field1,
       "param2":vo.field2,
       "paramN":vo.fieldN
    };
    openWindow39(args);  

}
```

As you can see from the example above, there are a few javascript methods available on the mobile app, that you can use to manage the notification:

---



