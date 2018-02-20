# Design Rules

**Limits**  
There are a series of limits in the use of datastore queries, so you are not free to define any kind of where conditions when retrieving data from a datastore entity: the GQL query language cannot be compared to the standard SQL.  
The main limits which come with Datastore are:

* no support for joins among entities
* a limited query language \(no support for exists, in, nested select, …\)
* no support for transactions over entities having different types
* it is possible to apply a filter in the where clause for one only field having a not equal operator \(&lt;, &gt;, &lt;=, &gt;=, &lt;&gt;\)
* limit to one only field when sorting data \(without an ad hoc file to define custom indexes\)
* custom index based on an ad hoc file: limit to one field with equal operator and one field with a not equal operator \(&lt;, &gt;, &lt;=, &gt;=, &lt;&gt;\); the consequence is that you can filter data by interval on a single field \(for instance by age between date 1 and date 2\), but you cannot filter data by interval if that interval is defined through two different fields \(for example filtering item prices valid between start\_date and end\_date\)
* custom index based on an ad hoc file: multiple sorting fields supported
* maximum number of custom indexes: 200

You can find some of these limits in the offical Google documentation:

[https://cloud.google.com/appengine/docs/java/datastore/queries](https://cloud.google.com/appengine/docs/java/datastore/queries)

**Design**   
In general, you cannot define joins between more entities.  
The consequence is that you can have difficulties in retrieving data stored in multiple entities and their aggregation to show them in a single list of data.  
Basically, there are two approaches to face with these limits:

* design the entities so that all the data needed for a specific list of data can be retrieved from a single entity. It means that tables must be denormalized, which is the opposite of what database designers usually do when defining a relational database
* use additional queries to get all data not belonging to the main entity; Platform allows you to execute any number of additional queries for each record read. That means you cannot use this technique when reading a large number of records: it is feasible only when you read a block of records, so that the total number of additional queries is limited.

**Indexes**   
When filtering or sorting data in a Google Datastore, not all filtering/sorting conditions are allowed. In some cases, additional indexes can be defined to support part of thefiltering/sorting conditions \(see the limits reported above\).  
This custom indexes can be defined outside Platform, since Google does not allow to define custom indexes outside the Google Development Console. A specific account to define indexes is required to access theGoogle Development Console.

**Unique indexes**   
Since the primary key in a Google Datastore entityis always composed of a single field, additional unique keys could be needed in case that field does not represent the “visible” identifying value, for instance when a collection represents a product or a client: in these cases, specific fields should contain unique values, as for a product code or a client id.  
Platform provides a “Unique indexes” folder to create them: in the App Designer, open the “Object” definition and select the “Unique indexes” folder: here you can create any number of unique indexes. Platform will check out the uniqueness for this combination of values each time a new insert or update operation is carried out.

**Common errors**   
There are the most common mistakes made when working with the Datastore and Platform:

* **error when loading data on a grid** ; check out the server-side log: probably there is a too complex where/order by clause and the Google Datastore is not able to manage it; try to simplify these clauses; you must take into account that sorting conditions require the definition of custom indexes; same for complex filtering conditions including not equals operators
* **error when applying a filtering condition through the quick filter panel on a grid or when clicking on a column header in order to sort by it** ; see the previous mistake: probably either a custom index is required or the Datastore is not able to manage such a complex where/sort clause
* **the query syntax is invalid** ; do not use an alias to refer the entity and do not specify every field in the select clause; this should be the typical query statement: select \* from EntityName where field = xxx ….
* **no reading or writing operations are working** : check out if you have correctly define every global parameter needed to access the Google Domain and Datastore

---



