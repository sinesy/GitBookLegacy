# Integration at model level

Once a document type and/or aspects have been created in Alfresco, these definitions can be imported in 4WS.Platform through a reverse engineering wizard which allows to select one or more aspects/document types from an Alfresco model, and import them as "object" \(or models\) in 4WS.Platform. Once they have become objects, they can be used as the starting point to create business components to feed grids, trees, detail forms.  
Both reading and writing of metadata are supported, as well as the document version.

These operations can be performed behind the scene through a series of web scripts injected initially in Alfresco engine which has been designed to work with 4WS.Platform: they allow to communicate with the same \(JSON\) format between the two products and manage operations such as:  
read a list of metadata \(related to a list of documents stored in Alfresco\)  
read a block of metadata \(a page of data\), apply filtering/sorting conditions on this list  
write metatata related to a specific document  
set a metadata value for a list of documents  
upload/download/preview documents stored in Alfresco

One of the key point of this integration is that metadata values to store in Alfresco CMS can be chosen starting from data provided by a database: that means that documents and database data can be mixed together, with 4WS.Platform as the central bus able to communicate with both the systems.

---



