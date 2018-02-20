# Google Datastore Introduction

Google Cloud Datastore is a NoSQL document database built for automatic scaling, high performance, and ease of application development. Datastore features include:

* Atomic transactions. Datastore can execute a set of operations where either all succeed, or none occur.
* High availability of reads and writes. Datastore runs in Google data centers, which use redundancy to minimize impact from points of failure.
* Massive scalability with high performance. Datastore uses a distributed architecture to automatically manage scaling. Datastore uses a mix of indexes and query constraints so your queries scale with the size of your result set, not the size of your data set.
* Flexible storage and querying of data. Datastore maps naturally to object-oriented and scripting languages, and is exposed to applications through multiple clients. It also provides a SQL-like query language.
* Balance of strong and eventual consistency. Datastore ensures that entity lookups and ancestor queries always receive strongly consistent data. All other queries are eventually consistent. The consistency models allow your application to deliver a great user experience while handling large amounts of data and users.
* Encryption at rest. Datastore automatically encrypts all data before it is written to disk and automatically decrypts the data when read by an authorized user. For more information, see Server-Side Encryption.
* Fully managed with no planned downtime. Google handles the administration of the Datastore service so you can focus on your application. Your application can still use Datastore when the service receives a planned upgrade.

---



