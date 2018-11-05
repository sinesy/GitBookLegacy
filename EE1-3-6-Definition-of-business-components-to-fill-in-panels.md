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

## Examples of filtering conditions

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



