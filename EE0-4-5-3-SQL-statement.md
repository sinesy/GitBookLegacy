# SQL statement

A Service task can used to perform a SQL statement, in order to execute a writing operation on a database table \(insert, update, delete, ..\).  
Required properties are:

* Id and Name: they identify the task and they are mandatory; be sure NOT to include accents in these fields \(only alphanumeric characters are allowed\).
* Documentation: an optional description of this task
* Class:  **it.sinesy.activiti.services.ExecuteSqlStmtServiceTask** 
* Class fields: in this list of fields, a set of properties must be defined, in order to correctly define the SQL statement to execute:

* name: property name to refer

* string value: value to assign to that property
* expression: optional expression to set, e.g.  ${VARIABLE == ’Test’ ? YES : ’NO’}

A mandatory couple name-value is:

* " **sql** " – the SQL statement to execute
* " **result** " – optional variable used to store the number of processed records.

A typical SQL statement execution would contain the following couples name-value:

* name = sql
* string value = update users set expiration\_date=null where username=:USER\_ID

**Important note**   
Do NOT use the notation ${VARNAME} in a SQL statement: you have to use the notation :VARNAME instead.

Additional properties:

* name = dataSourceName
* value = additional datasource id defined within 4WS.Platform and used to access to a different database schema, instead of the default repository schema used by 4WS.Platform and Activiti.

---



