# **Pure web page development**

Platform provides a utility javascript file you can include in your own web pages, in case you want to create an ad-hoc web application, without using any of the features provided by Platform using the standard UI, based on Sencha ExtJS data entry components.

That means you can still exploit everything provided by Platform in terms of serve-side layer: authentication, authorizations, user information, web services invocation.

All these features can be managed thanks to a utility main\_page.jsp file to include in your web page. This js file provides the following utility methods:

login\(callback,vo\)

Execute the authentication on Platform, in order to access later to the server-side layer.

The callback argument must be a js function, automatically invoked after the authentication process. It passes forward a js object containing 2 attributes: success \(true\|false\) and an optional message string, containing the error message, in case of authentication failure.

The js object named “vo” must include the following attributes: applicationId, companyId, siteId, username, password.

Example:

| login\(function\(res\) { // callbackif \(res.success==true\) {// do something}},{ // data to pass forwardapplicationId: "",companyId: "",siteId: xxx,username: "",password: ""}\); |
| :--- |


Once the login operation has been successfully completed, a set of global js variables are filled and available everywhere inside the web page:

context- string representing the web context for this web page

applicationId- string

companyId- string

siteId- number

username- string

password- string

languageId- string

userRoles- js array, whose elements are strings related to role id

translations- map containing all translations

init\(callback,vo\)

This method allows to by-pass the authentication on Platform, since it has been already done and sets the global js variables from the internal state available on the server layer.

The callback argument must be a js function, automatically invoked after the authentication process. It passes forward a js object containing 2 attributes: success \(true\|false\) and an optional message string, containing the error message, in case of authentication failure.

The js object named “vo” is optional, since in case of user already authenticated, this is not required.

Example:

| try {init\(initCompleted\);}catch\(e\) {alert\(e\);} |
| :--- |


## **Setting up a web page**

In order to use this utility .jsp file, your web page has to load it, through javascript and only after the js loading has been completed, you can start using it, by invoking “login” or “init” method.

Consequently, your web page must always include a way to load main\_page.jsp in it and wait for its loading completion.

This is an example of code to include in your web page in order to do it:

| &lt;html&gt;&lt;head&gt;&lt;script language="Javascript"&gt;functionloadScript\(url, callback\){ // utility function always to include in any web page...var script = document.createElement\("script"\)script.type = "text/javascript";if \(script.readyState\){ //IEscript.onreadystatechange = function\(\){if \(script.readyState == "loaded" \|\|script.readyState == "complete"\){script.onreadystatechange = null;callback\(\);}};} else { //Othersscript.onload = function\(\){callback\(\);};}script.src = url;document.getElementsByTagName\("head"\)\[0\].appendChild\(script\);}// 3. callback invoked after the initializationvarinitCompleted= function\(\) {// do something} // 1. load dynamically the infra js...loadScript\('../4ws/main\_page.jsp?applicationId=XYZ,function\(\) {// 2 after loading the infra js, initialize user data:// that will load web pages variables \(username, etc.\) and initialize translationstry {init\(initCompleted\);}catch\(e\) {alert\(e\);}}\); &lt;/head&gt;&lt;body&gt;...&lt;/body&gt;&lt;/html&gt; |
| :--- |


The example above requires that the authentication process has been already carried out before: in such a case, the “init” method will complete successfully, and the custom “initCompleted” method will be automatically invoked.

1.2 Loading a grid

A typical scenario involves the data loading to show on a grid.

There is a utility class you can use to simplify this task:

var myStore = new ListStore\(compId,callback,callbackError,synchronous\);

This class represents the content of the grid, in terms of data and can manage data retrieving, including filtering and sorting conditions, as well as data pagination.

This class requires a few arguments:

* compId - business component id, defined through Platform to fetch data for a list

* callback - a js function invoked at the end of every data loading

* callbackError - a js function invoked in case of errors when loading data

* synchronous - optional flag true\|false, used to force synchronous data loading; if not specified, data loading is asynchronous \(strongly recommended\)

Once created this object, you can force any number of time the data loading through a method it provides:

load\({ startPos: xyz, blockSize: xyz, filters: \[{ attrName: "", op: "", value: "" },...\] }\);

You can simply use this method by calling it without arguments:

load\(\);

or using it with any of its arguments, according to the need.

Remember that the store will not load data automatically when created: you have always to call “load” to force data loading.

The ListStore includes these attributes you can use at any time:

* valueObjectList - js array containing js objects coming from the server layer \(data loaded\)

* moreRows - flag true\|false, related to additional records available on the server side

* resultSetLength - max number of records on the server layer

You can use valueObjectList to fill in your grid.

Example:

| var gridStore = new ListStore\(149, // component idfunction\(\) {// callback invoked after each data loading...},function\(\) {// callback invoked after each data loading with errors...alert\('Ops'\);}\); |
| :--- |


There is not any utility available here to render the grid, starting from the data provided by this object: this is because you are free to use any external framework to render a grid.

Just to give you an example of a simple rendering of a grid, starting from basic javascript, the grid will be rendered by appending DOM childs \(by adding &lt;tr&gt; and &lt;td&gt; tags\) to a &lt;table&gt; tag.

| vargridStore=new ListStore\(149,function\(\) {// callback invoked after each data loading... var list =gridStore.valueObjectList;var myGrid = document.getElementById\("myGrid"\);while\(myGrid.children.length&gt;0\)myGrid.removeChild\(myGrid.children\[0\]\); // remove previous rowsfor\(var i=0;i&lt;list.length;i++\) {myGrid.append\(createTableRow\(list\[i\],\["clientCode","name","createDate","totalAmount","country"\],nullnull\) \);}},function\(\) {// callback invoked after each data loading with errors...alert\('Ops'\);}\); // utility methodfunctioncreateTableRow\(row,attributeNames,formatters,sizes\) {var tr = document.createElement\("tr"\);for\(var i=0;i&lt;attributeNames.length;i++\) {var td = document.createElement\("td"\);if \(sizes!=null\)td.style="width:"+sizes\[i\];tr.append\(td\);var value = row\[attributeNames\[i\]\];if \(value==null\)value = "";else if \(formatters!=null && formatters\[i\]!=null\)value = formatters\[i\]\(value\);var t = document.createTextNode\( value \);td.append\(t\);}return tr;} &lt;/script&gt; &lt;/head&gt;&lt;body&gt;&lt;tableid="myGrid" border=1&gt;&lt;/table&gt;&lt;/body&gt;&lt;/html&gt; |
| :--- |


## **Formatting data**

Suppose you need to format a number with a specific number of decimals or with the grouping or you need to format a date.

The main\_page.jsp provides a few utility methods, you can use both for formatting cells in grid and controls in form.

var formattedString = dateFormatter\(dateObj\);

Format a date object or a date/datetime coming from a JSON response to a formatted string related to a date without time, to show in a grid or form control. Such a date is automatically formatted according to the language set for the logged user.

var formattedString = dateTimeFormatter\(dateObj\);

Format a date object or a date/datetime coming from a JSON response to a formatted string related to a date+time, to show in a grid or form control. Such a date and time is automatically formatted according to the language set for the logged user.

var formattedNumber = numberFormatter\(numObj,decimals,grouping\);

Format a number to a formatted string, to show in a grid or form control. Such a number is formatted according to the other two arguments:

* decimals - number of decimals to use when formatting the number; if set to null, the number will not be formatted in any way for the decimal part of it

* grouping - flag true\|false used to define if the number must be formatted with the grouping \(thousand symbol\)

The decimal and thousand symbols to use are defined according to the language associated to the current user.

var formattedNumber= currencyFormatter\(numObj,decimals,grouping\);

Same behavior of the numberFormatter; in addition, a currency symbol is shown before the formatted string.The currency symbol is defined according to the language associated to the current user.

Let’s see how to use these utility methods in the previous example, to format a date or a number:

| vargridStore= newListStore\(149,function\(\) {// callback invoked after each data loading...var list =gridStore.valueObjectList;var myGrid = document.getElementById\("myGrid"\);while\(myGrid.children.length&gt;0\)myGrid.removeChild\(myGrid.children\[0\]\); // remove previous rows… for\(var i=0;i&lt;list.length;i++\) {myGrid.append\(createTableRow\(list\[i\],\["clientCode","name","createDate","totalAmount","abc","country"\],\[null,null,dateTimeFormatter,numberFormatter,null,null\],null\) \);}},function\(\) {// callback invoked after each data loading with errors...alert\('Ops'\);}\); |
| :--- |


## **Using combo-boxes**

You are free to include comboboxes in your web page. Platform can help you out in filling out the combo items, starting from a selector defined in Platform. Allowed selectors are static and dynamic combobox selectors.

What you can do is including a &lt;select&gt; tag in your web page and then let Platform do the rest, by using the method:

var combo = fillInCombo\(selectorId,comboId,synchronous\);

You have to specify:

* the selector id to use for filling our items in the combobox

* the HTML id which identifies your combobox in the web page

* a flag true\|false used to specify whether the data loading must be synchronous or not

Bear in mind that you need to set a synchronous loading in case you are using the combobox to decode a value in a grid cell or in a form control.

Consequently, you can use an asynchronous loading only in case of comboboxes not directly connected to data, as for a combobox in a filter panel.

Example of a combobox in a filter panel:

| ...// fill in the first comboboxfillInCombo\(49,"myCombo",false\); &lt;/script&gt;&lt;/head&gt;&lt;body&gt;&lt;select id="myCombo" onchange="myComboChanged\(this\);"&gt;&lt;/select&gt;&lt;/body&gt;&lt;/html&gt; |
| :--- |


Another very helpful usage of a combobox is to decode a value to a translation to show in a grid cell or in a form control.

As for the classical use of Platform, you have first to define a selector, then you can use it to decode values.

You can do it through a couple of utility method provided by the “fillInCombo” method. After invoking such a method, a couple of js methods are injected into the combobox:

* code2Desc\(code\)- this is used to convert a code to its description

* desc2Code\(desc\)- this is used to convert a description to its code

In the following example, you can see how to use a combobox to decode a value in a grid, for the column “country”:

| …// fill in the form comboboxvarfakeCombo= fillInCombo\(49,"country",true\); // create a grid datastorevargridStore= newListStore\(149,function\(\) {// callback invoked after each data loading...var list =gridStore.valueObjectList;var myGrid = document.getElementById\("myGrid"\);while\(myGrid.children.length&gt;0\)myGrid.removeChild\(myGrid.children\[0\]\); // remove all previous rows… for\(var i=0;i&lt;list.length;i++\) {list\[i\].country =fakeCombo.code2Desc\(list\[i\].country\);myGrid.append\( createTableRow\(list\[i\],\["clientCode","name","createDate","totalAmount","abc","country"\],\[null,null,dateTimeFormatter,numberFormatter2Dec,null,null\],\[150,400,160,120,80,200\]\) \);}},function\(\) {// callback invoked after each data loading with errors...alert\('Ops'\);}\);  &lt;/script&gt;&lt;/head&gt;&lt;body&gt;&lt;table id="myGrid" border=1&gt;&lt;/table&gt;&lt;/body&gt;&lt;/html&gt; |
| :--- |


## **Loading a form**

A typical scenario involves the data loading to show into a set of graphics controls included in a form. There is a utility class you can use to simplify this task:

var myStore = new FormStore\(compId,callback,callbackError\);

This class represents the content of the form, in terms of data and can manage data retrieving, starting from a set of values to pass forward to the server layer, in order to identify the right record to fetch.

This class requires a few arguments:

* compId - business component id, defined through Platform to fetch data for a list

* callback - a js function invoked at the end of every data loading

* callbackError - a js function invoked in case of errors when loading data

Once created this object, you can force any number of time the data loading through a method it provides:

load\({ filters: \[{ attrName: "", op: "", value: "" },...\] }\);

Remember that the store will not load data automatically when created: you have always to call “load” to force data loading.

The FormStore includes this attribute you can use at any time:

* vo - a js object containing data coming from the server layer \(data loaded\)

Example:

| // create a form datastorevarformStore= newFormStore\(159,function\(\) {// callback invoked after each data loading...var controlClientCode =document.getElementById\("clientCode"\);var controlName = document.getElementById\("name"\);var controlCreateDate = document.getElementById\("createDate"\);var controlTotalAmount = document.getElementById\("totalAmount"\);var controlAbc = document.getElementById\("abc"\);var controlCountry = document.getElementById\("country"\);controlClientCode.value = formStore.vo.clientId;controlName.value = formStore.vo.name;controlCreateDate.value =dateFormatter\( formStore.vo.createDate \);controlTotalAmount.value =currencyFormatter\( formStore.vo.totalAmount \);controlAbc.value = formStore.vo.abc;controlCountry.value = formStore.vo.country;},function\(\) {// callback invoked after each data loading with errors...alert\('Ops'\);}\); formStore.load\({// filtering conditions needed to load a single recordfilters: \[{ attrName: "clientCode",value: “....” }\]}\); &lt;/script&gt;&lt;/head&gt;&lt;body&gt;&lt;table border=1 &gt;&lt;tr&gt;&lt;td&gt;Code&lt;/td&gt;&lt;td&gt;&lt;input type=textid="clientCode" style="width:200px" /&gt;&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td&gt;Name&lt;/td&gt;&lt;td&gt;&lt;input type=textid="name"style="width:200px" /&gt;&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td&gt;Date&lt;/td&gt;&lt;td&gt;&lt;input type=textid="createDate"style="width:200px" /&gt;&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td&gt;Amount&lt;/td&gt;&lt;td&gt;&lt;input type=textid="totalAmount"style="width:200px" /&gt;&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td&gt;ABC&lt;/td&gt;&lt;td&gt;&lt;input type=textid="abc"/&gt;&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td&gt;Country&lt;/td&gt;&lt;td&gt;&lt;selectid="country"onchange=""&gt;&lt;/select&gt;&lt;/td&gt;&lt;/tr&gt;&lt;/table&gt;&lt;/body&gt;&lt;/html&gt; |
| :--- |


## **Other utility methods**

---

var t = getTranslation\(entry\);

Translate the specified entry into the corresponding translation, according to the language associated to the current user. In case the entry is not found, the same entry will be passed back.

var response = new SyncRequest\(\).send\(uri\[,method\[,data,mimeType\]\]\)

Synchronous web call to Platform server layer.

Example:

| try {var json = new SyncRequest\(\).send\(context+“/executeJs?...”,”GET”\);}catch\(e\) {alert\(e\);} |
| :--- |


new AsyncRequest\(\).send\(uri\[,method\[,data,mimeType\]\],callback,callbackError\)

Asynchronous web call to Platform server layer.

The last two arguments represents callback functions invoked when the response arrives, in case of successful execution and in case of error:

* callback\(json\)- json is a text formatted content

* callbackError\(json,status\)- json is a text formatted content related to the error, status the HTTP error code \(a number\), e.g. 401

logout\(\)

Log out from the server layer.

