# Define document types and aspects in Alfresco

In order to manage documents in a CMS, document types must be defined before.  
Alfresco is able to manage aspects and documents. An aspect is a set of properties \(e.g. author, document state, approved, approved date, etc.\), each with a type \(number, text, date\) related to the same "concept".  
A document type is composed of a set of properties or a set of aspects. That means that you can simply ignore the aspects and just create a document type by definining it own properties. As an alternative, you can define first one or more aspects and then link them to a document type, which is then composed of the properties inderectly defined in the aspects it is composed of. The perk of using aspects is the reuse of the same properties in different document types: often different document type can share a subset of properties: instead of defining them and replicate them for each document type, they can be defined once as an aspect and then the same aspect is linked to more document types.

Independently of the kind of organization to use when creating document types, these settings must be manually written in an XML file, named "alfresco documents model".  
Alfresco supports multiple models, but generally one model is enough, since it can contain all the required document types.

---



