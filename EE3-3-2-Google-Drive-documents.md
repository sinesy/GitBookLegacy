# Google Drive documents

Apart from the server-side js API provided by Platform, grids and forms can be easily created starting from the content of a GDrive folder, as for a database table, read through a business component.  
In this way, creating a simple Document Management System based on GDrive becomes a quite easy task.

Typically, the steps to follow when creating a list of documents read from GDrive includes:  
defining an object, by choosing "Add a Google Drive object" in the Objects list of the Web Designer; once define the object name and save it, the second folder becomes enabled  
defining the properties of the document \(object\) just defined; default properties are always created by default. These include: document id, type, creation date, etc.   
Here additional custom properties can be defined and added to each document  
creating a business component to feed a grid; the business component to create mustbe linked to the object just created and must have "List component fed by a Google Drive folder" type.   
Here the folder id is mandatory and must be specified. Go to Google Drive to get the id.  
An optional field is the where condition to apply, in case not all documents stored in the folder should be retrieved. The where condition must respect the Google Drive syntax, described in [https://developers.google.com/drive/v2/web/search-parameters](https://developers.google.com/drive/v2/web/search-parameters)  
creating a grid and link it to the business component  
the id column should have "File id" type, so that the download/upload/preview button would be viewed in grid  
if a document detail window is required, a form can be created; the form must be linked to a business component having type "Form component fed by a Google Drive folder"; when choosing this kind of component, the where condition is read only and always filled in with ":ID", which is the document identifier.  
Again, the id control should be mapped to "File id" type, so that the download/upload/preview button would be viewed for that field.

Note: the folder content acutally retrieved by a business component is not only filtered according to the folder and where conditions applied, but also according to the ACL \(Access Control List\) defined by the Google administrator or folder owner. that means that the documents list can be filtered according to the current logged user.

Note: it is also possible to retrieve documents belonging to a folder and its sub-folders too. Anyway, this operation is slower than the one which only gets documents directly connected to the folder.

Filter panels can also be linked to the grid, in order to filter documents according to a set of properties showed in that filter.  
Note that the filter panel also contains on the top a "Search by text" field: this allows to search by document content; this feature is automatically provided by Google Drive and could not always work: it depends on the document type and not works for image based PDF documents, for instance.

---



