# How to create business components by a datastore entity

Once created an object representing a datastore entity, you can define any number of business components connected to the object just created.  
In order to fill in a grid, a business component must be created: you have to choose a "business component for a list automatically/manually generated" and select the right object, that is to say, the object just created.  
In that case, the select clause will not be editable, since all the fields declared in the entity will be read.  
Neither relationships nor the from clause are enabled.  
You are free to define the where clause, according to the GQL syntax \(see [https://cloud.google.com/datastore/docs/apis/gql/gql\_reference](https://cloud.google.com/datastore/docs/apis/gql/gql_reference)\).

---



