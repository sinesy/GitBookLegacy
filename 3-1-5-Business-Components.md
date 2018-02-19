# What are business components

Business components are usually connected to a data model, except for two special kind of business component, used to create a read only query and called "Query for a report to show on grid" and "Component for control query".  
A business component allows to define a query to execute and used to populate a grid/tree nodes or a detail form component. The select part is usually read-only, since it is automatically composed from the from clause, which is implicitelly defined starting from the selected data model connected to the business component and from the selected relations.  
This means that the user can choose a data model \(a specific table\) and out-relations: starting from these models \(tables\) the select and from clauses are automatically composed.  
The user can define manually the where, order, group by and having clauses.

![](http://4wsplatform.org/wp-content/uploads/2015/12/BC-1024x487.jpg)

Any number of business components can be defined, so you can populate a bunch of different grids, each with a specific filtering condition.  
An exception to this behavior are the "Query for a report to show on grid" and "Component for control query" components, where neither data model nor relations are required: the user is free to define each part of the SQL query.  
Consequently, any number of retrieval queries can be defined.  
Each business component has a component type associated; these are the supported types:

* **Grid component automatically/manually created**  – when creating a grid component, it can have linked this component type; it is automatically created along with the data model creation
* **Detail component automatically/manually created ** – when creating a detail form component, it can have linked this component type; it could be automatically created along with the data model creation
* **Grid service automatically/manually created**  -starting from an URL invoking a web service, the response form the web service is retrieved, which must be in JSON format and having a format compatibile with the object definition; the service must return a list of records
* **Detail service automatically/manually created**  -starting from an URL invoking a web service, the response form the web service is retrieved, which must be in JSON format and having a format compatibile with the object definition; the service must return a single record, starting from the primary key values provided in the URL
* **Custom Java grid component**  – when creating a grid component, it can have linked this component type; in this case, the bean name of the component developed manually by the programmer is specified. See this section for more details.
* **Custom Java detail component**  – when creating a detail form component, it can have linked this component type; in this case, the bean name of the component developed manually by the programmer is specified. See this section for more details.
* **SQL definition component**  – a generic SQL instruction \(insert, update, delete\) manually invoked by the GUI, when a specific event happens
* **Custom SQL def. component**  – a generic SQL operation performed internally to a custom business component; in this case, the component bean name is specified
* **Query for a report to show on grid**  – a generic SQL query, linked to a grid component, manually defined by the user; since the SQL statement can include any number of tables, the linked table must be read only
* **Component for counter retrieval ** – a special business component invoked to generate a counter for a field when inserting records; in this case, the component bean name is specified.
* **Component for control query**  – a generic SQL query, same as the query for a report to show on grid, but it doesn’t create a new window with a grid.
* **Grid component filled by a server-side JS**  – once chosen the linked object, you are free to use server-side javascript and create all the business logic you need to get back a JSON string representing a list of records to fill in a grid. This business component can replace a “Grid component automatically/manually created” when the business logic is too complex to be managed by a single SQL query. See this section for more details.
* **Detail component filled by a server-side JS**  – once chosen the linked object, you are free to use server-side javascript and create all the business logic you need to get back a JSON string representing a single record to fill in a detail form. This business component can replace a “Detail component automatically/manually created” when the business logic is too complex to be managed by a single SQL query.
* **Grid component filled by a GDrive folder**  – when Platform is connected to a GSuite account, you can access to Google Drive folders. This component allows you to specify a Google Driver folder and get a list of all files stored in that folder. For each document a series of attributes are fetched. Such a list is used to fill in a grid.
* **Grid component filled by a GDrive folder and subfolders**  –when Platform is connected to a GSuite account, you can access to Google Drive folders. This component allows you to specify a Google Driver folder and get a list of all files stored in that folder and all its subfolders too. For each document a series of attributes are fetched. Such a list is used to fill in a grid.

The first two components requires to be linked to a specific object, where the object \(or data model\) represents a database table and its fields.  
The first component can be used to automatically generate a SQL query composed of a SELECT + FROM clauses, whose definition comes from the object the business component is linked to: starting from the object definition, the SELECT + FROM clauses can be automatically generated. The user has just to complete it, by adding for instance a filtering condition \(WHERE clause\). The result is a business component that can fetch a list of \(filtered\) records from a table, perfect to fill in a grid.  
The second component can be used to automatically generate a SQL query composed of a SELECT + FROM + WHERE clauses, whose definition comes from the object the business component is linked to: starting from the object definition, the SELECT + FROM clauses can be automatically generated. Moreover, the WHERE clause is automatically composed as well, starting from the primary key definition for the corresponding table: the WHERE allows to get one only record, starting from its primary key, which is not “fixed” in terms of values, but parameterized. The result is a business component that can fetch a single record from a table, starting from the primary key values, perfect to fill in a detail form.

---



