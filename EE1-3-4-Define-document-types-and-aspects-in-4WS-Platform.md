# Define document types and aspects in 4WS.Platform

An alternative way to define document types and aspects without knowing the syntax of the Alfresco XML model file, is by using the "Alfresco document types" and "Alfresco aspects" functionalities available in 4WS.Platform. These features allow to graphically define document types and aspects.  
Moreover, the same features can be used to mantain over the time the same objects: additional properties can be added to a document type or aspect.

Pay attention during the maintenance of the Alfresco XML model: it is a bad idea to remove or change already existing properties from and aspect or document type, since it is likely that Alfresco will not allow you to "commit" these changed.   
A better and common solution is to simply not use any more these properties and create new ones, in case you need to "change" the type or other settings.

---



