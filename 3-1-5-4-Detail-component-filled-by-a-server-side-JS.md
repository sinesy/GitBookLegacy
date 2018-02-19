# Detail component filled by a server-side JS

When choosing this component, you can fill in a detail form, starting from what got back by it.  
You have first to select an object from the combobox, then write javascript code in order to get back a JSON content compatible with structure of the selected object.

![](http://4wsplatform.org/wp-content/uploads/2018/02/jsdetail.png)

When writing server-side javascript in this component, you can access to a series of built-in methods you can use.  
The complete javascript methods list is reported in this section.  
A method you have always to include \(once\) at the end of the script is:

```js
utils.setReturnValue(jsonString);
```

where  **jsonString**  is a JSON string having always this content:

```js
{ ... }
```

To make it clear, let’s see an example. Suppose we have selected an object Customer related to a CUSTOMER table having these fields:  
CUSTOMER\_CODE  
CORPORATE\_NAME  
ENABLED  
That means we have to get back a JSON string with this format:

```js
{ "customerCode": "C1", "corporateName": "Customer 1", "enabled": true }
```

In case of a detail form, you have always in input all the primary key values, in order to make it possible to fetch a single record, related to such a primary key.  
Starting from this requisite, you can access to the primary key values through a built-in object named “reqParams”, where you can find as attributes all the input passed to the business component \(from the detail form\).  
This is an example of how to get data to fill in a detail form using server-side javascript:

```js
var customerCode = reqParams.customerCode; // get the primary key from the component inputs

// execute a query having only one record as a result
var json = utils.getPartialResult(
    "SELECT CUSTOMER_CODE,CORPORATE_NAME,ENABLED FROM CUSTOMERS WHERE CUSTOMER_CODE=?",
    null,
    false,
    true,
    [customerCode]
);

// convert the JSON string to a javascript object having this structure:
// [{...}]
var list = JSON.parse(json);

// get the first element...
var obj = list[0];

// now the javascript object "obj" must be re-converted to a JSON string
// since the setReturnValue method required a JSON string...
json = JSON.stringify(obj);

// get back data...
utils.setReturnValue(json);
```

---



