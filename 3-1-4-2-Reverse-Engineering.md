# Reverse Engineering

4WS.Platform dramatically simplifies the process of table/relations definition: you can use this product with an already existing database and 4WS.Platform can do a reverse engineering process to fetch all the metadata. Reverse engineering includes also the retrieval of foreign keys that become relations among data models as well as unique keys.  
After that process, you have just to change a few settings, like the ones related to counters, translations and other application specific features.  
This behavior clearly shows how the product can be used: you can start with a database already defined and create data models and relations in a few minutes; this is particularly valuable for old applications developed decades ago that need be converted to modern technologies: 4WS.Platform fits this need very well.

![](http://4wsplatform.org/wp-content/uploads/2015/12/ReverseEngineeering-1024x589.jpg)

When importing tables from a database, 4WS.Platform creates always a business component to use to fetch a list of data: basically the component is a SQL query whose select clause includes all database fields for the main data model and all data models referred by the out-relations.  
4WS.Platform checks also for primary keys or unique keys: if it has been defined for the data model, the data model is marked as "writable" and insert/update/delete operations are allowed for that data model. Moreover, a second business component will be automatically created and defined as a SQL query to fetch a single record, starting from the values of the primary key \(or unique key\).

---



