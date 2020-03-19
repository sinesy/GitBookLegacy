# Design rules

**Limits**  
There are a series of limits in the use of Mongo DB queries. Maybe the most important when compared with the SQL language used with relational database is the lack of the join keyword.  
Anyway, the expressivity of its language is as powerful as the one of SQL when focusing on a single table \(collection\).

The main limits which come with Mongo DB are:

* no support for joins among entities
* no support for transactions over collections: only atomic operations are supported

**Query design**   
The lack of the join keyword leads to the difficulty in retrieving data stored in multiple collections and their aggregation to show themin a single list of data.  
Basically, there are two approaches to face with these limits:

* design the collections so that the all amount of the data needed for a specific list of data can be retrieved from a single collection. It means that tables \(collections\) must be denormalized, which is the opposite of what database designers usually do when defining a relational database
* use additional queries to get all data not belonging to the main collection; Platform allows you to execute any number of additional queries for each record read. That means you cannot use this technique when reading a large number of documents: it is feasible only when you read a block of documents, so that the total number of additional queries is limited.

In case an additional query must be defined to fetch additional data coming from another collection, the steps to follow should be:

* add to the main collection \(the object in Platform\) additional fields to fill in and define them as “virtual fields”
* define one or more additional queries; for each query, select the collection to use and the aliases, so that the where clause would include :XXX variables connected to the main query and set the aliases to use. An example of where clause for an additional query could be:

`{ codArt: { $eq: :COD_ART } }`  
where :COD\_ART must be field retrieved by the main clause, whereas codArt is the corresponding field, expressed in camel mode.  
See the Mongo DB query syntax to use the right operators, as for $eq

**Indexes**   
When filtering or sorting data in a Mongo DB collection, the time required to fetch data could be quite high in case of high volumes of data \(e.g. millions of records\). In that scenario, an index is required to speed up the data fetching. Indexes can be composed of a single or multiple fields and can be used both for filtering or sorting data.  
It would be better to carefully define which indexes to create, according to the filtering/sorting conditions to enable. These conditions should be defined in advance and limited in number.  
Once choosing which indexes to create, Platform provides a “Indexes” folder to create them: in the Ap Designer, open the “Object” definition and select the “Indexes” folder: here you can create any number of indexes.

**Unique indexes**   
Since the primary key in a MongoDB collection is always a predefined id, additional unique keys could be needed, for instance when a collection represents a product or a client: in these cases, specific fields should contain unique values, as for a product code or a client id.  
Platform provides a “Unique indexes” folder to create them: in the App Designer, open the “Object” definition and select the “Unique indexes” folder: here you can create any number of unique indexes. Platform will check out the uniqueness for this combination of values each time a new insert or update operation is carried out.

---



