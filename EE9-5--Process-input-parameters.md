# Process input parameters

Optionally, a process definition can include one or more input parameters.  
Typically, these parameters should have a text type, as for a shell command. There could be some cases where a different type can be needed, as for a Java Business component, where a Java programmer could declare different input types \(e.g. Number, Date,…\).

For this reason, for each parameter a "Type" must be defined. Supported types are: Text, Number, Date and Date+time.  
According to the selected type, a value must be filled in: the columns "Text", "Number", "Date/Date time", "Enum" \(String only comma separated values, since 6.0.1 version\) can be used alternatively, with regards to the parameter type.  
The "Description" column is not actually used by the process: it is only provides a description within the scheduled process, to make it easy to figure out the meaning of that parameter.

---



