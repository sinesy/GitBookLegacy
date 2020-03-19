# Files management

Optionally, the sync process can include the chance to send any kind of files from the central server to each mobile device \(e.g. PDFs, images, etc\).  
Independently of the kind of files to send, on the central server two steps are required:   
saving files somewhere in a central area and make them available to the central server in order to send them to each device  
indexing these files for each user, so that every user linked to a specific device could receive different files if needed, according to a custom logic; since a user could own more than one device \(for instance, both a smartphone and a tablet\), files must be sent per device id and not per user id, since the sync process is different for each device.

The files indexing process is managed through a couple of tables: CON54\_FILES\_TO\_SEND and CON55\_USER\_FILES.  
The first stores all files to send, independently of the devices or users to sent to. The latter link a specific file defined in the first table for each device.  
Consequently, at the end of a specific sync process, the second table is cleaned up for the portion of files just sent to the user.

The table structure for CON54\_FILES\_TO\_SEND includes these fields and default values:

| APPLICATION\_ID FILE\_ID – absolute path including the file name, in case the file is stored on the file system or the file id in a remote storage \(e.g. Google file storage or Alfresco ECM\) SOURCE\_ID – e.g. FILE\_SYSTEM SHARED\_FILE – Y | N FILE\_NAME – file name FILE\_TYPE – not managed; e.g. PDF, PNG, JPG, etc. ROW\_VERSION USER\_ID\_CREATE CREATE\_DATE USER\_ID\_UPDATE LAST\_UPDATE STATUS |
| :--- | :--- |


La table structure for CON55\_USER\_FILES is as follows:

| APPLICATION\_ID FILE\_ID – see the previous table field description DEVICE\_ID – device id ROW\_VERSION USER\_ID\_CREATE CREATE\_DATE USER\_ID\_UPDATE LAST\_UPDATE STATUS |
| :--- |


---



