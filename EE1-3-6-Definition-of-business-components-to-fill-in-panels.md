# Business components to fill-in panels

For every imported object \(described in the previous section\), two business components are automatically created during the importing stage:

* a business component to read a list of documents
* a business component to read a single document

## Business components for a list of documents

The first component is basically  web service: each time a grid has to show a list of documents by invoking this component, it will call the Alfresco web service layer to get the required data and it will pass back that content to the Platform’s grid.  
The data flow is as follow:

Platform’s Grid \(browser\) -&gt; Platform’s business component \(Platform server\) -&gt; Alfresco CMS Web service layer  
You are free to change the URL automatically set in that bsiness component, and add additional filter conditions, in order to define exactly the filtering logic to apply to that grid.  
See the "Examples of filtering conditions" seciton to get more details about how to set additional filters, according to the Alfresco web service syntax.

## Business component for a detail form

The second component is used to feed a detail form by invoking the Alfresco API: it will get from Alfresco the metadata related to the specified document \(identified by a uuid\) it will pass back that content to the Platform’s detail form.  
The data flow is as follow:

Platform’s Form \(browser\) -&gt; Platform’s business component \(Platform server\) -&gt; Alfresco CMS API layer

Both grids and forms could required input parameters to use when fetching data: a grid could require parameters to dinamically filter the grid content, the form has to pass the uuid to get a specific document.  
In both cases, a parameter is defined using the Platform syntax: :XXX, dove XXX is the parameter name.

Please do not change the business component content for a detail form: it must always contain the ID and it should never be changed.

## Filtering conditions on database connected grids

In case of a grid connected to a business components for Reports on line or components for lists generated automatically, filtering and sorting conditions are applied automatically by the grid component and passed forward to the server layer through the HTTP request parameters.

Optionally, you can define additional filtering conditions to the business component through the Additional Filters tab folder, available in the business component definition window.

You can define any number of filtering conditions in this list: the only requirement is to include at least one binding variable in a filtering condition.

Example:

```js
AND (FIELD1 = :MY_VAR OR FIELD2 = :MY_VAR )
```

In this example, the variable name is MY\_VAR and such condition will be automatically appended to the WHERE condition defined for the business component as long as the variable value is passed to the HTTP request. The corresponding request parameter must be expressed in camel-case format. So that for the example above, the request parameter name must be _myVar_.

On the UI layer, such parameter is passed forward in a client-side javascript action in this way:

```js
gridxxx.store.baseParams.myVar = "...";
```

Note that every filter condition is appended to the base WHERE clause so it must start with a logical operation, which should be AND.

Suppose you need to define a condition in an IN, where you don't know in advance if 1, 2 or 3 values will be passed forward. You can manage this scenario by defining multiple filtering conditions, each one with different variable names:

```
AND FIELD IN ( :VAR1 )
```

```
AND FIELD IN ( :VAR2_1 , :VAR2_2 )
```

```
AND FIELD IN ( :VAR3_1 , :VAR3_2 , :VAR3_3 )
```

In this way, each filter condition will be applied alternatively. As a consequence. on the client side, you need to manage different variable names, according to the amount of values to pass forward.



## Filtering conditions on Alfresco connected grids

A typical setting of a business component for grids is as the follow:

```js
service/getList?format=json&type=...&model=...&prefix=...
```

* the model and prefix are automatically set by Platform, when importing an object, since all the objects retrieved inherit the same model \(and prefix\).
* the parameter type is used to define which document type to filter.

Consequently, such a kind of URL would retrieve all the documents stored in Alfresco having the specified document type \(and related to the specified model\).  
This is typically the starting point when retrieving list of documents from Alfresco. It is likely to add further filters to that base request. In order to do that, it is needed to include in the URL a parameter named  **filterBy** , used to add filter conditions.  
These conditions must be expressed according to the Alfresco Query Syntax.  
For instance, this is an URL including a filtering condition:

```
service/getList?format=json&filterBy=zig:Flag_Stato:"C"&type=...
```

zig:Flag\_Stato represents the model prefix + property name related to the specified document type, whereas the : symbol represents the " **starts with** " comparison operator and "…" is the value to compare.  
So prefix:property:"value" means the property must start with the specified value.

Another common comparison operator is the one where a property is  **between**  a specified interval, which is expressed in this way:

```js
prefix:property:[minValue TO maxValue]
```

You can filter documents belonging to a specified  **aspect** :

```js
ASPECT:"cm:aspectName"
```

To filter documents stored in a specified  **path** :

```js
+PATH:"/cm:generalclassifiable/cm:Software_x0020_Document_x0020_Classification/member"
```

You can also combine multiple expressions using the logical operators\*\*  AND, OR and NOT.

You can have a deep look at the Alfresco syntax through these two links:

* [http://wiki.alfresco.com/wiki/Search](http://wiki.alfresco.com/wiki/Search)
* [http://wiki.alfresco.com/wiki/Full\_Text\_Search\_Query\_Syntax](http://wiki.alfresco.com/wiki/Full_Text_Search_Query_Syntax)



