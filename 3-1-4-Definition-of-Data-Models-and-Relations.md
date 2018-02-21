# Definition of Data model and Relations

A data model is a representation of a database table, including its relations to other tables, defined as foreign keys or manually defined by the user when configuring the data model.  
For each table it is possible to define the following properties:

* table name
* name of the field used to execute logical deletes
* values for the logical delete field \(deleted/not deleted values\)
* name of the field used to manage the record version \(for optimistic locking\)
* flag used to define if version field must be automatically incremented or not \(in case a trigger will do that\)

![](http://4wsplatform.org/wp-content/uploads/2015/12/Object-1024x522.jpg)

Through these settings, it is possible to manage automatically some very common tasks: logical delete and optimistic locking.  
 **Logical delete**  is used when you do not want to physically delete records, because there are many relations that make that delete complex or maybe because you do not want to lose data, since you could decide to restore logical delete data in the future. In any case, logical delete can be automated by simply defining with is the field having that meaning and the values it can have: a filtering condition is automatically appliedto business components pointing to this data model to retrieve only not logically deleted records. In addition, records are logically deleted automatically, when you cancel a record from the GUI.  
 **Optimistic locking**  is a common practice used in multi-user applications, used to ensure that a record can be updated by one user per time. Each time a record is updated, the version field is incremented and future updates are allowed only if the version value for the update is the one currently stored in the record. This behavior is automatically managed with the version field, if specified.  
Version and logical delete fields are optional.  
For each field belonging to the table, the following metadata are fetched:

* field name
* field type \(VARCHAR, CHAR, etc\); additional field types are available: for instance a numeric field can be redefined manually as:
* an internal counter \(automatically managed by the interpreter\)
* a counter based on a specific counter table \(in this case you have to provide additional information: table name, counter field, where, initial value, increment value\)
* a database sequence \(in this case you have to provide also the sequence name\)
* a counter whose value is fetched by invoking a server side component
* a file identifier, used to identify a specific file managed through the current record
* field length \(for text, char or numeric fields\)
* number of decimals \(for decimal fields\)
* flag used to define if the field is mandatory
* flag used to define if the field is part of a primary key
* flag used to define if the field is virtual, i.e. not part of a table \(e.g. a concatenation of fields\)
* flag used to mark the data model as readonly or writable \(it cannot be changed by the user: it depends on the presence or not of a primary key/unique key\)
* combobox used to define if the field must be managed as a translation

![](http://4wsplatform.org/wp-content/uploads/2015/12/DataFields-1024x483.jpg)

---



