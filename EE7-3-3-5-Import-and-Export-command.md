# Import and export command

### Import command

This is an optional field and the behavior of Platform changes according to the fact that the fields is empty or not:  
if the field has been filled in with a command to process \(e.g. a .sh or .bat command\), then that command will be executed every time a device starts a sync process, but after that data from the central server has been prepared and sent to the device. Once the task of sending data to the device has been completed, data sent by the device to the central Platfom server is read from the "received" subfolder. Data read is write in "border tables" whose structure is similar to the one used my SqlLite database inside the devices. The import task represents a custom task, carried out by the command to invoke  
if the field has not beed filled in, then the "sync folder" path is taken into account and for each .sql file found within its "sync" subfolder, data is read from the device \(from the "received" subfolder\) and stored in the corresponding "border table" available in the central server.

### Export command

This is an optional field: if the field has been filled in with a command to process \(e.g. a .sh or .bat command\), then that command will be executed every time a device starts a sync process, but after that data read from the device has been stored to the central "border tables".  
It can be used attach a custom import job to move data coming from the devices to the final legacy central database. A job can be defined and it can use two kind of tables: the border table "copy of the mobile table" and its M\_xxx table, containing the SQL operation it is related to \(insert, update, delete\). In this way, a job has all the data needed to perform the right business logic on the final database.

---



