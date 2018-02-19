The App Designer includes a few functionalities useful for the every day monitoring activities and settings:
Mobile devices
To do list
Sync process History
Files upload
Analytics Events
Mobile Table creation
Dispatch file to users

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image21.png)

|   |
| :--- |

 **Mobile devices**  &#8211; list of the registered mobile devices, i.e. the ones which have been connected to the server-side at least once.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image14.png)

|   |
| :--- |

Since every user could own multiple devices (e.g. both a smartphone and a tablet), 4WS.Platform allows to use the same credentials (the same username) with different devices. Each device is identified by a device id. The device type is also recorded.
 **To do list**  &#8211; Optional filtering conditions to apply when extracting data from the central site and put them to device; the table behind this functionality is not directly used by Platform: an ETL extraction job should be developed to extract data from a central information system and it can use that table to apply the correct filters.
 **Sync process History ** &#8211; A list of all synchronizations is reported: for each device it is possible to see when it started, ended, the duration and the amount of data sent/recevied (expressed in bytes).

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image13.png)

|   |
| :--- |

 **Files upload ** &#8211; this can be considered an emergency feature: it allows to quickly upload one or more files in order to make them available for all the devices, if not sent yet.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image06.png)

|   |
| :--- |

The uploded file must be in .zip format. Platform will decompress it and analyze each file contained in the zip. For each file, the "SQL update statement" will be executed.
This SQL instruction should have this format:
update table set imagename=? where pk=?
Basically, this statement will check if the file under analysys has been already processed and sent in the past. If the statement execution will process zero rows, then the file will be ignored, otherwise, if not processed yet, the file will be indexed and processed as to send for all users.
Any new user will recevice the file too.
 **Analytics Events ** &#8211; Platform mobile supports a series of events thsat can be captured when the user is working on the app and send them to Google Analytics.
In order to use it, Google Analytics account must be set up before. Once done that, it is possible to activate one or more events to capture.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image17.png)

|   |
| :--- |

 **Mobile Table creation**  &#8211; this is a very common need: extracting data from one or more tables from a central information system, such as a database, reduce the data amount in terms of fields and in terms of records to send (through a filtering condition) and make it available to all devices, by recreating the simplified table structure and data,

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image18.png)

|   |
| :--- |

This functionality allows to make it possible, through the definition of a series of settings:
Starting SQL Query &#8211; the extraction query, including a filtering condition, to execute on the central database identified by the "Data source"
Data source &#8211; if not specified, the "Starting SQL query" will be executed on the main database schema (the repotory schema used by Platform); if specified, extracted data will be retrieved in that data source
Table name &#8211; the mobile table name; that table will be automatically created by Platform in the mobile device, when synchronizing data and structures; its structure will be automatically defined by Platform starting from the field types specified in the select clause of the starting SQL query
Sync data &#8211; if this flag is selected, then data will be synchronized automatically
Primary key fields &#8211; when loosing focus from the "Starting SQL query" field, the SQL query will be executed and the list of fields specified in the selected clause is showed in this grid: it is mandatory to select at least of field with represents the primary key for the new mobile table; in this way, Platform will be able to manage writing operations like updates and deletes of the mobile table.
Important note: ff the filtering condition expressed in the "Starting SQL query" input field contains variables expressed as :XXX, then data will be extracted multiple times, one for each device, accoding to the value of the variablesfor each user. Different users could have different values associated for those variables and hence extracted data would be different too.
Supported variables are: COMPANY_ID, SITE_ID, USERNAME, LANGUAGE_ID.
 **Dispatch file to users**  &#8211; this can be considered an emergency feature: it allows to quickly upload a file in order to make it available for all the devices.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image03.png)

|   |
| :--- |


                

---


