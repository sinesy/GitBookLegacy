setFormPanelMaxLengthXXX(attr,value)
where XXX is the form identifier (CON12) and attr the name of the attribute which identifies a specific input field, and value is the max lenght for the text – returns the value currently set on the input field of the form panel

Every time an event fired within the app must be captured to perform something, an action must be defined an linked to the event. Basically, this is what the Web Designer allows to define. An action is expressed as a set of Javascript instructions.
This language has been chosen because it can be interpreted by both the platforms: iOS and Android, so you can define once the application and use it on any platform, thanks to the portability of Javascript.
Platform provides a series of utility methods you can incllude in your Javascript scriptlets, described below.
Independently of the javascript code you&#8217;ll include in your actions, bear in mind that the javascript code must be interpreted on the embedded js interpreter for iOS and Android. These interpreters are not as good as the ones available for desktop computers.
showm
There are a view limitations you have to take into account when writing javascript code:

| Do not use |  **Correct solution**  |
| :--- | :--- |
| if (variable) | if (variable!=null) |
|  var1===var2 |  var1==var2 |
|  var1!==var2 |  var1!=var2 |
|  eval(jsonString) |  JSON.parse(jsonString) //jsonString must be !=null and !=&#8221;&#8221; |
|  var a = b || c |  var a = b!=null?b:c; |
|  replace a char var newStr = str.replace(/-/g,&#8221;&#8221;) |  var oRegExp = new RegExp(&#8220;-&#8220;,&#8221;g&#8221;); var newStr = str.replace(oRegExp, &#8220;&#8221;); |



showConfirmDialog(args,callbackSuccess(outcome),callbackCancel(outcome))
Show a not blocking confirm dialog, with an "Ok" and "Cancel" buttons; a callback function is invoked when closing the window: the outcome parameter is filled with "Y" ("Ok" button pressed) or "N" ("Cancel" button pressed).
Args is a JS object containing optional settings:

* title: dialog title
* subtitle: dialog subtitle
* heightPopup: dialog height
* titleButtonSuccess: "Ok" button text
* titleColorButtonSuccess: "Ok" button foreground color
* colorButtonSuccess: "Ok" button background color
* titleColor: title foreground color
* subtitleColor: subtitle foreground color
* backgroundColor: dialog background color
* titleButtonCancel: "Cancel" button text
* titleColorButtonCancel: "Cancel" button foreground color
* colorButtonCancel: "Cancel" button background color
* placeholderInputValue: placeholder text to show inside an input field to include in the window; it is an alternative to presetInputValue
* presetInputValue: default value to show inside an input field to include in the window; it is an alternative to placeholderInputValue
* keyTypeInputValue: input field type; allowed values in iOS: &#8220;DEFAULT&#8221;, &#8220;PASSWORD&#8221;, &#8220;ASCIICAPABLE&#8221;, &#8220;NUMBERSANDPUNCTUATION&#8221;, &#8220;URL&#8221;,
&#8220;NUMBER&#8221;, &#8220;PHONE&#8221;, &#8220;NAMEPHONE&#8221;, &#8220;EMAIL&#8221;, &#8220;DECIMAL&#8221;, &#8220;TWITTER&#8221;, &#8220;WEBSEARCH

## Example

```js
var risp = new Object();
risp.title = "This is the window title";
risp.subtitle = "This is the window sub-title, if needed";
risp.titleButtonSuccess = "Ok"; // this is the text for the ok button
var callbackSuccess = function(outcome) {
};
var callbackCancel = function(outcome) {
};
showConfirmDialog(risp,"callbackSuccess","callbackCancel"); // the second argument is the name of the callback function to invoke when the user would press on the Ok button; you have to pass "" if no callback function is needed. The third argument is related to the name of the callback function to invoke when the user would press on the Cancel button.
```

Pay attention that you have to specify the name of the function, NOT the function itself as the second/third argument of this method. Also, the parameter is MANDATORY, pass &#8220;&#8221; if no callback is needed.

showMessageDialog(args,callbackSuccess)
Show a not blocking message dialog, with an "Ok" button; a callback function is invoked when closing the window.
Args is a JS object containing optional settings:

* title: dialog title
* subtitle: dialog subtitle
* heightPopup: dialog height
* titleButtonSuccess: "Ok" button text
* titleColorButtonSuccess: "Ok" button foreground color
* colorButtonSuccess: "Ok" button background color
* titleColor: title foreground color
* subtitleColor: subtitle foreground color
* backgroundColor: dialog background color
* placeholderInputValue: placeholder text to show inside an input field to include in the window; it is an alternative to presetInputValue
* presetInputValue: default value to show inside an input field to include in the window; it is an alternative to placeholderInputValue
* keyTypeInputValue: input field type; allowed values in iOS: &#8220;DEFAULT&#8221;, &#8220;PASSWORD&#8221;, &#8220;ASCIICAPABLE&#8221;, &#8220;NUMBERSANDPUNCTUATION&#8221;, &#8220;URL&#8221;,&#8220;NUMBER&#8221;, &#8220;PHONE&#8221;, &#8220;NAMEPHONE&#8221;, &#8220;EMAIL&#8221;, &#8220;DECIMAL&#8221;, &#8220;TWITTER&#8221;, &#8220;WEBSEARCH

## Example

```js
var risp = new Object();
risp.title = "This is the window title";
risp.subtitle = "This is the window sub-title, if needed";
risp.titleButtonSuccess = "Ok"; // this is the text for the ok button
showMessageDialog(risp,""); // the second argument is the name of the callback function to invoke when the user would press on the Ok button; you can pass "" if no callback function is needed.
```

Pay attention that you have to specify the name of the function, NOT the function itself as the second argument of this method.


logger(logMessage)
Log a message in the internal app console, in order to see it in the Log Panel.
Note: There is also the &#8220;log&#8221; standard javascript method, used to log on the app console, but in this case, the messages will not be visible in the Log Panel.

deleteObject(object, tableName, fireWhenErrors)
generate a SQL delete instruction in the specified table, starting from the javascript object passed as argument: the record having the object pk will be deleted; fireWhenErrors: true|false

updateObject(object, tableName, fireWhenErrors) 
generate a SQL update instruction in the specified table, starting from the javascript object passed as argument; fireWhenErrors: true|false

insertObject(object, tableName, fireWhenErrors)
 generate a SQL insert instruction in the specified table, starting from the javascript object passed as argument; fireWhenErrors: true|false

executeQuery(query, dbType, fireWhenErrors, params)
executeSql(query, dbType, fireWhenErrors, params)
execute the specified SQL query on the specified database; allowed values for dbType are: "DBCON" (platform tables), "DBRO" (readonly tables), "DBRW" (readwrite tables); fireWhenErrors: true|false, params: a list of parameters, expressed with ?; returned value is a list of objects. Each object has value identifiers defined as attributes (select fields in camel mode) 
 **NOTE: Use executeQuery to select values, and executeSql to update/insert records!**   
## Example

```js
var list = executeQuery(
  "SELECT ...", 
  "DBRW", 
  true, 
  []
);
var json = convertToListResponseJson(list); 
return json;
```


getPartialResult(query, dbType, fireWhenErrors, params)
execute the specified SQL query on the specified database; when linked to a grid, it inherits filtering, sorting and pagination conditions from the grid, so that it can apply automatically filters, sortings and read a block of data instead of the whole result set.
Allowed values for dbType are: "DBCON" (platform tables), "DBRO" (readonly tables), "DBRW" (readwrite tables); fireWhenErrors: true|false, params: a list of parameters, expressed with ?; returned value is a list of objects. Each object has value identifiers defined as attributes (select fields in camel mode)   
## Example

```js
var listResponse = getPartialResult(
  "SELECT ...", 
  "DBRW", 
  true, 
  []
);
var json = convertToListResponseJson(listResponse.rows,listResponse.rows.length,listResponse.moreRows);
return json;
```


executeAction(actionId, params)
execute the specified Action and returns the result.
actionId: a String with the id of the action to execute;
params: an object with params to use in the action to execute. These params are accessible in the action to execute by vo.xxx or vo[&#8216;xxx&#8217;]
## Example

```js
var myArgs = {};
myArgs.title = "This is the title";
myArgs.message = "This is the message";
executeAction("123", myArgs);

------
on the action with id 123:

var message = {};
message.title = vo.title;
message.subtitle = vo.message;
message.titleButtonSuccess = "bye";

showMessageDialog(message, null);
```


changeCredentials(username, password)
replace the current account with the one specified through &#8220;saveCredentials&#8221; method and use it by now

saveCredentials(username, password)
save the specified username and password in a permanent area

clearInitialWindow()
remove the start window.

setMenuType(menuType)
change the menu type used by the app

changeUser(value)
change the username associated to the app

sync()
start the synchronization task

getGPSLongitude() 
returns the longitude GPS coordinate, expressed as a string

getGPSLatitude()
returns the latitudine GPS coordinate, expressed as a string

resizeAndSaveImage(sPNG, compression, width, height, path_sorg, pathDest)
where sPNG is a string having ‘true’ or ‘false’ value, compression is a number between 0.5 and 1, width/height represent the final size of the image currently stored in the path_sorg path and to re-create in pathDest, by resizing it

getFormPanelLabelXXX(attr)
where XXX is the form identifier (CON12) and attr the name of the attribute which identifies a specific input field &#8211; returns the text of the input field label or button of the form panel

setFormPanelLabelXXX(attr,value)
where XXX is the form identifier (CON12) and attr the name of the attribute which identifies a specific input field &#8211; set the specified text in the input field label or button of the form panel

getFormPanelValueXXX(attr)
where XXX is the form identifier (CON12) and attr the name of the attribute which identifies a specific input field &#8211; returns the value currently set on the input field of the form panel

setFormPanelValueXXX(attr,value)
where XXX is the form identifier (CON12) and attr the name of the attribute which identifies a specific input field &#8211; set the specified value in the input field of the form panel

setVisibleComponent(attr,visible)
Set the visibility state for the input control belonging to the current form panel, identified by the attribute name. The second argument can have the values &#8220;Y&#8221; or &#8220;N&#8221;, used to set the visibility

```js
setVisibleComponent("controlName","Y");
or
setVisibleComponent("controlName","N");
```


setVisibleColumn(attr,visible)
Set the visibility state for a column in grid; the column is identified by the attribute name. The second argument can have the values &#8220;Y&#8221; or &#8220;N&#8221;, used to set the visibility.
This method can be invoked only before showing the grid, so it should be used within a js action binded to a &#8220;before rendering grid&#8221; event.

```js
setVisibleColumn("columnName","Y");
or
setVisibleColumn("columnName","N");
```


addFilter(fieldName,op,value)
add a filtering condition to the filter panel search. Typically, this instruction is added to a js action linked to the &#8220;before search&#8221; event of the Search button in a filter panel.
Required parameters:

fieldName &#8211; physical field name; the table name is not required
op &#8211; the SQL operator, like: =, &lt;, &gt;, etc.
value &#8211; a string representing the filter value


removeFilter(fieldName)
Remove a filtering condition from the filter panel search. Typically, this instruction is added to a js action linked to the &#8220;before search&#8221; event of the Search button in a filter panel.
Required parameters:

fieldName &#8211; physical field name; the table name is not required; any filtering condition having this field name will be removed


insertFormPanelXXX()
where XXX is the form identifier (CON12) &#8211; switch the form in insert mode

saveFormPanelXXX()
where XXX is the form identifier (CON12) &#8211; save the content of a form panel (which can be in insert or edit mode)

reloadGridPanelXXX(args)
where XXX is the grid identifier (CON12) &#8211; reload the content of the grid

```js
var args = new Object();
args['INPUT_PARAM'] = 'EXAMPLE';

reloadGridPanel603(args);
```


reloadFormPanelXXX(args)
where XXX is the form identifier (CON12) &#8211; reload the form content

```js
var args = new Object();
args['INPUT_PARAM'] = 'EXAMPLE';

reloadFormPanel603(args);
```


reloadPreviewPanelXXX(args)
where XXX is the preview identifier (CON12) &#8211; reload the content of the preview panel

```js
var args = new Object();
args['INPUT_PARAM'] = 'EXAMPLE';

reloadPreviewPanel603(args);
```


loadHTMLOnPreviewPanelXXX(html)
where XXX is the preview identifier (CON12) &#8211; load the html in the preview panel

```js
var html = "&lt;html&gt;&lt;body&gt;.....&lt;/body&gt;&lt;/html&gt;"

loadHTMLOnPreviewPanel603(html);
```


reloadGalleryPanelXXX(args)
where XXX is the gallery identifier (CON12) &#8211; reload the content of the gallery panel

```js
var args = new Object();
args['INPUT_PARAM'] = 'EXAMPLE';

reloadGalleryPanel603(args);
```


openWindowXXX(args)
where XXX is the window identifier (CON08) &#8211; open the specified window

showInputDialog(args,callbackSuccess(outcome),callbackCancel(outcome))

 show a not blocking input dialog, with an "Ok" and "Cancel" buttons and an input text field; the input field is pre-filled with the default input value, if available; a callback function is invoked when closing the window: the outcome parameter is filled with the value typed by the user.
Args is a JS object containing optional settings:


* title: dialog title
* subtitle: dialog subtitle
* heightPopup: dialog height
* titleButtonSuccess: "Ok" button text
* titleColorButtonSuccess: "Ok" button foreground color
* colorButtonSuccess: "Ok" button background color
* titleColor: title foreground color
* subtitleColor: subtitle foreground color
* backgroundColor: dialog background color
* titleButtonCancel: "Cancel" button text
* titleColorButtonCancel: "Cancel" button foreground color
* colorButtonCancel: "Cancel" button background color
* presetInputValue: pre-set input value 
* placeholderInputValue: placeholder input value
* keyTypeInputValue: keyboard type to use when typing the value; iOS allowed values are: 
* DEFAULT
* ASCIICAPABLE
* NUMBERSANDPUNCTUATION
* URL
* NUMBER
* PHONE
* NAMEPHONE
* EMAIL
* DECIMAL
* TWITTER
* WEBSEARCH

## Example

```js
var opts = new Object();
opts['title'] = 'Invia mail';
opts['subtitle'] = 'To:';
opts['keyTypeInputValue'] = 'DEFAULT';
opts['titleButtonSuccess'] = 'Send';
opts['titleButtonCancel'] = 'Cancel';

var callbackSuccess = function(outcome) {};

var callbackCancel = function(outcome) {};

showInputDialog(
 opts,
 "callbackSuccess",
 "callbackCancel"
);
```


showListDialog(args,callbackSuccess(itemIndex),callbackCancel)
Show a dialog containing a list of descriptions. The user can choose one of more of them and a callback function is invoked with the selected items as argument.
Args is a JS object containing optional settings:

* title: dialog title
* subtitle: dialog subtitle
* heightPopup: dialog height
* titleColor: title foreground color
* subtitleColor: subtitle foreground color
* backgroundColor: dialog background color
* list: Array containing the objects, one for each row
* attrName: row identifier; it must be one of the object attributes
* cancelAllowed: allowed values are &#8220;Y&#8221; o &#8220;N&#8221;
* titleButtonCancel: &#8220;Cancel&#8221; button text
* titleColorButtonCancel: &#8220;Cancel&#8221; button foreground color
* colorButtonCancel: &#8220;Cancel&#8221; button background color

## Example

```js
var descriptions = [
  { description: "Item One", code: "Code1" },
  { description: "Item Two", code: "Code2" }
];
        
var fun = function(ris) {
  // ris contains the INDEX of the selected item
  log(descriptions[ris].code;
};
var opts = {};
opts.title = "Select an item";
opts.list = descriptions;
opts.attrName = "description";
opts.cancelAllowed = "Y";
showListDialog(opts,"fun");

```


Pay attention that you have to specify the name of the function, NOT the function itself as the second argument of this method.

 showContactsList(dataToShow,callback(array)) 
Show the list of contacts from the local Agenda.
Required arguments:

* dataToShow type of data to show: it can be a phone number or an email address ; allowed values: &#8220;telephone&#8221; or &#8220;emails&#8221;)


getUsername()
get the current user id

getApplicationId()
get the current application id

getToken()
 get the authentication token, which can be used in case you need to invoke Platform web services; the parameter to include in the URL is: "&amp;restfulToken="+getToken()
Note: It is strongly recommended to pass a String value, not a complex object, to ensure compatibility between Android and iOS apps

setUserSessionVariable(varName,varValue)
store temporarrely a value in the user mobile session; value is referred by the varName
The same value is also automatically passed to the server side, in order to make it available within business components or server-side javascript actions.
You can refer such a variable:

* within SQL type business components using the notation  **:VARIABLENAME** 
* within javascript type business components using the notation  **utils.getVariable(varName)** 
* within server-side javascript type actions using the notation  **utils.getVariable(varName)** 


getUserSessionVariable(varName)
get a value previously stored in the user mobile session; value is fetched starting from the varName identifier

getBaseURL()
Fetch the base URL used by the app to connect to Platform&#8217;s server side installation. This method is tipically used by getWebContent method.

getWebContent(url,httpMethod,contentType,bodyRequest)
execute the HTTP request.
Required parameters:

* url &#8211; URI to invoke (e.g. http://host:port/webcontent)
* httpMethod &#8211; HTTP method to use; allowed values: GET, POST, PUT, DELETE
* contentType &#8211; optional, can be null; e.g. application/json
* bodyRequest &#8211; optional, can be null; the body request, expressed as a String
* The return value is a String content.

## Example

```js
var url = getBaseURL()+"/executeJs?applicationId=...&amp;appId=...&amp;actionId=...&amp;otherparameters&amp;restfulToken="+getToken();
var json = getWebContent(url,"GET","application/json",null);
```




 shareDocument(path, filename)
Open the dialog for share the document. The dialog content depends on the specific mobile platform (Android or iOS).
Required parameters must be included in a javascript object, containing the following attributes:

* path &#8211; the path file, including the file name
* filename &#8211; the name of the file (with the extension)

A typical usage of this method is combined with getRemoteFileURL() method, used to get the right (remote) path for a file stored in the Platform central site, within a specific directory.

 downloadDocument(path, filename)
In Android launch the download of the file (Save the file in the default download folder), in iOs open the dialog for share or download the file (the dialog is the same as the shareDocument methot).
Required parameters must be included in a javascript object, containing the following attributes:

* path &#8211; the path file, including the file name
* filename &#8211; the name of the file (with the extension)

A typical usage of this method is combined with getRemoteFileURL() method, used to get the right (remote) path for a file stored in the Platform central site, within a specific directory.

 shareText(Text)
Open the dialog for share the text. The dialog content depends on the specific mobile platform (Android or iOS).
A typical usage of this method is for share a text on link by Whatsapp o the Email app.

 shareText(Text, imageUrl, appType)
Open the dialog for share the text. The dialog content depends on the specific mobile platform (Android or iOS).
A typical usage of this method is for share a text on link by Whatsapp o the Email app.

* text &#8211; Text to share, can be a link
* imageUrl &#8211; use only if attType is EMAIL to attach an image to the email
* appType &#8211; EMAIL, FACEBOOK, WHATSAPP, SMS, ALL


openRemoteDocument(fileName,url)
open a remote document in a full-size window.
Required parameters are:

* fileName &#8211; file name to show on top of the window
* url &#8211; a remote URL to invoke, in order to get the document

A possible usage of this method is combined with getBaseURL() and getToken() methods, used to get a document from the Platform central site, as for a PDF report.
If this is your need, this is the typical js code to include:

```js
var url = 
  getBaseURL()+
  '/reports/getReport?'+
  'applicationId=...&amp;appId=...&amp;'+
  'reportName=reports/myreporttemplate.jasper&amp;'+
  'datastoreId=...&amp;reportFormat=PDF&amp;'+
  'restfulToken='+getToken();

var json = getWebContent(url,"GET","application/json",null);
var response = eval("("+json+")");
if (response.success) {
    var title = "Report.pdf";
    var url = 
      getBaseURL()+'/showDocument?ì+
      'applicationId=MOBILE11&amp;title='+title+
      '&amp;docId='+response.data.docId+
      '&amp;exportFormat='+response.data.exportFormat+
      '&amp;restfulToken='+getToken();

    openRemoteDocument(title,url);
}
```



getRemoteFileURL(dirId,filename)
Get the complete URL to get a document path, previously stored in the Platform central site, within a specific directory.
Required parameters are:

* dirId &#8211; remote directory id, defined through the Web Designer
* filename &#8211; the remote file name, stored within the specified directory.


getAppParameter(name)
Get a parameter value defined at application level, through the Web Designer in the Application Parameter folder of the App detail window.
Required parameters are:

* name &#8211; parameter name


getPanelParameter(name)
Get a parameter value passed to the current panel (trough the window args variable).
Required parameters are:

* name &#8211; parameter name

## Example

```js
//From the window "A" I open the window "B"

//Window A
var args = {
    param1: "MyCustomParam"
};

//...
//Window B
getPanelParameter('param1');   //Output: "MyCustomParam"

```



setPanelParameter(name,value)
Store a parameter value within the current panel scope. It can be referred in SQL instructions or js instructions as :PARAMETERNAME variables.
Required parameters are:

* name &#8211; parameter name
* value &#8211; parameter value


showCardPanel(cardPanelID, panelID)
Switches from a card to another inside a cardPanel.
Required parameters are:

* cardPanelID &#8211; The ID of the cardPanel (parent panel)
* panelID &#8211; The ID of the card to focus (child panel)


openPreview(directoryId, fileName)
Show on a modal full size window a web content stored online on the Platform server, identified by the specified directory + file name.
Required parameters are:

* directoryId &#8211; The directory id identifying the absolute path where the resource has been stored on the Platform server
* fileName &#8211; filename related to the web resource to download and show


convertToListJson(list)
Convert a javascript list returned by the executeQuery method to a JSON string having format: [{&#8230;.},{&#8230;},&#8230;]
## Example

```js
var listResponse = getPartialResult(
  "SELECT ...",  
  "DBRW", 
  true, 
  []
);
var json = convertToListJson(listResponse.rows);
var res = '{ "moreRows": false, "valueObjectList": '+json+' }';
return res;
```



convertToListResponseJson(list,length,moreRows)
Convert a javascript list returned by the executeQuery method to a JSON string having format: { moreRows: &#8230;, valueObjectList: [{&#8230;.},{&#8230;},&#8230;] }
## Example

```js
var listResponse = getPartialResult(
  "SELECT ...", 
  "DBRW", 
  true, 
  []
);
var json = convertToListResponseJson(listResponse.rows,listResponse.rows.length,listResponse.moreRows);
return json;
```



convertToObjectJson(list,length,moreRows)
Convert a javascript object contained in the list returned by the executeQuery method to a JSON string corresponding to that object.
## Example

```js
var listResponse = executeQuery(
  "SELECT ...", 
  "DBRW", 
  true, 
  []
);
var json = convertToObjectJson( list[0] );
return json;
```



forceValidation(attributeName)
After setting a value to a lookup control, force the validation, by specifying the attribute name identifying the right lookup control.
Required parameters are:

* attributeName &#8211; attribute name identifying the lookup control where forcing the validation.


setBackgroundColorComponent(attributeName, hexBackgroudColor)
Sets the background color of the component.
Required parameters are:

* attributeName &#8211; attribute name identifying the component.
* hexBackgroudColor &#8211; color code in hexadecimal


closeWindow()
Close current visible window and move back to the previous one.

pull()
Get data from each input control and refresh the value object behind the form/editable panel.

checkMandatoryControls()
Check the current panel (form or editable panel) for mandatory input controls not filled: when finding one, shows a message dialog with the control name violating the mandatory property. The method returns &#8220;true&#8221; (no mandatory controls found) or &#8220;false&#8221; (a string), according to the outcome.

getCurrentDate()
Return an internal string representation of the current date (with &#8220;yyyy-MM-dd&#8221; format), that can be used when creating javascript objects to insert/update and you need to pass a date.

getCurrentDateAndTime()
Return an internal string representation of the current date (with &#8220;yyyy-MM-dd HH:mm:ss&#8221; format), that can be used when creating javascript objects to insert/update and you need to pass a date.

addDate(timeInMillis,format,amount)
Return an internal string representation of the current date (with &#8220;yyyy-MM-dd HH:mm:ss&#8221; format) plus an amount which can be specified with different formats, that can be used when creating javascript objects to insert/update and you need to pass a date.
Required parameters are:

* timeInMillis &#8211; number of milliseconds.
* format &#8211; string having one of these values: &#8220;DAY&#8221;, &#8220;MONTH&#8221;, &#8220;YEAR&#8221;, &#8220;HOUR&#8221;, &#8220;MINUTE&#8221;, &#8220;SECOND&#8221;; it can be null, if not null then also the &#8220;amount&#8221; parameter is required
* amount &#8211; number of days/months/&#8230; to add to the current date/time

## Example

```js
var s = getCurrentDate();
log("Current date with format yyyy-MM-dd "+s);

s = getCurrentDateAndTime();
log("Current Date with format yyyy-MM-dd HH:mm:ss "+s);

var dt = new Date();
var l = dt.getTime();
s = addDate(l);
log("Current date with format yyyy-MM-dd HH:mm:ss "+s);

s = addDate(l,"DAY",1);
log("Current date + 1 day with format yyyy-MM-dd HH:mm:ss "+s);

```


checkConnection();
Check if there is an Internet connection available: if there is, then returns &#8220;true&#8221; (a String), otherwise &#8220;false&#8221;.

setEnabledComponent(attr,enable)
Set the enable state for the input control belonging to the current form panel, identified by the attribute name. The second argument can have the values &#8220;Y&#8221; or &#8220;N&#8221;, used to set the enable
setEnabledComponent(panelId, attr, enable)
The same as above, but you can also pass the panelId as the first parameter

scanQRCode(callbackSuccess, callbackCancel, callbackError);
Open a QR code reader and execute the scan. 
Required arguments:

callbackSuccess &#8211; function name which will be invoked in case of successful scan; an argument is passed to the function: a json with data just read, expressed as a string

QRCode with a VCARD:

```js
{
  "displayValue": "Name Surname",
  "format": "QR_CODE",
  "rawValue": "BEGIN:VCARD\nVERSION:2.1\nFN:Name Surname\nN:Surname;Name\nTITLE:Mr\nTEL;CELL:+3912345678\nTEL;WORK;VOICE:+ 3912345678\nTEL;HOME;VOICE:+ 3912345678\nEND:VCARD\n",
  "valueFormat": "CONTACT_INFO"
}
```


QRCode with a VCARD:

```js
{
 "displayValue":"http://www.sinesy.it",
 "format": "QR_CODE",
 "rawValue":"http://www.sinesy.it",
 "valueFormat":"URL"
}
```


Note 1: iOs does not support valueFormat
Note 2: in iOs there is not difference between displayValue and rawValue


callbackSuccess &#8211; function name which will be invoked in case the user interrupts the scan
callbackError &#8211; function name which will be invoked in case of failed scan; an argument is passed to the function: the error code, expressed as a stringSupported barcodes are: EAN-13, EAN-8, UPC-A, UPC-E, Code-39, Code-93, Code-128, ITF, Codabar, QR Code, Data Matrix, PDF-417, AZTEC


scanBarcode(callbackSuccess, callbackCancel, callbackError);
Open a barcode reader and execute the scan. 
The supported format are:  EAN-13, EAN-8, UPC-A, UPC-E, Code-39, Code-93, Code-128, ITF, Codabar, QR Code, Data Matrix, PDF-417, AZTEC, note that iOS does not support: Codabar and UPC-A.
Required arguments:

callbackSuccess &#8211; function name which will be invoked in case of successful scan; an argument is passed to the function: a json with data just read, expressed as a string

EAN13 with a PRODUCT:

```js
{
 "displayValue":"5901234123457",
 "format": "EAN_13",
 "rawValue":"5901234123457",
 "valueFormat":"PRODUCT"
}
```


Note 1: iOs does not support valueFormat
Note 2: in iOs there is not difference between displayValue and rawValue


callbackSuccess &#8211; function name which will be invoked in case the user interrupts the scan
callbackError &#8211; function name which will be invoked in case of failed scan; an argument is passed to the function: the error code, expressed as a stringSupported barcodes are: EAN-13, EAN-8, UPC-A, UPC-E, Code-39, Code-93, Code-128, ITF, Codabar, QR Code, Data Matrix, PDF-417, AZTEC


openCamera(callback);
Open the camera to take a photo. In case it has been successfully taken, the callback will be invoked. The callback method will have the absolute path to the local image just stored.
Required arguments:

callback &#8211; function name which will be invoked in case the photo has been successfully taken; an argument is passed to the function: the absolute path of the image just saved, expressed as a string

## Example

```js
var getPhoto = function(imagePath) {
  // do something with the image...
}

openCamera("getPhoto");

```


 openGallery(callback);
Open the local gallery to choose a photo. When the image is selected, the callback will be invoked. The callback method will have the absolute path to the local image just selected.
Required arguments:

callback &#8211; function name which will be invoked when an image from the gallery is chosen; an argument is passed to the function: the absolute path of the image just selected, expressed as a string

## Example

```js
var getPhoto = function(imagePath) {
  // do something with the image...
}

openGallery("getPhoto");

```


 sendFile(url, filePath, fileName, jsCallback);
Invoke a remote server to pass a local file using the POST HTTP method and the multi-part content type: a file and a filename will be passed.
At the end of the sending process, the jsCallback will be invoked.
Required arguments:

url &#8211; URL to invoke
filePath &#8211; absolute path (without the file name) in the local file system related to the file to send
fileName &#8211; file name to send; it is located in the absolute path specified through the previous argument
callback &#8211; function name which will be invoked when the file has been successfully sent; an argument is passed to the function, containing the response of the web service invoked

In the following example, a predefined Platform web service is invoked: it has been designed to work withHTTP requests having POST method and multi-part content-type. Moreover, such a web service requires an action id which will be automatically invoked after sending the file. You can use it to process the file in some way and get back a response to the client.

```js
var myCallback = function(responseFromWebService) {
  // do something with the response
}
var filePath = ...
var fileName = ....
 
var url = getBaseURL() + "/executeJs/uploadfiles?appId=...&amp;applicationId=...&amp;actionId=...&amp;dirId=...&amp;unzip=false&amp;restfulToken="+getToken();
sendFile(url, filePath, fileName, "myCallback");


```



 showCardPanel(idPanelContainer, idCardPanel);
Set the panel to show inside a panel container having cardpanel type.
Required arguments:

idPanelContainer &#8211; panel identifier having cardpanel type; such a panel will have several subpanel in it and only one of them is shown at a time
idCardPanel &#8211; identifier for the panel to show inside the panel container



 panelScreenshot(idPanel);
Generate an image of the panel shown in the app, identified by idPanel and save it in the local file system. The method gets back the absolute path + image name for the just generated screenshot.
Required arguments:

id &#8211; identifier of the panel to capture
return the absolute path + image name for the just generated screenshot.


shareOrDownloadDocument(pathToShare,filename);
Open a dialog through which the end user can choose an app where sharing the specified file. It is also possible to choose to download the file locally.
Required arguments:

pathToShare &#8211; absolute path where the file to share/download is located
filename &#8211; name of the file to share/download, located in the specified absolute path


shareDocument(path,filename);
Open a dialog through which the end user can choose an app where sharing the specified file. 
Required arguments:

path &#8211; absolute path where the file to share is located
filename &#8211; name of the file to download, located in the specified absolute path


downloadDocument(path,filename);
Open a dialog through which the end user can download locally the specified file. 
Required arguments:

path &#8211; absolute path where the file to download is located
filename &#8211; name of the file to share, located in the specified absolute path


setWindowTitle(title);
Change the title of the window currently shown. 
Required arguments:

title &#8211; the title to set in the currently shown window


PUSH NOTIFICATIONS
Through the following  **server-side**  javascript function you can notify via push notification the mobile app.
utils.sendPushNotification(appId, usernamesList, title, body, actionIdToCall, valueObject, iOSBadgeCount);

```js
var usersEmails = ["email1@gmail.com","email2@gmail.com","emailN@gmail.com"]; //an array of registered user email accounts
var appMobileId = "MINION"; //the mobile application id
var notificationTitle = "Hello!"; //notification title
var notificationBody = "How did the cat get so fat?"; //notification body
var actionIdToCall = 123; //[optional] mobile actionId to call on the notification click if necessary
var valueObject = {"field1":"value1","field2":"value2","fieldN":"valueN"}; //[optional] map of &lt;String, String&gt; to use in the action id if necessary
var iOSBadgeCount = 1; //Total count of notification
    
utils.sendPushNotification(appMobileId, usersEmails , notificationTitle, notificationBody, 123, JSON.stringify(valueObject), iOSBadgeCount);
```

When the push notification reaches the mobile application, it calls the optional actionId defined in the  **sendPushNotification**  injecting in the valueObject a parameter with the status of the push:

```js
vo.notificationFieldStatus = "RECEIVED"
```

When the user clicks on the notification, the mobile app calls the optional actionId defined in the  **sendPushNotification**  injecting in the valueObject a parameter with the status of the push:

```js
vo.notificationFieldStatus = "CLICKED"
```

This is an example of the optional actionIdToCall:

```js
if(vo.notificationStatus == "RECEIVED"){
    
    //For example this will update the "ideas" menu badge count with the count of unread notifications
    var unreadNotification = getUnreadNotificationsCount();
    setMenuBadges("ideas",unreadNotification);

} else if(vo.notificationStatus == "CLICKED"){

    //Reset the notification count
    resetUnreadNotifications();
    
    //update the "ideas" menu count
    setMenuBadges("ideas",0);
    
    //Open the window 39
    var args = {
       "param1":vo.field1,
       "param2":vo.field2,
       "paramN":vo.fieldN
    };
    openWindow39(args);  
    
}
```


getUnreadNotificationsCount();
Returns the unread notifications count

setMenuBadges(menuFunctionId, count);
Sets the badge for the menu item by its functionId

resetUnreadNotifications();
Sets to zero the unread notifications count.
After this, the method  **getNotificationsCount()**  will return zero.
This method doesn&#8217;t update the menu item badge, you have to call

clearSearchFilterPanelXXX()

where XXX is the filter panel identifier (CON12) &#8211; clean the components of panel

applySearchFilterPanelXXX()
where XXX is the filter panel identifier (CON12) &#8211; apply the filter conditions of panel to linked grid

reloadMapPanel

where XXX is the form identifier (CON12) &#8211; reload the form content

```js
var args = new Object();
args['INPUT_PARAM'] = 'EXAMPLE';

reloadMapPanel603(args);
```


setEnabledPanelButtonXXX(buttonId, enable)
Enable or disable the button in panel
Required arguments:

* XXX is the panel identifier
* buttonId &#8211; key of button component
* enable &#8211; Y/N for enable or disable


setFormPanelMaxLengthXXX(attr,value)
Set the max length for an input text.
Required arguments:

* XXX is the panel identifier (CON12)
* attr -the name of the attribute which identifies a specific input field
* value &#8211; the max length for the text


setFormPanelPlaceholder(panelId,attr,placeholder)
The placeholder attribute specifies a short hint that describes the expected value of an input field (e.g. a sample value or a short description of the expected format).
The short hint is displayed in the input field before the user enters a value.
Required arguments:

* XXX is the panel identifier (CON12)
* attr -the name of the attribute which identifies a specific input field
* placeholder &#8211; is the short hint that describes the expected value of an input field


getPaletteFromImage(filePath)

Returns the color palette from an image, the palette si an array like:  [[r,g,b],&#8230;.,[r,g,b]]
Required arguments:

* filePath is the path of a local image (no remote file)


```js
var palette = getPaletteFromImage(filePaht);
var paletteArray = JSON.parse(palette);
```


syncSqlInstruction()
Send to server the sql instractions of data modified. This operation not is a total sync.

showToast(message)
A toast provides simple feedback about an operation in a small popup. It only fills the amount of space required for the message and the current activity remains visible and interactive. Toasts automatically disappear after a timeout.

setPanelOptionalParameterXXX(parName, value)
Set the optional parameter for panel grid or detail
Required arguments:

* XXX is the panel identifier
* parName &#8211; name of parameter
* value &#8211; value to set for parName


getPanelOptionalParameterXXX(parName)
Return the value of optional parameter of panel grid or detail ()
Required arguments:

* XXX is the panel identifier
* parName &#8211; name of parameter


openUrl(url)
Open the browser whith url

setCustomColumnHeader(attributeName, header)
Set the header of attribute name column for current grid  **(action must be executed BEFORE RENDER)** 
Required arguments:

* attributeName &#8211; key of column
* header &#8211; text for column header


getMode()

Returns the mode (READONLY, INSERT or EDIT) of current panel

getFilterPanelValueXXX(attr)
where XXX is the filter identifier (CON12) and attr the name of the attribute which identifies a specific input field &#8211; returns the value currently set on the input field of the filter panel

```js
getFilterPanelValue1559("attributeName");

```


setFilterPanelValueXXX(attr,value)
where XXX is the filter identifier (CON12) and attr the name of the attribute which identifies a specific input field &#8211; set the specified value in the input field of the filter panel

```js
setFilterPanelValue1559("attributeName", "value");

```


setFocusByAttributeXXX(attr)
where XXX is the panel identifier (CON12) and attr the name of the attribute which identifies a specific input field &#8211; set the focus on the component

```js
setFocusByAttribute1559("attributeName");

```


setUserAppCustomVariable(varNames,varValues)
store temporarily a value in the user mobile and server session; value is referred by the varName
varNames and varValues can be a list of comma separated strings

```js
var valueOfVarName = setUserAppCustomVariable('varName', 'value');
setUserAppCustomVariable('varName1,varName2,varName3', 'value1,value2,value3');
```


getUserAppCustomVariable(varName)
get a value previously stored in the user mobile and server session; value is fetched starting from the varName identifier

```js
var valueOfVarName = getUserAppCustomVariable(varName);
logger('valueOfVarName: ' + valueOfVarName);

```


scrollPanelToXXX(x, y)
where XXX is the panel identifier (CON12), if the panel is scrollable scroll (ex. web preview o grid) the panel to the x and y position specified.

```js
 scrollPanelTo559(0, 0); //scroll panel to top
```






                

---


