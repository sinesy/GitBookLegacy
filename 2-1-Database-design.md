# Database design

In case you need to design a new database, it can be helpful to create tables having a common structure, in terms of field names and type.  
These are some rules that we suggest to follow:  
 **PRIMARY KEY** : You should not define fields called ID or FUNCTION in the DB, as they may conflict with some Javascript commands. A possible variant is to call ID\_ or \_ID, e.g. CUSTOMER\_ID, PRODUCT\_ID, etc.  
Every table must have either a primary key or unique keys.  
Platform does not replace the business analysis: this important task must be carried out before the development of the application, as well as the database design. Independently of the way an application will be developed, the analysis still plays a foundamental role in the development cycle of the application.  
 **DATABASE TYPES** : field types must be defined according to the database types; these are common types that can be used with Platform:

* Oracle database

  * NUMBER\(N\)

  * DATE

  * CHAR\(N\)

  * CLOB

* MS SQLServer database

  * NUMERIC\(N\)

  * DECIMAL\(M,N\)

  * DATE

  * DATETIME
  * NVARCHAR\(N\)
  * NCHAR\(N\)
  * TEXT

* MySQL database

  * NUMERIC\(N\)

  * DECIMAL\(M,N\)

  * DATE

  * DATETIME
  * VARCHAR\(N\)
  * CHAR\(N\)
  * TEXT

* PostgreSQL database

  * NUMERIC\(N\)

  * DECIMAL\(M,N\)

  * DATE

  * DATETIME
  * VARCHAR\(N\)
  * CHAR\(N\)
  * TEXT

Moreover, we suggest to define the database instance with a Unicode charset: this will ensure that characters typed using the GUI will be stored correctly into the database.

**IDENTITY FIELDS/SEQUENCES** : Oracle sequences are supported, as well as identity fields in SQLServer, PostgreSQL and MySQL

**STANDARD FIELDS TO INCLUDE IN ANY TABLE** : if you want to trace data creation/updating carried out by the users, a few fields should be added to each table; in the following list a series of fields are reported with type and meaning:

* USER\_ID\_CREATE VARCHAR\(255\)\)/NVARCHAR\(255\) – Platform can use this field to automatically store the user who is creating the record
* CREATE\_DATE DATE/DATETIME – Platform can use this field to automatically store the current date when creating a new record
* USER\_ID\_UPDATE VARCHAR\(255\)\)/NVARCHAR\(255\) – Platform can use this field to automatically store the user who is updating the record
* LAST\_UPDATE DATE/DATETIME – Platform can use this field to automatically store the current date when updating the current record
* ENABLED CHAR\(1\)/NCHAR\(1\) – Flag used to manage logical deletion of records: it can have S/N or Y/N values, used to filter a list of "valid" records, i.e. not logically deleted; when deleting a record, it will be marked as logically deleted \(flag set to ‘N’\), i.e. not actually removed from the database, but just updated to the ‘N’ value
* ROW\_VERSION NUMBER\(12\)/NUMERIC\(12\) – Numeric field used to manage concurrent updates to the same record from different users: each time the record is updated by a specific user, Platform will automatically increase the value of this field and will forbit the next update if the record to update will not have the ROW\_VERSION value aligned to the most refreshed value: this behavior will avoid to have inconsistent data stored into the database due to different users working on old data.

**DATA PARTITION** : according to the database and data visibility, there are scenarios where data must be partitioned according to the user. That means that \(all\) tables should contain an additional field in the primary key used to filter data according to the current user.

Furthermore, in case of an "application service provider" installation, where the same database should be used to serve different organizations sharing the same database structure but NOT the same data, data must be partitioned according to the organization \(i.e. a set of users beloning to the same organization\). That means that all tables should contain an additional field in the primary key used to filter data according to the organization the user belongs to.  
These two needs are both supported by Platform, through two additional fields to add to all tables as part of the primary key:

* COMPANY\_ID CHAR\(1\)/NCHAR\(1\) NOT NULL – this field represents the organization; users belonging to the same organization will be defined using the same COMPANY\_ID value
* SITE\_ID NUMBER\(5\)/NUMERIC\(5\) NOT NULL – this field represents the property of a record; different records could have different values of SITE\_ID \(e.g. 00000,00001,00002 etc\); in this way, a user could be granted to read \(and/or write\) records having SITE\_ID 00000 or 00001 but not 00002.

**PERFORMANCE ISSUES** :  
When working with databases, there can be performance issues involved with the execution of SQL queries.  
It is important to being aware of these issues and the right way to deal with them:

* **total number of records –**  usually a business component for lists executes two SQL queries: the first is the real query used to fetch the first block of data, the second is a SELECT COUNT\(\*\) FROM … used to recon the total number of records composing the result set. This information is used to show on the grid the total number of records and allow the scrolling among the pages of data until the last block of data. The second query can consume a significant amount of time with a very large table content: in this scenario it would be better to disable the execution of the second query. In order to do it, open the business component for list, click of the “Panels” subfolder and open all grids depending on that business component: in the grid definition window, you can see a check box named “Do not count records”: when selecting it, the second query will be disabled
* **where conditions on not indexed fields**  – a very common scenario when a SQL query sounds slow is when there are WHERE conditions working on fields which have not been declared as indexed. Consequently the database cannot optimize the query to quickly fetch data. In such a scenario, try to add indexes to those fields.
* **where UPPER conditions on fields**  – pay attention to the filtering conditions applied to columns in grid. If you declare this filtering conditions as NOT case-sensitive, it means that Platform will apply automatically an UPPER function to the field, like in this example: SELECT \* FROM TABLE WHERE UPPER\(FIELD\) = ‘TEXTINUPPERCASE’ . Unless you have defined a complex index on the UPPER function for that field, the database will not perform a fast query.
* **queries with binding variables**  vs queries without binding variables – it is  **not correct comparing**  the executing time of a query executed with Platform using binding variables \(e.g. SELECT FIELD1 FROM TABLE WHERE FIELD2 = ? \) with the same query executed through an external SQL client where the binding variables have been replaced with in-line values: they query is not the same and consequently also the execution time! Pay attention to the where conditions, otherwise you can lead to the wrong result that the query in Platform is slow “for some reason”
* **CHAR type field in Oracle database**  – in case of Oracle database and a SQL query having a WHERE condition on CHAR type fields, it could happen that the SQL query seems slower: sometimes the performance can be improved in this scenario when replacing the binding variable on the CHAR field with an in-line value. You can force the execution of business component for list without the use of binding variables, by unchecking the checkbox named “Bind variables” in he business component definition window
* **the same query, executed multiple times**  – if you execute a SQL query in Platform and it seems slow and a few seconds after you execute exactly the same query on an external SQL client and here it is faster: bear in mind that a database is able to cache the result after the first execution of the query, so it could be wrong to compare the execution time described in this scenario! Try to invert the query executions: first on the SQL client, then on Platform: what about the resulting time?
* **fetch size when extracting data from a query**  – if you are executing a SQL query with a server-side js component and you are processing the whole result and this operation requires several seconds or minutes, but when executing the query on an external SQL client you can see the results instantly,, remember that it is likely the the SQL client is showing you only a porting of the whole data: that is the reason why it is faster; try to scroll all data shown on the SQL client until the end of the resultset: how long does it take?

## Maintenance

It is not advisable to rename PK columns in a table. The application uses the PK fields to generate unique keys as well as to set the parameters of input/output for windows and panels.  
If you decide to change the primary keys fields, you have to align the data model, through the ad hoc button available in the detail model form and then manually align the input/output parameters folder of panes using that object.

---



