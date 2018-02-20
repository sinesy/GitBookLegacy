This is an optional field: if the field has been filled in with a command to process \(e.g. a .sh or .bat command\), then that command will be executed every time a device starts a sync process, but after that data read from the device has been stored to the central "border tables".  
It can be used attach a custom import job to move data coming from the devices to the final legacy central database. A job can be defined and it can use two kind of tables: the border table "copy of the mobile table" and its M\_xxx table, containing the SQL operation it is related to \(insert, update, delete\). In this way, a job has all the data needed to perform the right business logic on the final database.

---



