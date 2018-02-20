# How to create business components by a MongoDB collection

Once created an object representing a Mongo DB collection, you can define any number of business components connected to the object just created.  
In order to fill in a grid, a business component must be created: you have to choose a "business component for a list automatically/manually generated" and select the right object, that is to say, the object just created.  
In that case, the select clause will not be editable, since all the fields declared in the collection will be read.  
Neither relationships nor the from clause are enabled, since the Mongo DB query language does not allow you to define joins as for a relational database.  
You are free to define the where clause, according to the Mongo DB query syntax \(see [https://docs.mongodb.org/v3.0/tutorial/query-documents/](https://docs.mongodb.org/v3.0/tutorial/query-documents/)\).

---



