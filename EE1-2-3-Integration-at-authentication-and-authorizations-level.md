# Integration at authentication and authorizations level

Alfresco CMS and 4WS.Platform work in the same way: they must have an ADMIN user and a saet of users and groups who can use some parts of the product.  
These users and groups can be defined internally to each of the two products or can be fetched externally, from an LDAP server.  
An important feature of Alfresco is the ability to set an Access Control List \(ACL\) for each document or folder. That means that it is possible to define which users/groups have access to that document/folder, in terms of: read or write metadata, upload/download a document, delete it.  
4WS.Platform supports authorizations too, at panel level, at menu level, at document level. The latter feature is the same provided by Alfresco: in 4WS.Platform you can see the documents organization in Alfresco and define an ACL for a document/folder: this will be propagated to Alfresco. Therefore, there no more need to know more systems, use multiple GUIs: all the required settings and data/documents can be accessed from a single UI: the one provided by 4WS.Platform.

---



