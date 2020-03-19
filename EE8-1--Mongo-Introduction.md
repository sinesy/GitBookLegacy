# MongoDB Introduction

MongoDB is a cross-platform document-oriented database.  
Classified as a NoSQL database, MongoDB eschews the traditional table-based relational database structure in favor of JSON-like documents with dynamic schemas \(MongoDB calls the format BSON\), making the integration of data in certain types of applications easier and faster.

The main features of Mongo DB are:

* Document-oriented – Instead of taking a business subject and breaking it up into multiple relational structures, MongoDB can store the business subject in the minimal number of documents. For example, instead of storing title and author information in two distinct relational structures, title, author, and other title-related information can all be stored in a single document called Book.
* Ad hoc queries – MongoDB supports search by field, range queries, regular expression searches. Queries can return specific fields of documents and also include user-defined JavaScript functions.
* Indexing – Any field in a MongoDB document can be indexed \(indices in MongoDB are conceptually similar to those in RDBMSes\). Secondary indices are also available.
* Replication – MongoDB provides high availability with replica sets. A replica set consists of two or more copies of the data. Each replica set member may act in the role of primary or secondary replica at any time. The primary replica performs all writes and reads by default. Secondary replicas maintain a copy of the data of the primary using built-in replication. When a primary replica fails, the replica set automatically conducts an election process to determine which secondary should become the primary. Secondaries can also perform read operations, but the data is eventually consistent by default.
* Load balancing – MongoDB scales horizontally using sharding. The user chooses a shard key, which determines how the data in a collection will be distributed. The data is split into ranges \(based on the shard key\) and distributed across multiple shards. \(A shard is a master with one or more slaves.\) MongoDB can run over multiple servers, balancing the load and/or duplicating data to keep the system up and running in case of hardware failure. Automatic configuration is easy to deploy, and new machines can be added to a running database.
* File storage – MongoDB can be used as a file system, taking advantage of load balancing and data replication features over multiple machines for storing files. This function, called Grid File System, is included with MongoDB drivers and available for development languages \(see “Language Support” for a list of supported languages\). MongoDB exposes functions for file manipulation and content to developers.
* Aggregation – MapReduce can be used for batch processing of data and aggregation operations. The aggregation framework enables users to obtain the kind of results for which the SQL GROUP BY clause is used.
* Server-side JavaScript execution – JavaScript can be used in queries, aggregation functions \(such as MapReduce\), and sent directly to the database to be executed.

---



