# Synchronization folder

This path is mandatory: it represents an absolute path in the Platform server file system, where all required files for the app are stored and used during the synchronization process between Platform server and the mobile devices.  
Typically, this base folder contains the following subfolders:

"sync" – folder where are stored the files related to the synchronization settings, one file for each extraction logic \(mobile table\) to create; these files are created using the "Mobile table creation" menu item. Platform server automatically reads all these files and prepares data/data structures for all the mobile devices, in order to send data to the devices and to manage data coming from them; data are fetched starting from a central database where a SQL extraction query is performed. A file stored in this folder must have the following format:

```
SELECT COD_ART,DESCRIZIONE,PREZZO,STATUS FROM LISTINO_RICAMBI COD_ART SELECT * FROM LISTINO_RIC WHERE COD_ART=? 
INSERT INTO LISTINO_RIC(COD_ART,DESCRIZIONE,PREZZO,STATUS) VALUES (?,?,?,?) UPDATE LISTINO_RIC SET COD_ART=?,
DESCRIZIONE=?,PREZZO=?,STATUS=? WHERE COD_ART=? INSERT INTO L_LISTINO_RIC(LOG_DATE,OP_TYPE,USER_CODE_ID,COD_ART) 
VALUES(?,?,?,?) 1
```

A data import job is created for each file stored in this folder; this job reads data from the starting database and creates insert/update SQL operations and write these records in the border table created along with the file. The job figures out whether creating a SQL insert or update by reading data from the source database and for each record it checks if the record exists or not in the border table. Every mobile device will have the same table locally.

Important note: it is not a good idea to create mobile tables having a huge number of fields, because the limited resources available on a mobile device; consequently the mobile table should not have the same structure of the corresponding table in the central database, if this one has a large number of fields.  
The first list in the file is the SQL query to execute in the legacy system. It can contain joins with other tables if needed, but every field having the same name in different tables must be defined in the select clause through an alias which would ensure a unique name in the select.  
Each field reported in the select clause represents a field created in the border table.  
However, the resulting border table should have fewer fields than the original ones, so it is essential that the select does not have too many fields.  
For each border table defined, 4WS.Platform will create a configuration file having the same name; for instance: for a table having name "PRICELIST", there will be a file named "PRICELIST.sql"  
The second line in the file represents the fields list which compose the primary key of the border, separated by a comma.  
The third line is the SQL query executed on the border table to check out whether a specific record to import from the lagacy system is already stored in the border table and decide if an insert or update operation is required toimprot fresh data.  
The forth line contains the SQL insert operation to perform in the border table, in case the record to import from the legacy system is not stored in the border table yet.  
The fifth line contains the SQL update operation to perform in the border table, in case the record to import from the legacy system is already stored in the border table.  
The sixth line is a SQL operation used to log the operation on an auxiliary table named L\_"bordertable".  
The last line reports the positions of the primary key fields within the select clause.

"common" – this folder contains ddl_xxx.sql and dml\_xxx.sql files created starting from the data import job and coming from the legacy system: for each configuration file defined in the "sync" subfolder, a corresponding import job will be carried out and the following operations will be executed:  
update of the corresponding border table  
update of the corresponding L_"bordertable"  
generation of a dml\_xxx.sql file containing the same SQL instructions performed in the border table when importing data from the legacy system;   
all these files will be sent to every device at the first synchronization and copied into "dml\_scripts/user/device/to\_send" just before trasmitting them to the mobile device  
for each previously registered device \(which has already executed the first synchronization\), the single dml\_xxx-sql file will b copied to the folder "dml\_scripts/utente/device/to\_send".  
 **"dml\_scripts" **   
user 1  
deviceid1  
"to\_send" – folder containing SQL script files to send  
"sent"- folder containing SQL script files already sent  
"received" – folder containing received SQL script files  
"processed" – folder containing SQL script files already received and processed  
deviceid2  
…  
user 2  
…  
user N

All the content of the "to\_send" folder will be compressed and sent to the related device during the sychronization. If the sync process successfully completes, then the same content will be moved to the "sent" folder; that folder can be automatically emptied after a certain amount of days, which can be defined through the "Data deleting wait time" parameter, available in the application detail window.

All files coming from the device are saved in the "received" folder.  
If the "File reading" parameter available in the application detail window has been defined, then just after the completion of the writing process of these files the command specified through this parameter will be executed. This comand should be used to externally process the data coming from the device and then move these files to the "processed" folder.  
In case that parameter has not been defined, an automatic data import job will be performed for each configuration file found within the "sync" subfolder; this automatic job will take into account files having format XXX.sql where XXX is the name of the corresponding border table. If the file is read and process successfully, then the file is also moved to the "processed" folder.

"logs"  
user 1  
deviceid1  
"central\_logs" – log folder related to errors generated on the central side  
"device\_logs" – log folder related to errors generated on the device  
deviceid2  
…  
user 2  
…  
user N  
"files" – folder containing the files to send to the device and which will be saved on the "customFiles" folder of the device.  
user 1  
deviceid1  
"to\_send"  
"received"  
deviceid2  
…  
user 2  
…  
user N

This folder can be fed automatically, starting from the content of CON54 and CON55 tables: the first contains references to files which could be sent to all users, whereas the second defines which files to send to which users; files are sent on a device id basis, not on a user basis, since a single user could use multiple devices, each with its own files and synchronization tasks.  
The CON54 table includes not only files stored on the serfer file system, but also files stores on Alfresco CMS, thanks to the SOURCE\_ID table field, used to define which storage is used for the file \(allowed values: FILE\_SYSTEM o ALFRESCO\). These files are fetched and copied to the "to\_send" folder only during a synchronization process, in order to reduce the amount of space required on the file system of the server.

---



