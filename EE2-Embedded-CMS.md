# Embedded CMS

### **What is a CMS?**

An organization often has to manage a large number of documents, such as bills, transport documents, technical documentation, production orders and so forth. This large amount of documents would require a lower storage space and would be more easily retrieved if they were digitalized. For instance, bills coming from vendors could be scanned and converted to an electronic format, other documents could be created directly in a digitalized version, through some office applications or other information systems.  
When such a scenario occurs, there is the need to store several gigabytes of documents in an efficient way, indexing them through ad hoc criterias, which can change according to the document type.  
Moreover, they must be searched quickly and efficiently, that is to say, through specific search policies, like the navigation of a documents hierarchy, composed of categories and sub categories or by looking up documents using custom fields, such as the document title, author, creation date, etc.  
Another very helpful feature is the ability to search for a document based on its content, starting from a group of words to find inside the document.  
Finally, since that gigantic quantity of data is strategic for a company, it is essential to create a backup of it, in order to ensure the restoring of the duplicated data in case of loss of data due to hardware failures or software malfunctions.  
What just described is normally part of a system called Content Management System \(CMS\).

Every organization should have an information system including a CMS module or, as an alternative, it should add a stand alone CMS system if it is not supported by the main I.S., since its presence allows to take advantage of what described above.

### **Platform CMS main features**

Platform Enterprise Edition \(from version 5.2\) provides a basic CMS, including the following features:

* a CMS engine, through which it can store and retrieve documents, using a UUID identifier for each document
* organization of documents in folders
* definition of metadata for each document type, stored in a specific folder
* optional support for versioneddocuments, i.e. the simultaneous storage of all versions for the same document name
* optimized for storaging up to 16 billions documents
* definition of any number of filtering/sorting conditions for documents
* upload/download/preview of documents
* bulk import of documents from an external FTP server or from the serverfile system, combined with a CSV file containing metadata linked to files
* optional backup of documents in input folders
* custom logic \(expressed as server-side javascript actions\), which can be executed before importing everyrow in the CSV, in order to perform additional checking and optionally skip the row importing

* custom logic \(expressed as server-side javascript actions\), which can be executed just afterimporting arow in the CSV, in order to perform additionalenquiry and fill data for the same record

### **How to use it**

The CMS module is fully integrated with the rest of the Platform and is based on the availability of one or more database tables, used to store the metadata linked to the imported documents.  
The constraint to respect in order to make it working, is the definition of a field in the table used to maintain the document metadata. Such a field must be a text field having a length of at least 36 characters and will be used to store the UUID \(universal unique identifier\), identifying a specific file. In this way, every record is linked to a specific document.  
Once designing and created one or more tables, representing your document types and used to store the corresponding metadata, the next step is executing the reverse engineering process and let Platform define the data models for each tables. At the same time, Platform will create also a series of business components, useful to fetch a list of documents and a single document.

**Defining a document type \(model\)**  
It is up to you the definition of the primary key for each table: independently from the primary key, you have to include a special field for storing the UUID.  
When defining the data model, you can also activate the versioning of files or not: in the data model detail you can enable/disable this feature using the “ **Manage versioned files** ” check-box. When enabled, each time a new version of the same document is uploaded, it will become the current version, but it does not replace the previous one:  previous versions are maintained as well, and can be retrieved when needed, through the file detail window.

When defining the data model, you can also activate the ACL checking or not: in the data model detail you can enable/disable this feature using the “ **Manage ACL for files** ” check-box. When enabled, uploaded files will be secured and only allowed users can access to them: operations like showing, uploading for the first time/next times, deleting will be granted according to the role assigned to the document type. That means that uploaded documents have a specific role assigned and only users having the same role will be enabled to access such file.

![](/assets/Schermata 2019-05-10 alle 10.56.11.png)

**It is essential at this stage to specify which field is the UUID field** : in order to do it, open the data model and change the field type for such a field to “CMS File”.

![](http://4wsplatform.org/wp-content/uploads/2016/11/datamode2.png)

**Defining UI components linked to the document type**

Next, you can define one or more panels working with the business components and the data model just defined.

In case of a grid panel, you have to set a column with a “CMS File” type \("Type" column\) for the corresponding field defined in the data model. You should find it already defined, since you have created the panel starting from a business component linked to that data model.

In case of a form panel, you have to set an input control with a “CMS File” type for the corresponding field defined in the data model. You should find it already defined, since you have created the panel starting from a business component linked to that data model.

Independently of the panel you are configuring,  **there is a second mandatory field to set: the directory id** \("Directory upload" column\). This property of a grid or form is related to the CMS File column/control: it must be set with the base path where all files will be stored.  
You can define a unique directory id for all your document types \(for all your panels\) or define different directory ids for different panels.

![](/assets/Schermata 2019-05-10 alle 11.03.44.png)

A constraint you have to respect when importing documents is that** a file name must be unique per directory id** : you cannot import two distinct documents having the same name and save them in the same directory.  
Consequently, it is a good idea to **define distinct directories for different panels/data models, if you are not sure you can have the same file names for different usages**.

### Working with documents

At this point you are ready to fill your application with metadata and files, through the upload feature: when pressing on the upload/download button, a dialog window is shown. Through it you can upload/download/preview a document.

![](http://4wsplatform.org/wp-content/uploads/2016/11/upload.png)

The preview feature is supported according to the browser capabilities and the installed plugins on the browser: a PDF can be shown as long as a plugin like Acrobat Reader has been installed on the user machine and recognized by the browser.

### ACL Management

The term Access Control List \(ACL\) stands for the ability for Platform to check out the allowed operations for a file, when it is stored in the directory linked to a document type through a panel.

For the combination "document type" + "directory" \(where documents are stored\) it is possible to define one or more roles, where for each role these operations are supported:

* can view documents
* can upload documents for the first time \(insert\)
* can upload documents multiple times \(update\)
* can delete documents uploaded previously \(delete\)

In this way, it is possible to restrict documents access not only through the standard features provided by Platform at grid/form level \(filtering records, allowed CRUD operations\) but also manage document CRUD operations specifically, using roles st directory level.

In order to do it, use the "Administration -&gt; Permissions -&gt; Roles -&gt; CMS ACL List" button to show the document type ACL feature:

![](/assets/Schermata 2019-05-10 alle 11.25.07.png)

### Bulk import

A very common scenario for a CMS is the bulk import of documents and metadata.  
Platform supports to alternative ways to import documents and metadata:

* bulk import through a remote FTP server – representing the best approach for a cloud solution like 4Ws.Platform
* bulk import from the server file system – in that case, documents should have been already moved to the local file system, so it is unlikely to followthis approach, more feasible for “on premise” installations of 4Ws.Platform

In any case, a csv file is required when importing multiple documents: the CSV file can have any field separator, like , \(comma\) or ; \(semi-colon\)  
**The CSV file must respect the standard CSV forma** t: files not respecting such a standard will generate errors.  
The CSV file must respect also the following constraints:

* the first line must contain a list of column identifiers, used when importing data to correctly map values with the document metadata
* one of the columns must be related to the filesto import: every row in the CSV must refer a file in the remote repository containing docmentsand csv
* csv file and documents must be contained in the same are

It is not essential that the csv file contains all and only the metadata required by a document: the csv could contain many more data, not imported if not needed.  
The csv file could contain less datathan the ones required as metadata for a document: additional metadata not provided by the csv could be defined:

* as default values \(e.g. current user, current import date/time\)
* after importing data in the table, by executing SQL queries or other custom logic, needed to reckon the right values and set them as metadata, through SQL updates

In any case, bulk import is executed through js methods provided by Platform: you can call them from within a server-side js action.  
An advantage of this approach is the chance to invoke such an action from the UI \(e.g. through a button or when an event is fired, like a saving operation\) or it can be scheduled automatically, through the embedded Platform scheduler.  
This is an example of how to define a server-side js action used to execute a bulk import from a remote FTP server:

```js
var defaultValues = new Object();
var map = new Object();
map["ID_CORRISPONDENZA"] = "ID_Corrispondenza";
map["DATA_CONTABILE"] = "DataContabile";
map["FK_TIPOLOGIA_CORRISPONDENZA"] = "FK_TipologiaCorrispondenza";
map["DESCRIZIONE"] = "Descrizione";
map["NOME_FILE_FISICO"] = "NomeFile_Fisico";
map["DATA_FATTURA"] = "DataFattura";
utils.bulkImportFromFTP(
      "myFtpHost", 
      myFtpPort,
      true // use SSL for the FTP connection
      "ftpUsername", 
      "ftpPassword"
      "myFtpRemoteDirToWorkWith", 
      null, // optional filtering condition to apply when reading files from the specified remote dir
      49, // directory id where files will be stored (base dir)
      39, // optional directory id where input files will be moved after being read (backup dir),
      null, // data source id related to the db schema where the application table has been defined
      "MY_DOCUMENTS", // table name where metadata read from the csv file will be imported, 
                      // for each file in input
      "index.csv", // csv file containing the matadata to import in the database table
      "FilaNameField", // the first line of the csv file must contain all column identifiers; 
                       // one of these must be this one, related to the column having the names 
                       // of files to import
      "csvUniqueIdField", // (optional) field name in the first row of the csv file, related to 
                          // a value which identifies uniquelly a row/file in the file: it will be used 
                          // when updating files already indexed; if not specified the "csvFileNameField" 
                          // property will be used instead 
      ";", // fields separator in the csv file
      defaultValues, // js object (a map) containing default values to apply to each record 
                     // to store in the specified table, in case no value has been defined for them; 
                     // entries are names for fields in table 
      map, // js object (a map) used to convert names in the first row of the csv file to names 
           // of fields in table 
      "NULL", // optional value to decode in the csv file: every occurrence found in the csv file 
              // with this value will be converted to null
      true, // true will skip the current processed row in the csv file in case of errors and 
            // continue with the next one; false will interrupt the processing of file:
            // previous rows have been already loaded in the table 
            // and corresponding files indexed
      true, // true will skip the processing of a file if not found inside the csv file
      1059, // optional action id related to a server-side js action to execute before 
            // every file to process: a "vo" variable is available, containing all metadata read from
            // the csv file; return false will skip the processing of the current row and file import
      1069  // optional action id related to a server-side js action to execute just after
            // the processing a row; the uuid value is available as part of the "vo" variable
            // passed to the action
);
```

As you can see, there are many options you can count on.  
It is up to you which ones to exploit.  
For instance, you can decide which policy to use when importing data and there are errors:

* skip the single row in the csv file and go on with the next one; in that case, the document is skipped too and it will remain in the original position
* interrupt the import process when coming across an error; in that case, all metadata and documents previously imported will remain inside theCMS, whereas all next documents will be ignored

Default values can be mapped as in the example above: entries are table fields, where the value can havea string, numeric o date type.  
Here you have always to specify which column in the csv file would contain the file name, so that it is possible to match a specific row in the csv with the corresponding file.  
This column is also used to match again the same file, in case you want to update the metadata in next loadings and/or replace the file: the file name will be used to identify the file previously stored and get the corresponding record to update in the application table.  
Optionally, you can use the csvUniqueIdField argument to specify a column in the csv representing a value which can identity univokely a record in the application table: this value will be used instead of the file name in loadings where you want to update metadata as well as the file name. In this scanario, it is not essential that the file name would be the same as the one loaded initially: it can have a different name, so that the previous one will be removed \(if not versioned\) and replaced by the new one.

In case of complex logic to carry out for each row to import, you can rely on two optional server-side j actions: one is invoked just before the processing of each row in the csv file; the second is invoked just after importing metadata and document within the CMS.  
If you need to skip the metadata+document import for a specific row, you can do it by creating a server-side js action like this on, invoked before the row processing \(action id 1059 in the example above\)

```js
if (mycustomlogic) {
  // in this case, the row must be skipped...
  utils.setReturnValue("false");
}
```

If you need to fill the record in the table with additional metadatanot coming from the csv file, you can do it by creating a server-side js action like this one, invoked after the row processing\(action id 1069 in the example above\)

```js
for(var id in vo)
 utils.log(id+"="+vo[id],"DEBUG");

 var json = utils.executeQuery("SELECT * from MY_DOCUMENTS WHERE UUID=?",null, false,true,[vo.UUID]);
 utils.log(json,"DEBUG");
 // execute additional queries or logic...
 // ...
 // var data = ....

 utils.executeSql("UPDATE MY_DOCUMENTS SET OTHERFIELD=? WHERE UUID=?",null,false,true,[ data, vo.UUID ]);
```

You can use the before processing row action to fill data to insert into the application table, instead of using the second action.  
In such case, you can use the

```js
utils.setAttributeName(fieldName,value);
```

method to pass forward a value to insert along with the others.  
In the before processing action, you have also two pre-defined variables available:

```js
reqParams.insert
reqParams.uuid
```

The insert boolean variable: if true, it means that the row to process will be inserted in the application table, otherwise, and update SQL operation will be performed.  
In case of an update operation \(insert flag isfalse\), the second variable uuid contains the unique identifier for the file already stored.  
If needed you can define a custom logic using these variables according to the scenario: an insert or an update.

### **CRUD operations**

  
You can manage through server-side js actions single documents as well.  
The following methods are provided by Platform and you can use them in an action:

* insert a document in the CMS – a UUID is returned back; metadata in additional tables are managed apart
* updatea document \(replace it\) in the CMS – metadata in additional tables are managed apart
* deletea document fromthe CMS – a UUID must be providedmetadata in additional tables are managed apart

These are a few examples related to CRUD operations working on the CMS subsystem:

```js
// insert a new document, starting from a file in the server file system
var uuid = utils.importFileInCMS(
     pathWhereTheFileIsLocatedInInput,
     destinationDirectoryId,
     dataSourceIdWhereTheTableisLocalted, 
     tableName
);

// insert a new document, starting from a file stored starting from a dir id
var uuid = utils.importFileInCMS(
     sourceDirectoryIdWhereTheFileIsLocated,
     fileName,
     destinationDirectoryId,
     dataSourceIdWhereTheTableisLocalted, 
     tableName
);

// replace an already existing document, starting from a file in the server file system
utils.updateFileInCMS(uuid, pathWhereTheFileIsLocatedInInput);

// replace an already existing document, starting from a file stored starting from a dir id
utils.updateFileInCMS(
     uuid,
     sourceDirectoryIdWhereTheFileIsLocated,
     fileName
);


// delete an already existing document
utils.deleteFileFromCMS(uuid);
```

---



