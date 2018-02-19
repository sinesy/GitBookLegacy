# Online report

The typical workflow for the creation of a grid involves the creation of a data model with its relations, the definition of a business components to feed grids and finally the creation of the grid binded to the business component and inheriting the field related to the data model.  
The limit of this procedure is basically related to the need of a data model and relations, which determine the complexity of the SQL query, in terms of inner/outer joins and involved tables.  
However, there may be scenarios where a more complex SQL query is needed, for instance a nested query, a union, etc.  
In order to overcome this limit, a special kind of business component called " **Query for a report to show on grid** " can be used. In this way, the user is free to define manually each part of the SQL query \(select, from, where, order by, group by, having\). A readonly grid is automatically created starting from the select clause of this SQL statement, without the need to define a data model/relations before.  
A menu item can also be created along with the business component + grid: in this way it is possible to create powerful reports and access to them directly from the application menu.  
They are a window containing a grid panel, having the same features ofany other panel, so it is possible to include it in any other panel or window too.

---



