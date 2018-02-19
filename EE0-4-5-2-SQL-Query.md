# SQL Query

A Service task can used to perform a SQL query, in order to get one or more rows and use this data to fill in process properties and refer them in any other part of the process.  
Required properties are:

* Id and Name: they identify the task and they are mandatory; be sure NOT to include accents in these fields \(only alphanumeric characters are allowed\).
* Documentation: an optional description of this task
* Class:  **it.sinesy.activiti.services.ExecuteSqlQueryServiceTask** 
* Class fields: in this list of fields, a set of properties must be defined, in order to correctly define the SQL query to execute:

* name: property name to refer

* string value: value to assign to that property
* expression: optional expression to set, e.g.  ${VARIABLE == ’Test’ ? YES : ’NO’}

A mandatory couple name-value is:

* " **sql** " – the SQL query to execute; the records read will be stored in a process variable named "result", expressed in JSON format:

```js
[{ "field1": "value1", … },{ … },...}]
```

* " **result** " – optional variable used to store the result set in another process variable

A typical SQL query execution would contain the following couples name-value:  
name = sql  
string value = select name,surname from users where username=:USER\_ID

**Important note**   
Do NOT use the notation ${VARNAME} in a SQL query: you have to use the notation :VARNAME instead.

Important note  
If you want to refer the outcome provided by the query execution and stored in a variable named as specified by the "result" field, you have to pay attention to the format of such an outcome.  
For example, you could have defined a field "result" = "MY\_QUERY" and the query execution could return something like:

```js
[{ "FIELD1": "...", … },{ … },...}]
```

Consequently, if you are within a JavaScript service task and need to access to the value for "FIELD1", this is the right instruction to write:

```js
var myVariable = ${MY_QUERY[0].FIELD1}
```

If you want to let the rest of the process access to such a value, you have to store it as a process variable, using this instruction:

```js
execution.setVariable("FIELD1", myVariable);
```

**Additional properties** :

* name = dataSourceName
* value = additional datasource id defined within 4WS.Platform and used to access to a different database schema, instead of the default repository schema used by 4WS.Platform and Activiti.

---



