# How to create a new mobile app

In order to create a new mobile app, these steps are needed:

* use the App Designer to create a new mobile app and specify an APPLICATION\_ID, a menu type, the app colors and at least  **the sync folder path** .
* once created the empty app, the App Designer must be used to define:

* objects

* business components \(online or offline\); only if a b.c. is declared to work offline, an offline table is required; offline tables creation and data sync are managed using the ad hoc feature called "Mobile table creation" available in the "Mobile" menu of the App Designer

* panels
* windows; windows can be optimized per device display size: they can be showed for tablets only, smartphone only or both
* menu items; note that all menu items have one level only: do not create subfilders
* other stuff, such as actions and events

On-line apps  
The easiest way to configure a mobile app is to create on-line functionalities, that is to say, panels and windows whose content is retrieved and sent to the central server, where an installation of 4WS.Platform is available.  
In this scenario, the synchronization task is only related to synchronizing metadata, i.e. the UI and behaviour of the app, not data or data structures, since these reside on the central server.

Off-line apps  
A more complex scenario includes the creation and alignment over time of mobile tables, whose data comes from the central site or can be managed/created directly on the mobile app and then optionally sent to the central site. In order to make it possible, it is needed to define which tables and data to “move” to the device and which data extraction policy to apply.  
Platform provides two alternative waysto create automatically server-side tables to a mobile app and synchronize data among them:

* synchronize  **only changes**  generated on the server-side table and move them to the device table and the opposite
* synchronize t **he whole content**  of a table, by replacing the previous content with the new one

The first approach is helpful when you want to minimize the amount of data to send, since it is restricted only to records really changed.  
The second approach comes in handy when youhave a huge amount of data to send and the changes identification task would spend too much time to get the changes. In such a scenario, it would be better to send the whole content, by deleting everything and replace it with the new one.  
Consequently, the second solution can only be applied for readonly data, since any change coming from the device would be lost the next time the sync process starts.

Synchronize only changes  
The ad hoc feature called " **Mobile table creation** " available in the "Mobile" menu of the App Designer can be used to automate the creation of thesetables and data.  
What is not covered is the alignment of the legacy tables from data stored in the "border tables" in the central server; if needed, this task must be managed externally, using ad hoc integration tools like Talend. An exception is represented by the case the extraction query only works on a single table: in such a case, the alignment is on both sides: from the central site to the device and the opposite.  
Optional jobs must be created outside the Platform environment, in case a custom sync logic is needed from device to the central site.

For each "Mobile table creation" execution, a couple of "border tables" are created in the central server; the structure of the first "border table" mantains the same names and types of the SELECT clause specified in the "Mobile table creation" feature.  
The typical "border table" has the following structure:

```js
(pk) field1
(pk) field2,
(pk) ...
fieldX
fieldX+1
...
```

The corresponding M\_xxx table has the following structure:

```js
(pk) field1
(pk) field2,
(pk) ...
(pk) operation type
(pk) storing data
(pk) device id
```

where the operation type can have the following values: I, U o D \(insert, update or delete\).  
By matching data coming from these two tables, it is possible to create on the fly SQL operations to carry out on a legacy database, within a custom import job.  
Apart from the creation of these two "border tables", for each "Mobile table creation" execution, additional files are also created and mantained:

* a ddl\_xxx.sql file is created inside the "common" subfoder, in order to automate the creation of the same tables offline, in each device
* zero or more dml\_xx.sql files are created every time changes in data coming from the legacy database are available; these files will be sent to each device; only in case the SQL query specified in the "Mobile table creation" feature contains :USERNAME or other predefined variables, the creation of the dml\_xxx.sql are postponed to the specific sync process with a device and filled accoding to the variable values linked to each device: that means that it is posssible to send different data to different devices.

Synchronize the whole content  
The ad hoc feature called " **Sync central table** " available in the "Mobile" menu of the App Designer can be used to automate the creation of thesetables and data which are readonly: do not use this feature to work on data that you want to write from within the mobile app. If this is your need, you have to use the first functionality described above, which works on changes applied on the central site and on mobile devices and only synchronizes these ones.  
The “Sync central table”feature extract all data from the table and move it to an equivalent mobiletable, after deleting the previous content. The mobile table has the same data structure of the one available on the server-side.  
When configuring this task, you can optionally apply a SQL filtering condition to reduce the amount of data to extract. Filtering conditions can also includes some variables, like :USERNAME, :COMPANY\_ID, :SITE\_ID, :LANGUAGE\_ID  
Optionally, you can also define a ** server-side js action**  used to figure out whether data can be extracted or not: you can use such an action to execute SQL queries to make such decision and return false in case you want to skip the sync task for this table. For example, you could refresh data on the server side every night, so it would be useless and time consuming sync the same data for the whole day, since it will not change until the day after!  
The server-side js action can be used to compare the last sync date for the device with the “last refreshed data” for the table on the central site, as long as this date is available.  
Two input variables are available and can be referred within the action class:

* **lastSyncDate**  – expressed as a String having format “yyyy-MM-dd HH:mm:ss”, related to the last sync date for that device; null in case it is the first time

* **deviceId**  – the device unique identifier

This is an example of how to define this action:

```js
var deviceId = reqParams.deviceId;
var lastSyncDate = reqParams.lastSyncDate;
var json = utils.executeQuery("select...", null, false,true,[...]);
var list = eval("("+json+")");
....

if (...)
  utils.setReturnValue("true"); // go on with the data extraction
else
  utils.setReturnValue("false"); // skip the data extraction
```

Authentication and authorization  
 **Users and roles**  must be defined to work with the mobile app; users and roles must NOT be defined using the App Designer but the interpreted web application corresponding to the mobile app

First Deploy  
The initial empty mobile app must be created using the ad hoc feature provided within the "Mobile" menu of the App Designer: " **Create an iOS app** " or " **Create an Android app** ".

---



