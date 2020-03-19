# Files writing and reading

### Files writing

This is an optional field and the behavior of Platform changes according to the fact that the fields is empty or not:  
if the field has been filled in with a command to process \(e.g. a .sh or .bat command\), then the internal Platform Mobile Scheduler will automatically execute that command on a regular basis, every XXX seconds specified through the "imp/exp data wait time" field; if the  "imp/exp data wait time" has not been specified, it is assumed to be 1 hour  
if the field has not beed filled in, then the "sync folder" path is taken into account and for each .sql file found within its "sync" subfolder, the corresponding job will be executed; this job will read the .sql file and read data from a legacy system and produce a new data file named dml\_xxx.sql created in the "common" subfolder. The dml file contains all data to send to each device which has not been sent yet, since last sync. Once a device starts a new sync process, the content of the dml file is read and sent to the device and copied also to "to\_send" subfolder, to create a backup of all data sent to every device.

### Files reading

This is an optional field: if the field has been filled in with a command to process \(e.g. a .sh or .bat command\), then that command will be executed every time a device starts a sync process, in order to read data sent by the device to the central Platfom server.

---



