# Appendix : Synchronization flow

The sync process is composed of the following steps:

* the mobile device has to authenticate to the Platform central server, where the mobile app has been configured
* the mobile device privides to Platform its current database version and application version, so that Platform can figure out whether metadata are required to the device to be updated to the last application version or if DDL instructions are needed to the device to upgrade its database repository
* the mobile device updates its database repository and metadata \(if needed\)
* the mobile device requests for DDL and DML files to update its application local database and data \(if needed\); these files are read from the central server’s "to\_send subfolder linked to the specific device
* the mobile device performs all the DDL and DML operations, by executing all the DDL operations first, than by grouping all DML files by table and creation date, then execute them on separated thread, in order to speed up the process of local database preparation
* the mobile device will send to the central server all data generated locally that will be saved on the central server in the "received" subfolder linked to the current device
* the mobile device will ask for all custom files, to store locally within the "customFiles" subfolder, used by the rest of the app to show icons or other static custom content \(navigation buttons, loader, HTML used by the about window, etc.\)
* the mobile device will ask for all application files not downloaded yet, as for images, PDFs, etc.

---



