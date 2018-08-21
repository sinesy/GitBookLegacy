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

* **App orientation** - define how the render the app content: horizontally \(Landscape\) or vertically \(Portrait\)
* **Synchronization type** - the synchronization is the process managed by Platform, through which it is possible to update the application content \(in terms of UI, business logic, tables, data, files\), without the need to "publish" the app again in the AppStore or GooglePlay. That means it is possible to update the mobile app behind the scenes, using Platform sync system. It is possible to define when this synchronization process must be executed: automatically or manually. In the first case, every time the app is launched, the sync process will automatically start, search for updates if available. In the latter, the sync process can only be started by the end user, through a "Sync" command available the app menu
* **App version **- reports the current app version; this value is used to figure out whether the app requires a sync process or not. It can be manually edited in order to force a sync process \(in case of automatic sync type\).
* **Synchronization folder **- defines the base path in the Platform server side file system, where storing files needed during the sync process. The content of this storage is automatically managed by Platform
* **File writing/reading + Import/extract command + Start date/time imp/exp + Wait data imp/exp **- these fields are usually left empty and they can be used to by-pass the default sync mechanism directly managed by Platform, in order to execute external commands \(e.g. shell commands used to launch ETL processes\) needed to prepare data to pass to the mobile apps or viceversa
* **Wait data deleting **- number of days to wait before deleting data not send to mobile devices yet. As already described before, Platform automatically manage the sync process, when a mobile app is launched. The sync process can involve the preparation of data to sent to every mobile device \(in case of offline functionalities\). This data preparation can be time consuming: for that reason, it is optimized by Platform, by prepare all data needed for each device in advance, before a device starts the sync process: in this way, data is already available at that time and the sync process time is minimized. As a consequence, data preparation involves disk space consumption on the server-side layer. The current field defines the max number of days to maintain data in the server-side, before deleting them, in order to take under control the storage consumption for devices which do not sync for a long time
* **Sync menu enable **- flag used to show/hide the Sync command in the app menu; it is recommended to maintain it visible, in order to allow the end user to force a sync task, if needed. This command should always be visible, in case of "manual sync type".
* **Metadata sync menu enable** - flag used to show/hide the Sync command in the app menu; it is recommended to maintain it visible, in order to allow the end user to force a sync task, if needed. This command should always be visible, in case of "manual sync type". This command should be shown as an alternative to the previous one and it reduce the sync process to app UI/behavior only, not to data.
* **Enable realtime sync** - in case of an app including offline functionalities, i.e. detail forms through which it is possible to read/write data in local database tables, the data changes \(insert, update, delete operations\) are sent to the server-side only when a sync task is started. When this flag is set, the changes are sent to the server-side in real time, that is to say, when they are written locally they are also sent to the server-side, without waiting for the sync task. Pay attention to this feature: it is network consuming and it could slow down the performance of the mobile app
* **About menu enable** - flag used to show/hide the About command in the app menu, where it is reported information about the app. Such information is defined in the "About" panel in the app definition window, expressed in HTML format.
* **Logout menu enable when** - a boolean expression which can includes variables supported by the mobile app \(expressed with the :XXX format with && or \|\| as logical operators\) and used to figure out whether the Logout menu is enabled or not. When the Logout command is enabled, the user is logged out and its personal data could be lost \(or not\), according to the following field
* **Logout behavior **- When the Logout command is enabled and the user clicks on it in the mobile app, the user is logged out and its personal data
  * will be maintained inside the app, if the current field is set to "Do nothing"
  * will be cleared up, if the current field is set to "Remove all data"

---

#### Events settings

![](/assets/mobile_events.png)

---

You can find additional information into the API Documentation [here](https://4wsplatform.gitbooks.io/api/content/mobile-variables/inside-a-business-component-executed-on-the-mobile-app.html).

---



