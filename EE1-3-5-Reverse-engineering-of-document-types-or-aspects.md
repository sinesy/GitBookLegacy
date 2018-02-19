# Reverse engineering of document types or aspects

Once defined an XML model in Alfresco, using either the Alfresco Admin Console or 4WS.Platform creation features described in the previous section, the next point is to import these definitions from Alfresco to 4WS.Platform: in this way, it will be possible to read an write metadata and documents related to those document type/aspect definitions.  
If not already done, you have to open the Application parameters in the App Designer \(the second folder in the Application Detail window\) and specify the settings needed to connect to the Alfresco CMS server: the base URL, admin username and password, the XML model file name.  
Once done that, you’d better re-logon into the App Designer.

In order to import the Alfresco document type/aspect definitions, you have to choose the "Add objects from Alfresco" menu item available in the App Designer.  
Through this feature, you can import:

* one or more document types
* one or more aspects
* a "virtual" aspect representing the "union" of all the aspects defined in the model; this selection could be helpful sometimes to get a list of documents, independently of their type/aspect and having a shared set of properties to show

For each selected item, an object will be created, including its properties.  
Each created object will have:

* a field for each property defined in the corresponding document type/aspect
* a special field named "cm:id", required in Alfresco to identify a single document in the whole repository \(a uuid\)
* a special field named "cm:name", required by Alfresco to assign a name to a specific file; note that you can have multiple files having the same name, but you cannot have those within the same folder
* a special field named "cm:Parent\_Id", required by Alfresco to save the file in a specific folder; that folder is identify by the Parent\_id \(a uuid\)
* a special field named "cm:typeShort", required by Alfresco to assign a specific document type to every file

Starting from this object definition, you can create any number of panels, combined together, and manage documents in lists or detail forms, as you wish and take advantage of all the advanced features provided by the Platform UI to organize the content in panes and panes in rich input controls.

---



