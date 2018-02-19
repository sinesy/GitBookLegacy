A typical setting of a business component for grids is as the follow:

```js
service/getList?format=json&amp;type=...&amp;model=...&amp;prefix=...
```

* the model and prefix are automatically set by Platform, when importing an object, since all the objects retrieved inherit the same model \(and prefix\).
* the parameter type is used to define which document type to filter.

Consequently, such a kind of URL would retrieve all the documents stored in Alfresco having the specified document type \(and related to the specified model\).  
This is typically the starting point when retrieving list of documents from Alfresco. It is likely to add further filters to that base request. In order to do that, it is needed to include in the URL a parameter named  **filterBy** , used to add filter conditions.  
These conditions must be expressed according to the Alfresco Query Syntax.  
For instance, this is an URL including a filtering condition:

```js
service/getList?format=json&amp;filterBy=zig:Flag_Stato:"C"&amp;type=...
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

---



