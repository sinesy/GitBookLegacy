# Server-side functionalities

The App Designer includes a few functionalities useful for the every day monitoring activities and settings:

* Read-write table
* Read only tables
* Mobile devices
* Sync process History
* Upload APK
* Upload IPA
* Analytics Events
* Android App Creation
* iOS App Creation

![](/assets/menu.png)

---

#### **Read-write tables**

This is a very common need: extracting data from one or more tables from a central information system, such as a database, reduce the data amount in terms of fields and in terms of records to send \(through a filtering condition\) and make it available to all devices, by recreating the simplified table structure and data.

![](/assets/rw.png)

This functionality requires a few settings:

* **Starting SQL Query **– the extraction query, including a filtering condition, to execute on the central database identified by the "Data source"; if the expressed filtering condition  contains variables expressed as :XXX, then data will be extracted multiple times, one for each device, according to the value of the variables for each user. Different users could have different values associated for those variables and hence extracted data would be different too. Supported variables are: COMPANY\_ID, SITE\_ID, USERNAME, LANGUAGE\_ID.

* **Table name** – the mobile table name; such table will be automatically created by Platform in the mobile device, when synchronizing data and structures; its structure will be automatically defined by Platform starting from the field types specified in the select clause of the starting SQL query

* **Data source** – if not specified, the "Starting SQL query" will be executed on the main database schema \(the repository schema used by Platform\); if specified, extracted data will be retrieved in that data source

* **Sync data** – if this flag is selected, data will be synchronized automatically \(it should be the default option\)

* **Data target** –for every configured read-write table, a copy of such table will be created on the server as well: this copy is needed in order to prepare all data to send to all devices and also to receive all changes produced by devices and collect them in a unique central place. If not specified, such copy of the mobile table will be created on the main database schema \(the repository schema used by Platform\); if specified, the copy of the mobile table will be created in that data source
* **Primary key fields **– when loosing focus from the "Starting SQL query" field, the SQL query will be executed and the list of fields specified in the selected clause is showed in this grid: it is mandatory to select at least one field with represents the primary key for the new mobile table; in this way, Platform will be able to manage writing operations like updates and deletes of the mobile table. _Pay attention to the correct definition of this primary key: once created, it cannot be changed any more_! 

---

#### **Read-only tables**

This is a very common need: extracting data from a specific central table and send its content to all devices. Such data is used only to select data or fill in forms in the mobile app: it is readonly and never changes from the device perspective. It can be filtered, in case not all data must be sent or must be sent with different filtering conditions, according to the user.

![](/assets/ro.png)

This functionality requires a few settings:

* **Table name** – the server table name to use for extracting data to send to mobile devices; such table will be automatically created by Platform in the mobile device, when synchronizing data and structures; its structure will be automatically defined by Platform starting from the selected server table; such table comes from the selected "Data source".
* **WHERE Filter **– optional input field used to filter data to send to the mobile devices; it does NOT have to include the WHERE keyword; if the expressed filtering condition contains variables expressed as :XXX, then data will be extracted multiple times, one for each device, according to the value of the variables for each user. Different users could have different values associated for those variables and hence extracted data would be different too. Supported variables are: COMPANY\_ID, SITE\_ID, USERNAME, LANGUAGE\_ID.

* **Data source** – if not specified, the selected table belongs to the main database schema \(the repository schema used by Platform\); if specified, the selected table is part of the selected data source

* **Action to avoid data sync **– this is an optional field; if specified, it is a server-side javascript action used to figure out if data on the server table has changed: only if data has changed, the read-only table will be sent again to the mobile app: its previous content on the mobile side is completely cleared up and replaced by the new one. This feature is very helpful in case of very large table content \(10.000 records or more\) and it is not recommended to sent such content at every mobile synchronization, because of the long waiting time required to send large content from the server to the client. Suppose to provide server data which only changes during the night: it would be useless to send for every sync during the day; an javascript action could be used to decide if the content for the server table has changed, for example by comparing last device sync time with the last updated recod in the central table.

Content of the "Action to avoid data sync"

```js
var outcome = "true"; // sync for the read-only table will be carried out
if (some condition) {
  outcome = "false"; // do not sync data again, since the device already owns an updated version of it
}

utils.setReturnValue(outcome);
```

A typical scenario for such an action is comparing last sync time for the device with some other time, related to the table content. The last snyc time for the device can be fetched in this way:

```js
    var response = utils.executeQuery(
        "SELECT MAX(START_DATE) AS START_DATE " + 
        "FROM CON46_SYNC_HISTORY " + 
        "WHERE APPLICATION_ID=? AND DEVICE_ID=? AND SYNC_STATE <> ? ",
        null, false, true, 
        [userInfo.applicationId, reqParams.deviceId, 'STARTED']
    );
    var risp = JSON.parse(response);
    if(risp.length == 1) {
        lastSyncDate = risp[0].startDate;
        // do something with this info... 
    }
```

Note: you can skip the scriptlet described above, since Platform already passes forward such data in the reqParams input object, through an attribute named lastSyncDate, so the code reported above can be simplified as:

```js
     var lastSyncDate = reqParams.lastSyncDate;
```





Suppose your central table contains a LAST\_UPDATE datetime field: you can use it to get the last modified record time and compare it with the "lastSyncDate":

```js
        if(lastSyncDate != null) {

            var response = utils.executeQuery(
                "SELECT MAX(LAST_UPDATE) AS LAST_LOAD_DATA_DATE " + 
                "FROM MYCENTRALTABLE ",
                ..., // data source id
                false, true, null
            );
            var list = JSON.parse(response);
            if(list.length == 1) {
                var lastLoadDataDate = list[0].lastLoadDataDate;                    
                if(lastLoadDataDate != null) {
                    lastLoadDataDate = utils.addDate(lastLoadDataDate.substring(0, 19), 'yyyy-MM-dd HH:mm:ss', 'DAY', 0);
                    lastSyncDate = utils.addDate(lastSyncDate.substring(0, 19), 'yyyy-MM-dd HH:mm:ss', 'DAY', 0); // convert it to a javascript Date

                    if(lastSyncDate >= lastLoadDataDate) {
                        outcome = "false";
                    }
                }
            }
        }
```

---

#### **Mobile devices**

Show the list of the registered mobile devices, i.e. the ones which have been connected to the server-side at least once.

![](/assets/devices.png)

Since every user could own multiple devices \(e.g. both a smartphone and a tablet\), 4WS.Platform allows to use the same credentials \(the same username\) with different devices. Each device is identified by a device id. The device type is also recorded.

A double click of a row in this grid will open a detail window containing the list of all synchronization processes already performed:

![](/assets/snyc.png)

This sync history is particularly helpful to figure out problems related to the sync for a specific mobile device. Typical errors involved with mobile devices are:

* a very slow performance when synchronizing data which always happens, for all attempts; this can depend on a bad internet connection involved with the device; in order to prove it to the end user, you can look at the last columns in this grid: they reports the transfer rate both for upload and download: if they are always very low \(a few kbytes per second or ever worse\), it means there is a problem with the internet connection of that device
* a very slow performance when synchronizing data which happens only sometimes; in many cases, this is due to a bad internet connection involved with the device in the moment when the user was synchronizing; in order to prove it to the end user, you can look at the last columns in this grid for the time the user has reported a problem: they reports the transfer rate both for upload and download: if they are always very low \(a few kbytes per second or ever worse\), it means there is a problem with the internet connection of that device.

The folder named "**Errors when aligning central tables**" reports all errors fired during the mobile synchronization and the SQL instruction having errors, if there is any.

![](/assets/erros.png)

---

#### Sync process history

This is the same functionality described in the previous section: here all processes for all devices is reported in a single grid, whereas in the previous section is limited to the selected device only.

---

#### Upload APK

This functionality allows to upload a .apk file \(the Android mobile app\) in the central repository, in order to make it available to all devices which can download it and upgrade themselves.

![](/assets/and.png)

Platform provides this feature in order to update itself when launching the app in the mobile device: the first step for the app is checking out on the server side if there is an app update available and prompt it to the user. Here it is possible to specify whether the update is mandatory or not, though the "Mandatory" checkbox: a mandatory update means that the app does not allow to use it any more, until the user has downloaded and update the app, in order to maintain consistency between the app functionalities and the ones on the server-side. It is not always required to select the check box and force the user to update the app, in case there are not inconsistencies at data level, as for the case of an update including only bug fixes or improvements at UI level.

This feature can be used only along with an application parameter named "**Directory of Android apk \(Directory id or absolute path\)**" available in the **MOBILE** section. Basically, you have first to define a directory \(Administration -&gt; Directories\) where these files will be stored \(e.g. in the server file system or in Google Cloud Storage\) and then set the directory id in the application parameter. In this way, when uploading the .apk file, this will be stored in such a path.

After that, the mobile app will retrieve it form the same place.

---

#### Upload IPA

This functionality allows to upload a. ipa file \(the iOS mobile app\) in the central repository, in order to make it available to all devices which can download it and upgrade themselves.

![](/assets/ios.png)

Platform provides this feature in order to update itself when launching the app in the mobile device: the first step for the app is checking out on the server side if there is an app update available and prompt it to the user. Here it is possible to specify whether the update is mandatory or not, though the "Mandatory" checkbox: a mandatory update means that the app does not allow to use it any more, until the user has downloaded and update the app, in order to maintain consistency between the app functionalities and the ones on the server-side. It is not always required to select the check box and force the user to update the app, in case there are not inconsistencies at data level, as for the case of an update including only bug fixes or improvements at UI level.

This feature can be used only along with an application parameter named "**Directory of iOS ipa \(Directory id or absolute path\)**" available in the **MOBILE** section. Basically, you have first to define a directory \(Administration -&gt; Directories\) where these files will be stored \(e.g. in the server file system or in Google Cloud Storage\) and then set the directory id in the application parameter. In this way, when uploading the .ipa file, this will be stored in such a path.

After that, the mobile app will retrieve it form the same place.

---

#### **Analytics Events**

Platform mobile supports a series of events that can be captured when the user is working on the app and send them to Google Analytics.  
In order to use it, Google Analytics account must be set up before. Once done that, it is possible to activate one or more events to capture.

![](/assets/ana.png)

