
---

# Reference guide

When defining a new mobile app through the App Designer, there are a few settings to set in the "**Configuration**" panel. This panel is the same used when defining a web application. Among them, there are a few mandatory fields to set:

* **app id**
* **description**
* **context path mobile** - this subfolder is used to include static content to pass to the mobile app, such as images, documents, etc.
* **context path web** - this subfolder will be used only by the corresponding web application opened starting from the Platform home page; this web application is typically used only to define users and roles for the mobile app

Apart from the main settings defined in the "Configuration" panel, there two additional panels you can use to set further settings for a mobile app:

* "**Mobile**" - this panel includes settings that are specific for a mobile app and not shown when defining a web app
* "**Events**" - this panel includes events at app level \(not related to panels or components...\), that are specific for a mobile app and not shown when defining a web app

In the following sections, the Mobile and Events panels are described more in depth.

---

#### Mobile settings

![](/assets/mobile_dettaglio.png)In the "Mobile" panel there are fields specific for a mobile app, including:

**App orientation** - define how the render the app content: horizontally \(Landscape\) or vertically \(Portrait\)

**Synchronization type** - the synchronization is the process managed by Platform, through which it is possible to update the application content \(in terms of UI, business logic, tables, data, files\), without the need to "publish" the app again in the AppStore or GooglePlay. That means it is possible to update the mobile app behind the scenes, using Platform sync system. It is possible to define when this synchronization process must be executed: automatically or manually. In the first case, every time the app is launched, the sync process will automatically start, search for updates if available. In the latter, the sync process can only be started by the end user, through a "Sync" command available the app menu

**App version **- reports the current app version; this value is used to figure out whether the app requires a sync process or not. It can be manually edited in order to force a sync process \(in case of automatic sync type\).

**Synchronization folder **- defines the base path in the Platform server side file system, where storing files needed during the sync process. The content of this storage is automatically managed by Platform

**File writing/reading + Import/extract command + Start date/time imp/exp + Wait data imp/exp **- these fields are usually left empty and they can be used to by-pass the default sync mechanism directly managed by Platform, in order to execute external commands \(e.g. shell commands used to launch ETL processes\) needed to prepare data to pass to the mobile apps or viceversa

**Wait data deleting **- number of days to wait before deleting data not send to mobile devices yet. As already described before, Platform automatically manage the sync process, when a mobile app is launched. The sync process can involve the preparation of data to sent to every mobile device \(in case of offline functionalities\). This data preparation can be time consuming: for that reason, it is optimized by Platform, by prepare all data needed for each device in advance, before a device starts the sync process: in this way, data is already available at that time and the sync process time is minimized. As a consequence, data preparation involves disk space consumption on the server-side layer. The current field defines the max number of days to maintain data in the server-side, before deleting them, in order to take under control the storage consumption for devices which do not sync for a long time

**Sync menu enable **- flag used to show/hide the Sync command in the app menu; it is recommended to maintain it visible, in order to allow the end user to force a sync task, if needed. This command should always be visible, in case of "manual sync type".

**Metadata sync menu enable** - flag used to show/hide the Sync command in the app menu; it is recommended to maintain it visible, in order to allow the end user to force a sync task, if needed. This command should always be visible, in case of "manual sync type". This command should be shown as an alternative to the previous one and it reduce the sync process to app UI/behavior only, not to data.

**Enable realtime sync** - in case of an app including offline functionalities, i.e. detail forms through which it is possible to read/write data in local database tables, the data changes \(insert, update, delete operations\) are sent to the server-side only when a sync task is started. When this flag is set, the changes are sent to the server-side in real time, that is to say, when they are written locally they are also sent to the server-side, without waiting for the sync task. Pay attention to this feature: it is network consuming and it could slow down the performance of the mobile app

**About menu enable** - flag used to show/hide the About command in the app menu, where it is reported information about the app. Such information is defined in the "About" panel in the app definition window, expressed in HTML format.

**Logout menu enable when** - a boolean expression which can includes variables supported by the mobile app \(expressed with the :XXX format with && or \|\| as logical operators\) and used to figure out whether the Logout menu is enabled or not. When the Logout command is enabled, the user is logged out and its personal data could be lost \(or not\), according to the following field

**Logout behavior **- When the Logout command is enabled and the user clicks on it in the mobile app, the user is logged out and its personal data

* will be maintained inside the app, if the current field is set to "Do nothing"
* will be cleared up, if the current field is set to "Remove all data"

---

#### Events settings

![](/assets/mobile_events.png)

The "Events" panel allows to define a series of events which can be set at mobile app level, i.e. not linked to a specific window, panel, control:

**Action before showing **- js action executed inside the mobile app, every time the app is launched or after every synchonization, in order to execute a custom logic needed to the rest of the app

**Action after showing** - js action executed inside the mobile app, every time the app is launched or after every synchonization, in order to execute a custom logic needed to the rest of the app and to apply after showing the app, i.e. after the menu creation or after showing the initial window of the app

**Before writing data** - server-side js action executed before writing data in online functionalities \(insert/update/delete operations\); it should always return a JSON object containing the "success" attribute: a false value would interrupt the writing operation with an error, reported in the "message" attribute.

Example:

```js
{
  success: true|false,
  message: "the-reason-why-interrupting-the-writing-op"
}
```

**First window to show** - optional field used to define the initial window to show automatically when opening the app or after a sync process; if not specified, the About content is automatically shown

**Action before first sync **- js action executed inside the mobile app, only the first time the app is launch, after the first sync process

**Action after sync **- server-side js action executed on the server-side, at the end of every sync process. More precisely, this action is invoked for each offline table used to read/write data \(i.e. for each offline table defined through the Mobile -&gt; Read/write tables\). Platform automatically pass forward to the action a "vo" javascript object containing:

* the mobile table under management
* the primary key values for each record changed on the mobile app and received during the sync process. For each primary key, the corresponding writing operation is reported as well, expressed as I \(insert\), U \(update\) or D \(delete\).

Such "vo" object always has a structure as follows:

```
{
  "tableName":".....",
   "pks":[
       {"opType":"...","pk": {...}   },
      ...
   ]
}
```

In this way, it is possible to know exactly which records have been modified by the mobile app and, if needed, execute custom logic based on such information.

Example:

```
{
  "tableName":"MOB_CLIENTS",
   "pks":[
       {"opType":"U","pk":{"clientCode":"C2"}},
       {"opType":"U","pk":{"clientCode":"C5"}},
       {"opType":"D","pk":{"clientCode":"C7"}}
   ]
}
```

**Action to invoke on logout **- js action executed on the mobile device when the Logout command is clicked by the end user.

It could be used to perform custom deleting logic on the offline database.

**Push message action **- js action automatically invoked inside the mobile device, each time a Push notification is received by the app. Please note that before receiving Push notification, the app must be previously configured with Firebase Push service and correctly registered on it, as well as the specific mobile device.

Once done that, this action will be invoked automatically when a Push notification is received.

**Registration action **- js action invoked when the user is signing up, in order to perform custom logic needed at the end of the registration task, such as writing data in custom tables.

**App started in Beacon region **- js action executed in the mobile device every time the device is close to a configured Beacon and the app is currently opened

**App started exit from Beacon region **- js action executed in the mobile device every time the device is not any more close to a configured Beacon and the app is currently opened

**App off in Beacon region **- js action executed in the mobile device every time the device is close to a configured Beacon and the app is currently closed

**App off exit from Beacon region **- js action executed in the mobile device every time the device is not any more close to a configured Beacon and the app is currently closed

**Network connectivity lost/restored** - js action executed when the mobile device lost or restore connection. The passed vo contains the connection status in the field "connectionStatus", this field can value "ONLINE" or "OFFLINE"

Example:

```
if(vo.connectionStatus == "ONLINE){
    //connection restore
}else{
    //you are offline
}
```

---

You can find additional information into the API Documentation [here](https://4wsplatform.gitbooks.io/api/content/mobile-variables/inside-a-business-component-executed-on-the-mobile-app.html).

---



