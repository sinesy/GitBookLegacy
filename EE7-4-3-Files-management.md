Optionally, the sync process can include the chance to send any kind of files from the central server to each mobile device (e.g. PDFs, images, etc).
Independently of the kind of files to send, on the central server two steps are required: 
saving files somewhere in a central area and make them available to the central server in order to send them to each device
indexing these files for each user, so that every user linked to a specific device could receive different files if needed, according to a custom logic; since a user could own more than one device (for instance, both a smartphone and a tablet), files must be sent per device id and not per user id, since the sync process is different for each device.

The files indexing process is managed through a couple of tables: CON54_FILES_TO_SEND and CON55_USER_FILES.
The first stores all files to send, independently of the devices or users to sent to. The latter link a specific file defined in the first table for each device.  
Consequently, at the end of a specific sync process, the second table is cleaned up for the portion of files just sent to the user.

The table structure for CON54_FILES_TO_SEND includes these fields and default values:

|  APPLICATION_ID FILE_ID &#8211; absolute path including the file name, in case the file is stored on the file system or the file id in a remote storage (e.g. Google file storage or Alfresco ECM) SOURCE_ID &#8211; e.g. FILE_SYSTEM SHARED_FILE &#8211; Y|N FILE_NAME &#8211; file name FILE_TYPE &#8211; not managed; e.g. PDF, PNG, JPG, etc. ROW_VERSION USER_ID_CREATE CREATE_DATE USER_ID_UPDATE LAST_UPDATE STATUS  |
| :--- |

La table structure for CON55_USER_FILES is as follows:

|  APPLICATION_ID FILE_ID &#8211; see the previous table field description DEVICE_ID &#8211; device id ROW_VERSION USER_ID_CREATE CREATE_DATE USER_ID_UPDATE LAST_UPDATE STATUS  |
| :--- |


                

---


