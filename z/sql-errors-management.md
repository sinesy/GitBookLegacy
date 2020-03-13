# SQL errors management

When working with a database, it is possible to bump into SQL errors fired by a specific database, when writing data \(insert, updates, deletes\).

Each database has its own error codes and meanings.

Platform provides a feature within the AppDesigner, focused on showing a more user friendly error message, instead of the one provided by the database.

Through **Administration -&gt; SQL Errors**, you can define the error codes and corresponding error messages, for each supported language.

![](/assets/sqlerror.png)

These messages must be defined starting from:

* **database type** \(DB2, Oracle, MS SqlServer, MySQL, PostgreSQL\)
* **error code**, i.e. a numeric value provided by the database, specific for an error; you can figure out which value it has by looking at the server-side log, when a SQL error is fired by the database; check out for "SQL error" patterns in the server log
* optionally you can also specify a **SQL message**, which will be searched by Platform in the original SQL error message: it is matches inside the original error, then the corresponding error message will be shown

Each time Platform finds an error code defined in this feature, for the specific database in use, it will replace the original error message with the one \(translated\) provided through this feature.









