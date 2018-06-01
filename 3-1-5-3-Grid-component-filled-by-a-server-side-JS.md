# Grid component filled by a server side JS

When choosing this component, you can fill in a grid, starting from what got back by it.  
You have first to select an object from the combobox, then write javascript code in order to get back a JSON content compatible with structure of the selected object.

![](http://4wsplatform.org/wp-content/uploads/2018/02/jsgrid.png)

When writing server-side javascript in this component, you can access to a series of built-in methods you can use.  
The complete javascript methods list is reported in this section.  
A method you have always to include \(once\) at the end of the script is:

```js
utils.setReturnValue(jsonString);
```

where  **jsonString**  is a JSON string having always this content:

```js
{ "valueObjectList": [{...},{...},...], "moreRows": true|false }
```

Moreover, the content of valueObjectList is a list of objects whose structure must always respect the structure of the object.

To make it clear, let’s see an example. Suppose we have selected an object Customer related to a CUSTOMER table having these fields:  
CUSTOMER\_CODE  
CORPORATE\_NAME  
ENABLED  
That means we have to get back a JSON string with this format:

```js
{ 
   "valueObjectString": [
      { "customerCode": "C1", "corporateName": "Customer 1", "enabled": true },
      ...
   ], 
   "moreRows": true 
}
```

How to generate the list of javascript objects to pass to the “ **valueObjectList** “? The easiest way is through the  **utils.getPartialResult**  method. This method has been designed to work with a grid: it support data pagination, data filtering and sorting. It means that when the end user will scroll data in the grid, apply filters or sort columns, these settings will be passed automatically behind the scene to this business component and the getPartialResult method will use them automatically: you have just to define the “base” SQL query in getPartialResult and this method will enhance the “base” SQL with what needed to manage pagination, filtering/sorting conditions.

**Notice the difference between getPartialResult and executeQuery: the second always get back the whole result set, not a block of data end it ignores the filtering/sorting conditions coming from the grid. Pay attention to its usage: you should not use to get the main data to pass back to the grid: the right method to use is getPartialResult.**

In a real scenario, usually the javascript code to write is never as easy as the one reported in the screenshot above, otherwise it would have been easier to use directly a “Grid component automatically/manually created” and use SQL.  
A typical scenario when you have to use javascript is when you cannot retrieve all data you need to pass to the grid through a single SQL query. Consequently, you could have the need to:

* fetch the main data through getPartialResult
* iterate over each fetched row and for each for, execute additional queries to retrieve additional data
* combine the data from the main query with the one fetched through the additional queries

This is an example where all these steps are reported:

```js
var json = utils.getPartialResult(
    "SELECT CUSTOMER_CODE,CORPORATE_NAME,ENABLED FROM CUSTOMERS WHERE ENABLED=?",
    null,
    false,
    true,
    ["E"]
);

// convert the JSON string to a javascript object having this structure:
// { valueObjectList: [{...},{...},...], moreRows: true|false }
var obj = JSON.parse(json);

// suppose you have to return records having this structure:
// { "customerCode": "C1", "corporateName": "Customer 1", "enabled": true, "totalOrders": xyz }

// iterate over the records fetched and for each execute an additional query to get the total nr of orders...
for(var i=0;i&lt;obj.valueObjectList.length;i++) {
    var record = obj.valueObjectList[i];
    json = utils.executeQuery(
        "SELECT COUNT(*) AS NUM FROM ORDERS WHERE CUSTOMER_CODE=?",
        null,
        false,
        true,
        [ record.customerCode ]
    );
    var orders = JSON.parse(json); // json: [{ "num": xyz },{...}...]
    if (orders.length&gt;0)
      record.totalOrders = orders[0].num;
}

// now the javascript object "obj" must be re-converted to a JSON string
// since the setReturnValue method required a JSON string...
json = JSON.stringify(obj);

// get back data...
utils.setReturnValue(json);
```

---

**Working with complex SQL queries and decoding fields**

In case of a complex SQL query to pass to getPartialResult method, involving multiple tables and fields, it could happen that a filtering or sorting condition will not be applied correctly, since on the grid \(UI\) an attribute is passed forward to the javascript business component and here the attribute is not translated correctly.

In such a scenario, you can use a utility method to use for each attribute to decode:

**utils.decodeField\(attributeName,databaseField\);**

where **attributeName** is the attribute coming from the grid \(UI\), like "contacts.customerCode"  and **databaseField** represents the tablename.fieldname to use instead of the attribute, like "CONTACTS.CUSTOMER\_CODE".

In case of multiple mappings, i.e. for more than one attribute, you can use setDecodeField for each of them.

