# Data coming from database

There can be data read from the database which depend on a specific language. In order to fetch translations about a specific language, a condition about the current language must be included in the where clause of a SQL query; the language can be specified in the SQL statement using the system variable :LANGUAGE\_ID.  
When working with translations stored in a database, typically these translations are stored using two alternative techniques:

* using a dictionary table, where each record contains a translation related to a specific language; therefore the primary key of a dictionary table should contain the language identifier and a code \(or a counter\) that uniquelly identifies the record in the main table \(e.g. Products, etc.\)
* including a series of fields in the main table \(e.g. Products\), one for each supported language; therefore each field has a specific meaning, that is to say, it is related always to the same language.

4WS.Platform supports both the scenarios just described. It allows to show translations in grids and detail forms:

* in a detail form, only one translation is showed, the one related to the language associated to the logged user
* in a grid it is possible to show multiple translations for each record: each translation will be related to a specific language to show in its own column.

It means that translations can be managed \(changed\) for one language only when using a detail form, whereas a grid allows to manage multiple translations with a single operation.

This behavior can be defined in the App Designer during the definition of the columns for a grid.  
There is a special settings in this panel that allows to specify how to manage translations:

* a field for each language
* using a dictionary

In the first case, the user who is configuring the columns has to specify for each field which is the associated language. In this way the interpreter will be able to save automatically a description for each language, since it knows where to save them for all languages.  
In the second case, the data model related to the main table has to include a relation to the dictionary table, which has to be defined as a data model too. Using this relation, the interpreter is able to save records on the dictionary table, for each language.

---



