Platform makes it possible to create a complex program, through a Javascript action. This program can be executed on the servsender side.
This program can exploit a series a predefined functions and variables, including database access functions; the whole call to this action is transactional, so that all the SQL instructions executed within this action are related to the same SQL transaction: in case of an error, the whole transaction will be rollbacked.
Server-side Javascript can be embedded within either a server-side Javascript action or in a server-side Javascript business component.
In this way, the action can be binded to a client-side or server-side event, in order to perfom complex business logic when a specific event occurs.
Moreover, a list or a tree or a detail form could be fed trough a server-side Javascript busainess component, in case of a very complex data retrieval logic.

A simple way to invoke a server-side javascript action is through an Ajax request:


```js
var response = new SyncRequest().send(contextPath+"/executeJs?applicationId=XXX&amp;actionId=YYY&amp;...",
"POST", jsonStringObject);
```



where jsonStringObject is a string representation of a javascript object; it can be  **null** .
The response represents a string response, typically expressed as a json format string.

When executing this request, the javascript action has access to some predefined variables and methods, described below.

Independently of the type of component embedding the server-side Javascript (an action or a business component), a few predefined variables are always available:

* vo &#8211; the javascript representation of the json string passed through the Ajax request
* reqParams &#8211; a map of related to all request parameters
* userInfo &#8211; a map of , related to the UserInfo java object; e.g. username, languageId, companyId, etc.


Another way to invoke a server-side javascript action is through a special Ajax request where you can upload a file as well.
The request must have the a multipart/form-data content type, as the one provided by the standard HTML form. An example of such a form is reported below:

```js
&lt;html&gt;
&lt;body&gt;
  &lt;form action="/contexpathplatform/executeJs/uploadfile?companyId=...&amp;siteId=100&amp;username=...&amp;password=...&amp;languageId=...&amp;appId=...&amp;actionId=...&amp;dirId=9&amp;unzip=N" 
        method=POST  
        enctype="multipart/form-data" &gt;
  &lt;input type="hidden" name="actionId" value="..." /&gt;
  &lt;input type="hidden" name="dirId" value="..." /&gt;
  &lt;input type="hidden" name="unzip" value="N" /&gt;
  &lt;input type="file" name="fileName"&gt;&lt;br/&gt;
  &lt;input type=submit&gt;
  &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;

```

This call allows to send the file, save it and then invoke the specified action, which must be a server side js action.
All parameters passed to the server are accessible form the action (reqParams), as well as the request headers (reqHeaders).
The file name is also included in vo as the attribute fileName.
The dirId is optional: if not specified, the uploaded file is saved in the tmp dir of the Application Server and then passed (absolute path + file name) to vo.fileName
The parameter unzip can have values Y or N: if set to Y, then the uploaded file (which must be a zip file) is automatically unzipped and its content (a single file) is used to set the vo.fileName (absolute path included).


In case of server-side Javascript actions (not js business components), it is also available a simple debugger you can use to control the right execution of the source code you wrote.
In order to stop the execution of the js code at specific positions, there is a special method you have to include in the code:
 **utils.suspend(&#8220;executionpoint&#8221;);** 
where the text specified as argument is used to give a friendly name to the suspendingpoint.
You can add any number of these instructions inside your js action: the execution will be interrupted at each of them.
More precisely, the execution  **is interrupted in a specific action only if**  in the App Designer the user has opened the definition window for that action and has pressed the &#8220;Debug&#8221; button on the right: in that case, a window is opened, showing the list of all executions for that actions which have been suspended.
That means an action will not be suspended until the &#8220;Debug&#8221; window is showed. Again, when closing the &#8220;Debug&#8221; window will makes not working the suspension again. This behavior avoids to stop actions executions when there is no one who is checking them through the Debug window.
In the &#8220;Debug&#8221; window there is a &#8220;Resume&#8221; button which is used to resume the execution of a suspended action.
The &#8220;Resume all&#8221; button is used to resume all the suspended execution for that action.
A double click on a suspended execution will open a detail window where you can see all the variables defined within that action. A righe click on a node of the variables tree will allow you to changethe current value.
Again,there is a &#8220;Resume&#8221; button which is used to resume the execution of a suspended action. When pressing it, you can resume the execution.


Furthermore, there is also a set of predefined methods, accessible through a global object named utils:

Generic SQL execution (NO SQL queries)
## Syntax

```js
var rows = utils.executeSql(sql, dataSourceId, separatedTransaction, interruptExecution, params)
```

## Details

* rows &#8211; int value: number of processed rows
* sql &#8211; string value: sql to execute; it can contains ? or :XXX
* dataSourceId &#8211; num value; it can be null and used to specify a different db to use with the sql statement
* separatedTransaction &#8211; boolean value; if true, the SQL instruction is executed on a separated transaction which is immediately committed (as for a REQUIRE_NEW EJB directive)
* interruptExecution &#8211; boolean value; if true, an erroneous SQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql statement.


An :XXX variable can be replaced by vo or params values

## Example


```js
var updatedRowsNr = utils.executeSql(
"UPDATE PRM01_USERS SET USER_CODE_ID=:USER_CODE_ID, DESCRIPTION=:USER_CODE_ID WHERE COMPANY_ID= :COMPANY_ID AND STATUS=? AND LOCKED=?",
null, // no additional datastore!
false, // do it on a separated transaction
true, // fire an Exception in case of error
["E", "N"]
);
```

 **Note** : every SQL instruction will be logged.


Generic SQL execution (NO SQL queries) without logging it.
## Syntax


```js
var rows = utils.executeSqlNoLog(
sql,
dataSourceId,
separatedTransaction,
interruptExecution,
params
)
```


## Details

* rows &#8211; int value: number of processed rows
* sql &#8211; string value: sql to execute; it can contains ? or :XXX
* dataSourceId &#8211; num value; it can be null and used to specify a different db to use with the sql statement
* separatedTransaction &#8211; boolean value; if true, the SQL instruction is executed on a separated transaction which is immediately committed (as for a REQUIRE_NEW EJB directive)
* interruptExecution &#8211; boolean value; if true, an erroneous SQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql statement.

An :XXX variable can be replaced by vo or params values

## Example

```js
var updatedRowsNr = utils.executeSql(
"UPDATE PRM01_USERS SET USER_CODE_ID=:USER_CODE_ID, DESCRIPTION=:USER_CODE_ID WHERE COMPANY_ID= :COMPANY_ID AND STATUS=? AND LOCKED=?",
null, // no additional datastore!
false, // do it on a separated transaction
true, // fire an Execution in case of error
"E",
"N"
);
```


Note: the SQL operation will not be logged. This method csan be useful with bulk operations, whose execution could slow down if a log message were produced for each execution.

Execute a series of SQL statements, stored in the specified file.
## Syntax


```js
var rows = utils.executeSqlFile(
sqlFile,
dataSourceId,
separatedTransaction,
interruptExecution,
params
)
```


## Details

* rows &#8211; int value: number of processed rows
* sqlFile &#8211; absolute path + file name, related to the SQL script to execute
* dataSourceId &#8211; num value; it can be null and used to specify a different db to use with the sql statement
* separatedTransaction &#8211; boolean value; if true, the SQL instruction is executed on a separated transaction which is immediately committed (as for a REQUIRE_NEW EJB directive)
* interruptExecution &#8211; boolean value; if true, an erroneous SQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql statement.

An :XXX variable can be replaced by vo or params values

SQL query execution
## Syntax


```js
var jsonList = utils.executeQuery(
sql,
dataSourceId,
separatedTransaction,
interruptExecution,
params
)
```


## Details

* jsonList &#8211; string value: list of json objects, i.e. the result of the query execution
* sql &#8211; string value: sql to execute; it can contains ? or :XXX
* dataSourceId &#8211; num value; it can be null and used to specify a different db to use with the sql statement
* separatedTransaction &#8211; boolean value; if true, the SQL instruction is executed on a separated transaction which is immediately committed (as for a REQUIRE_NEW EJB directive)
* interruptExecution &#8211; boolean value; if true, an erroneous SQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql query.


An :XXX variable can be replaced by vo or params values

## Example


```js
var rows = utils.executeQuery(
"SELECT USER_CODE_ID,DESCRIPTION FROM PRM01_USERS WHERE COMPANY_ID=:COMPANY_ID AND STATUS=? AND LOCKED=?",
null, // no additional datastore!
false, // do it on a separated transaction
true, // fire an Execution in case of error
"E",
"N"
);
```

var username = rows[0].userCodeId;


Execute the specified SQL query and enrich it by adding filtering/sorting and pagination settings defined through ListCommand object automatically created when this method is invoked through a "Server JS business component" connected to a grid panel.
## Syntax

* var json = utils.getPartialResult(sql, dataStoreId, separatedTransaction, interruptExecution, pars);
* Details:
* sql &#8211; base SQL query
* dataStoreId &#8211; optional data source id (a number)
* separatedTransaction &#8211; flag used to define if this query has to be perfomed in a separated transaction
* interruptExecution &#8211; flag used to defined if the whole server side transation must be interruped and roolbacked in case of errors
* pars &#8211; optional (can be expressed as [] in js) list of parameters binded to ? variables in the SQL query
* Returns a list of records, expressed in JSON format, which also includes &#8220;valueObjectList&#8221;, &#8220;moreRows&#8221; and &#8220;resultSetLength&#8221; attributes.


In case of a complex SQL query including aliases, it could be needed to decode the field (to filter/sort) from the grid panel into an alias. You can do it through a specific utility method:setDecodeField(fieldToDecode, decodedField).
In this way, you can control exactly which fields to apply in case of filtering or sorting conditions.
## Example

```js
utils.setDecodeField("ROW_VERSION*ROW_VERSION AS RV","RV");
var json = utils.getPartialResult(
    "SELECT USER_CODE_ID,DESCRIPTION,ROW_VERSION*ROW_VERSION AS RV "+
    "FROM PRM01_USERS "+
    "WHERE STATUS='E'",
    null,
    false,
    true,
    []
);

utils.setReturnValue(json);

```



Get translation, given an entry
## Syntax

```js
var translation = utils.getResource(entry)
```


## Details

* translation &#8211; string value: the translation for the entry value
* entry &#8211; string value: the entry to translate


Get translation for a specific language, given an entry
## Syntax

```js
var translation = utils.getResourceByLanguageId(entry, languageId)
```

## Details

* translation &#8211; string value: the translation for the entry value
* entry &#8211; string value: the entry to translate
* languageId &#8211; string value: the language id to use when translating the entry


Get language id for a specific username
## Syntax

```js
var languageId = utils.getLanguageIdFromUsername(userId)
```

## Details

* languageId &#8211; string value: the language id expressed like (IT,EN,&#8230;)
* userId &#8211; string value: the username to use to get language id


Log a message
## Syntax

```js
utils.log(msg, type);
```

## Details

* msg &#8211; string value: message to log
* type &#8211; string value: message type; allowed values:INFO,WARN,DEBUG,ERROR

Since 5.2.1 version

```js
utils.info(msg);

utils.warn(msg);

utils.debug(msg);

utils.error(msg);
```



Set the return message; this method can be omitted; in that case a default jso message with success: true will be sent back.
## Syntax

```js
utils.setReturnValue(response)
```

## Details
response &#8211; string value: messagge to send back


Convert a number to its text representation
## Syntax

```js
var text = utils.numberToText(num, decimals, languageId, showDecimals, sep)
```

## Details

* text &#8211; string value: the text representation of the number (e.g. duecento ventiquattro/00)
* num &#8211; a number, including a decimal number
* decimals &#8211; a number, it is used to round the num to this number of decimals
* languageId &#8211; language identifier
* showDecimals &#8211; true/false; define if the decimal part must be included
* sep &#8211; integer vs decimal separator, e.g. /



Round a number to the specified number of decimals
## Syntax

```js
var result = utils.round(num,decimals)
```

## Details

* result &#8211; rounded decimal number
* num &#8211; a decimal number
* decimals &#8211; number of decimals that the final number must be rounded to



Get absolute path of WEB-INF/classes folder of Platform application
## Syntax

```js
var path = utils.getBasePath()
```

## Details

* path &#8211; the absolute path of WEB-INF/classes folder of Platform application


It can be helpful for instance to get the basedir for a more complex organization of files.


Get a parameter value
## Syntax

```js
var paramValue = utils.getParameter(paramName)
```

## Details

* paramName &#8211; a string value representing a parameter named defined at installation level (CON44 table) or at application level (CON07 table)
* paramValue &#8211; the value defined for the specified parameter name or null if not found; if the parameter is found as an application parameter, that value is returned, otherwise it will be returned the value defined at installation level



Send an email, using SMTP settings defined at application level/globally
## Syntax

```js
utils.sendEmail(from, to, cc, bcc, subject, body, isHtmlContent, returnReceipt, zipFiles, deleteFilesAfterSending, dirId, fileName, filesToAttach)
```


## Details

* from &#8211; (optional, can be null) a string representing the email address to use as the &#8220;from address&#8221; to send the email
* to &#8211; a string composed of one or more email addresses, separated by a comma (,)
* cc &#8211; carbon copy addresses &#8211; a string composed of one or more email addresses, separated by a comma (,)
* bcc &#8211; hidden addresses &#8211; a string composed of one or more email addresses, separated by a comma (,)
* subject &#8211; a string representing the email title
* body &#8211; the email body content
* isHtmlContent &#8211; a boolean flag used to define if the body content is in HTML format or not
* returnReceipt &#8211; a boolean flag used to request a return receipt to the destinators
* zipFiles &#8211; a boolean flag used to compress all files to attach in a unique zip file and send it, in order to reduce the email size
* deleteFilesAfterSending &#8211; a boolean flag used to optionally delete files to attach, after sending the email
* dirId&#8211; optional dir id used to save the message also to the server file system
* fileName&#8211; optional file name required in case the dir id has been specified; the message will be save in eml format on the file system
* filesToAttach &#8211; a list of files to attach, separated by a comma; use [] to notinclude files; each file must include the absolute path

This method will fire an exception if the email has NOT been sent correctly (e.g. attachment file not found).

 **IMPORTANT NOTE** :
In order to use this feature, you have also to define a few parameters:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD


Send an email, using SMTP settings defined at application level/globally
## Syntax

```js
utils.sendEmail(smtpHost, smtpPort, useTLS, protocol, smtpUsername, smtpPassword, from, to, subject, body, isHtmlContent, zipFiles, deleteFilesAfterSending, filesToAttach)
```

## Details

* smtpHost &#8211; SMPT host name to use
* smtpPort &#8211; SMTP port
* useTLS &#8211; flag to use (Y/N) to enable TLS
* protocol &#8211; Protocol to use (e.g. smtp vs smtps)
* smtpUsername &#8211; SMTP username to use to authetication to the SMTP server
* smtpPassword &#8211; SMTP password to use to authetication to the SMTP server
* from &#8211; (optional, can be null) a string representing the email address to use as the &#8220;from address&#8221; to send the email
* to &#8211; a string composed of one or more email addresses, separated by a comma (,)
* cc &#8211; carbon copy addresses &#8211; a string composed of one or more email addresses, separated by a comma (,)
* bcc &#8211; hidden addresses &#8211; a string composed of one or more email addresses, separated by a comma (,)
* subject &#8211; a string representing the email title
* body &#8211; the email body content
* isHtmlContent &#8211; a boolean flag used to define if the body content is in HTML format or not
* returnReceipt &#8211; a boolean flag used to request a return receipt to the destinators
* zipFiles &#8211; a boolean flag used to compress all files to attach in a unique zip file and send it, in order to reduce the email size
* deleteFilesAfterSending &#8211; a boolean flag used to optionally delete files to attach, after sending the email
* filesToAttach &#8211; a list of files to attach, separated by a comma; use [] to notinclude files; each file must include the absolute path


This method will fire an exception if the email has NOT been sent correctly (e.g. attachment file not found).

Create a .docx file starting from a template and save it to the specified absolute path
## Syntax

```js
var file = utils.generateDocx(reportId,args,langId,path,fileName)
```

## Details

* reportId &#8211; long value representing a specific report template in CON66
* args &#8211; a collection of pairs &lt;attributeName,attributeValue&gt; to use to bind queries connected to that report
* langId &#8211; (optional) language that identify the template to use; can be null
* path &#8211; the absolute path where saving the document (it must not include the file name)
* fileName &#8211; (optional) the name to use when creating the file; may be null: in that case, a dynamic name will be assigned automatically
* file &#8211; the file name of the generated .docx file

This method will fire an exception in case of problems when generating the docx file.


Convert a docx file to a pdf file and save it to the file system.
## Syntax

```js
utils.convertDocxToPdf(docxFile, pdfFile, deleteDocxFile)
```

## Details

* docxFile &#8211; string representing the source file, in docx format
* pdfFile &#8211; string representing the new file to create, in pdf format
* deleteDocxFile &#8211; boolean flag used to automatically delete the source file, when the pdf file has been created

Important note: this method can work with 3 alternative implementations behind the scenes:

* using CloudConvert Web Servivce API &#8211; in order to enable this implementation, you have to set the globsl property CloudConv Key, i.e. you have to buy this online service before invoking it
* using LibreOffice Portable &#8211; this product must be installed in the same server hosting Platform; moreover, the global property named "LibreOffice Path" must be defined too. In case you need to convert a docx to a PDF/A (PDF archive format), you have first to change the file &lt;pathlibreoffice&gt;/Data/settings/user/registrymodifications.xcu and change/add the following line:

&lt;item oor:path=&#8221;/org.openoffice.Office.Common/Filter/PDF/Export&#8221;&gt;&lt;prop oor:name=&#8221;SelectPdfVersion&#8221; oor:op=&#8221;fuse&#8221;&gt; **&lt;value&gt;1&lt;/value&gt;** &lt;/prop&gt;&lt;/item&gt;
In that case, all PDFs generated will have this format.

* if none of the previous settings have been defined, a default PDF conversion is used, based on POI open source library, which does not ensure a good PDF conversion anyway.


Stored SQL function execution
## Syntax

```js
var json = utils.executeStoredFunction( sql, dataSourceId, separatedTransaction, interruptExecution, params)
```

## Details

* json &#8211; string value: the result of the function execution
* sql &#8211; string value: stored function to execute, including its parameters
* between parenthesis (see example below); it can contains ? or :XXX
* dataSourceId &#8211; num value; it can be null and used to specify a different db to
* use with the sql statement
* separatedTransaction &#8211; boolean value; if true, the SQL instruction is executed on a separated transaction which is immediately committed (as for a REQUIRE_NEW EJB directive)
* interruptExecution &#8211; boolean value; if true, an erroneous SQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; array value: can be []; it represents values which replace ? symbols in sql
* Example:

var returnedValue = utils.executeStoredFunction(&#8220;usercheck1(?, ?)&#8221;,&#8230;.

Progressive
## Syntax

```js
var value = utils.getProgressive(String tableName, String columnName,Boolean separatedTransaction, Boolean interruptExecution)
```

## Details

* tableName &#8211; String: name of table for calculating progressive
* columnName &#8211; String: column name of field to calculating progressive
* separatedTransaction &#8211; boolean value; if true, the SQL instruction is executed on a separated transaction which is immediately committed (as for a REQUIRE_NEW EJB directive)
* interruptExecution &#8211; boolean value; if true, an erroneous SQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue


Counter
## Syntax

```js
var value = utils.getCount(String tableName, String valueColumnName, String incrementValue, String where, Boolean separatedTransaction, Boolean interruptExecution, Long dataSourceId)
```

## Details

* value &#8211; Long: new value of counter
* tableName &#8211; String: name of table for calculating counter
* valueColumnName &#8211; String: column name of field to calculating counter
* incrementValue &#8211; String: increment value for counter
* where &#8211; String: where condition for query
* separatedTransaction &#8211; boolean value; if true, the SQL instruction is executed on a separated transaction which is immediately committed (as for a REQUIRE_NEW EJB directive)
* interruptExecution &#8211; boolean value; if true, an erroneous SQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* dataSourceId &#8211; additional data source to use when executing this SQL statement; if set to null, the default database connection will be used


 **Date functions** 
Remove time from date
## Syntax

```js
var newDate = utils.removeTime(java.util.Date date)
```

## Details

* date &#8211; java.util.Date: date without time


Adds or subtracts the specified amount of time to the given calendar field, based on the calendar&#8217;s rules. You can use
 **utils.addDate(Long currentTimeMillis, String field, int amount)** 
 **utils.addDate(String field, int amount)** : use a current date;
 **utils.addDate(String date, String format, String field, int amount)** : convert the date with the specify format (default: &#8220;yyyy-MM-dd&#8217;T&#8217;HH:mm:ss&#8221;)
## Details

* field &#8211; String: the calendar field

## Example

* amount &#8211; number: the amount of date or time to be added to the field


(Since version 5.0.1) Convert the date expressed as a String to a Date. The string must have the specified format (default: &#8220;yyyy-MM-dd&#8217;T&#8217;HH:mm:ss&#8221;)
## Syntax

```js
date = utils.convertStringToDate(dateAsString, String format)


```

Detail:

* dateAsString  date expressed as a string
* format &#8211; String: date format for string


Convert the date to String with the specify format (default: &#8220;yyyy-MM-dd&#8217;T&#8217;HH:mm:ss&#8221;)
## Syntax

```js
stringDate = utils.convertDateToString(java.util.Date date, String format)


```

Detail:

* date &#8211; java.util.Date: date to convert in string
* format &#8211; String: date format for string


Convert the date js object to a java.sql.Date, helpful in case you want to use it with a utils.executeSql or utils.executeQuery methods and pass it as a parameter (for a DATE typefield).
## Syntax

```js
var javasqlDateValue = utils.convertDateToSqlDate(java.util.Date date)


```

Detail:

* date &#8211; java.util.Date: date to convert in string



Convert the date js object to a java.sql.Date, helpful in case you want to use it with a utils.executeSql or utils.executeQuery methods and pass it as a parameter (for a DATETIME/TIMESTAMP typefield).
## Syntax

```js
var javasqlTimestampValue= utils.convertDateToTimestamp(java.util.Date date)


```

Detail:

* date &#8211; java.util.Date: date to convert in string



Send an alert message to a user
## Syntax

```js
utils.sendAlertMessage(from, message, destinations, priority, conversationId, messageTag)
```

## Details

* from &#8211; username to use to send the message; can be null, if not specified, it will be automatically filled with the current logged user
* message &#8211; message to send
* destinations &#8211; list of usernames who will receive the alert; they must be separated by a comma (,)
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.

Send an email message to a user
## Syntax

```js
utils.sendAlertEmailWithConversation(from, subject, message, destinations, priority, isHtmlContent, returnReceipt, conversationId, messageTag, filesToAttach)
```

## Details

* from &#8211; username to use to send the message; can be null, if not specified, it will be automatically filled with the current logged user, whose email address must be defined in the user detail form
* subject &#8211; email title
* message &#8211; message to send; it can be expressed in HTML format
* destinations &#8211; list of usernames who will receive the alert; they must be separated by a comma (,); for each username specified, its email address must be defined in the user detail form
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD


Send an email message to a user
## Syntax

```js
utils.sendAlertEmailWithEmailAddressesWithConversation(from, subject, message, destinations, priority, isHtmlContent, returnReceipt, conversationId, messageTag, dirId, fileName, filesToAttach)
```

## Details

* from &#8211; email address to use to send the message; can be null, if not specified, it will be automatically filled with the email address of the current logged user (defined in the user detail form)
* subject &#8211; email title
* message &#8211; message to send; it can be expressed in HTML format
* destinations &#8211; list of email addresses who will receive the alert; they must be separated by a comma (,)
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD


Send an email message to a user
## Syntax

```js
utils.sendAlertEmailFromTemplate(String from,Number templateId,String destinations, String carbonCopy, String blindCarbonCopy, String priority,boolean isHtmlContent,Map jsObj,Long dirId,String fileName, String... filesToAttach)
```

## Details

* from &#8211; username to use to send the message; can be null, if not specified, it will be automatically filled with the current logged user, whose email address must be defined in the user detail form; it can be overridden by the template "from" field
* templateId &#8211; id of the template previously defined, used to set subject and body; optionally, the template can be optionally used to set from, to, cc, receipt flag too
* destinations &#8211; list of usernames who will receive the alert; they must be separated by a comma (,); for each username specified, its email address must be defined in the user detail form; it can be overridden by the template "to" field
*  **carbonCopy**  &#8211; optional argument used to specify a separated list (by comma) of email addresses which will receive the email message in carbon copy
*  **blindCarbonCopy**  &#8211; optional argument used to specify a separated list (by comma) of email addresses which will receive the email message in blind carbon copy
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
*  **isHtmlContent**  &#8211; flag used to specify if the message text is formatted in HTML or plain text
* jsObj &#8211; javascript record which substitute the variables in the template previously defined
* dirId&#8211; optional dir id used to save the message also to the server file system
* fileName&#8211; optional file name required in case the dir id has been specified; the message will be save in eml format on the file system
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD



Send an email message to a user
## Syntax

```js
utils.sendAlertEmailFromTemplateWithEmailAddresses(String from, Number templateId, String destinations, String priority, boolean isHtmlContent, NativeObject jsObj,  dirId, fileName, filesToAttach)
```


## Details

* from &#8211; username to use to send the message; can be null, if not specified, it will be automatically filled with the current logged user, whose email address must be defined in the user detail form; it can be overridden by the template "from" field
* templateId &#8211; id of the template previously defined, used to set subject and body; optionally, the template can be optionally used to set from, to, cc, receipt flag too
* destinations &#8211; list of usernames who will receive the alert; they must be separated by a comma (,); for each username specified, its email address must be defined in the user detail form; it can be overridden by the template "to" field
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
* jsObj &#8211; javascript record which substitute the variables in the template previously defined
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD



Send an email message to a user
## Syntax

```js
utils.sendAlertEmailFromTemplateWithEmailAddressesWithSMTPSettings(String from, Number templateId, String destinations, String priority, boolean isHtmlContent, NativeObject jsObj, String smtpHost,String smtpPort,String protocol,String smtpUsername,String smtpPassword,String useTLS, dirId, fileName, filesToAttach)
```


## Details

* from &#8211; username to use to send the message; can be null, if not specified, it will be automatically filled with the current logged user, whose email address must be defined in the user detail form; it can be overridden by the template "from" field
* templateId &#8211; id of the template previously defined, used to set subject and body; optionally, the template can be optionally used to set from, to, cc, receipt flag too
* destinations &#8211; list of usernames who will receive the alert; they must be separated by a comma (,); for each username specified, its email address must be defined in the user detail form; it can be overridden by the template "to" field
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
* jsObj &#8211; javascript record which substitute the variables in the template previously defined
* smtpXXX&#8211;SMTP settings, required to connect to an SMTP server
* dirId&#8211; optional dir id used to save the message also to the server file system
* fileName&#8211; optional file name required in case the dir id has been specified; the message will be save in eml format on the file system
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD



Send an email message to a user
## Syntax

```js
utils.sendAlertEmailFromTemplateWithConversation(String from, Number templateId, String destinations, String priority, boolean isHtmlContent, NativeObject jsObj, conversationId, messageTag, dirId, fileName, filesToAttach)
```

## Details

* from &#8211; username to use to send the message; can be null, if not specified, it will be automatically filled with the current logged user, whose email address must be defined in the user detail form; it can be overridden by the template "from" field
* templateId &#8211; id of the template previously defined, used to set subject and body; optionally, the template can be optionally used to set from, to, cc, receipt flag too
* destinations &#8211; list of usernames who will receive the alert; they must be separated by a comma (,); for each username specified, its email address must be defined in the user detail form; it can be overridden by the template "to" field
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
* jsObj &#8211; javascript record which substitute the variables in the template previously defined
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD



Send an email message to a user
## Syntax

```js
utils.sendAlertEmailFromTemplateWithEmailAddressesWithConversationAndSMTPSettings(String from, Number templateId, String destinations, String priority, boolean isHtmlContent, NativeObject jsObj, conversationId, messageTag, String smtpHost,String smtpPort,String protocol,String smtpUsername,String smtpPassword,String useTLS, dirId, fileName, filesToAttach)
```


## Details

* from &#8211; email address to use to send the message; can be null, if not specified, it will be automatically filled with the email address of the current logged user (defined in the user detail form); it can be overridden by the template "from" field
* templateId &#8211; id of the template previously defined, used to set subject and body; optionally, the template can be optionally used to set from, to, cc, receipt flag too
* destinations &#8211; list of email addresses who will receive the alert; they must be separated by a comma (,); it can be overridden by the template "to" field
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high).
*  **isHtmlContent**  &#8211; flag used to specify if the message text is formatted in HTML or plain text
* jsObj &#8211; javascript record which substitute the variables in the template previously defined
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history
*  **smtpXXX**  &#8211; parameters needed to connect to an SMTP server
* dirId&#8211; optional dir id used to save the message also to the server file system
* fileName&#8211; optional file name required in case the dir id has been specified; the message will be save in eml format on the file system
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD


Send an email message to a user
## Syntax

```js
utils.sendAlertEmailFromTemplateWithEmailAddressesWithConversation(String from, Number templateId, String destinations, String priority, boolean isHtmlContent, NativeObject jsObj, conversationId, messageTag, dirId, fileName, filesToAttach)
```

## Details

* from &#8211; email address to use to send the message; can be null, if not specified, it will be automatically filled with the email address of the current logged user (defined in the user detail form); it can be overridden by the template "from" field
* templateId &#8211; id of the template previously defined, used to set subject and body; optionally, the template can be optionally used to set from, to, cc, receipt flag too
* destinations &#8211; list of email addresses who will receive the alert; they must be separated by a comma (,); it can be overridden by the template "to" field
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high).
* jsObj &#8211; javascript record which substitute the variables in the template previously defined
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history
* dirId&#8211; optional dir id used to save the message also to the server file system
* fileName&#8211; optional file name required in case the dir id has been specified; the message will be save in eml format on the file system
* filesToAttach &#8211; list of files, expressed with an absolute path.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" to "Y", otherwise these messages cannot be showed on the client side.
 **Note** : in order to send email, additional application/common parameters must be defined:

* MAIL_SMTP_HOST
* MAIL_SMTP_PORT

These are optional:

* MAIL_SMTP_PROTOCOL
* MAIL_SMTP_USE_TLS
* MAIL_SMTP_USERNAME
* MAIL_SMTP_PASSWORD



Send a chat message to a user
## Syntax

```js
utils.sendChatMessage(from, message, destinations, priority, conversationId, messageTag)
```

## Details

* from &#8211; username to use to send the message; can be null, if not specified, it will be automatically filled with the current logged user
* message &#8211; message to send
* destinations &#8211; list of usernames who will receive the alert; they must be separated by a comma (,)
* priority &#8211; priority to use for the messages to show to a specific user: messages having a higher priority will be showed at the top of the list; it can be null; if not specified, it will be set to "normal"; allowed values: 0 (minor), 1, (normal), 2 (high)
* conversationId &#8211; conversation id used to identify a chain of messages; optional: if not specified, each message represents the first and last message in the convo
* messageTag &#8211; optional hidden text to add to the message and used to search for specific messages stored in the message history.

Note: in order to use this feature, you have first to define an application parameters named "SHOW_ALERT_MENU_ITEM" or "SHOW_CHAT_POPUP_MESSAGE" to "Y", otherwise these messages cannot be showed on the client side.


Execute a command on the shell. Optionally, a list of arguments can be passed to the command.
It returns the exit code produced by the command execution
## Syntax

```js
var exitCode = utils.executeShellCommand(command, arg1, arg2, ...)
```

## Details

* command &#8211; command to execute; it must include the absolute path to the command and must end with a .sh or .bat with no spaces within
* arguments &#8211; zero or more String type arguments; [] otherwise



Parse a simple XML document and generate a Javascript &#8220;compatible&#8221; representation, expressed using lists and js objects, where each js object has special attributes named: &#8220;tagName&#8221;, &#8220;tagValue&#8221; and &#8220;subTags&#8221;.
The document (list of tags) is expressed as a list of js objects, where each js object can have a list of subtags and attributes, expressed object&#8217;s attributes. The js object always contains special entries named &#8220;tagName&#8221;, &#8220;subTags&#8221; and optionally &#8220;tagValue&#8221; if there is tag value.
## Syntax

```js
var jsObjectsList = utils.parseXML(xmlDocument);
```

## Details

* xmlDocument &#8211; an XML document as a String

Returns an XML representation, expressed as a list of Javascript objects, where each of them has three special attributes: "tagName", "tagValue" and "subTags". You can then navigate through this js object and extract any data.
## Example

JohnDoe&#8230;
JaneRoe&#8230;


Search for the specified path within the XML document parse result (i.e. after invoking parseXML method).
## Syntax

```js
var jsObjectsList = utils.findTagsByPath(xmlDocNodes, path);
```

## Details

* xmlDocNodes &#8211; XML document parsed through parseXML method
* path &#8211; a tags path, expressed as tag1/tag2/tag3&#8230;
* Return all occurrences matching the specified path.

## Example
JohnDoe&#8230;
JaneRoe&#8230;

var xml = utils.getWebContent(&#8220;http://&#8230;&#8221;,false,&#8221;GET&#8221;, null,null,null,null);
var xmlDocNodes = utils.parseXML(xml); // list of companies
var staffList = utils.findTagsByPath(xmlDocNodes, &#8220;company/staff&#8221;);


Scroll all input nodes and for each create a js object whose attributes are the subtags having the specified tagNames (i.e. after invoking parseXML and findTagNames methods).
For each selected node, a new js object will be created and it will have as many attributes as the ones specified through tagNames argument, whose values will be retrieved by as sub tags values.
## Syntax

```js
var jsObjects = utils.findTagsByNames(selectedNodes, tagNames);
```

## Details

* selectedNodes &#8211; nodes to analyze
* tagNames &#8211; list of tag names to compare with each subtag of each selected node.

## Example
JohnDoe&#8230;
JaneRoe&#8230;

var xml = utils.getWebContent(&#8220;http://&#8230;&#8221;,false,&#8221;GET&#8221;, null,null,null,null);
var xmlDocNodes = utils.parseXML(xml); // list of companies
var staffList = utils.findTagsByPath(xmlDocNodes, &#8220;company/staff&#8221;);
var jsObjects = utils.findTagsByNames(staffList,[&#8220;firstname&#8221;,&#8221;lastname&#8221;]);

will return a list of js objects having this structure:
[{ "firstname": &#8220;John&#8221;, "lastname": &#8230; }, { "firstname": "Jane", &#8230;}]

Convert a javascript object to its JSON representation
## Syntax

```js
var json = utils.getJSONString(obj);
```

## Details

* obj &#8211; javascript object to convert to its JSON representation


Convert a list of javascript objects into its JSON representation: [&#8230;]
## Syntax

```js
var json = utils.getJSONList(jsObjectsList);
```

## Details

* jsObjectsList &#8211; list of javascript objects to convert to JSON format
* Returns a JSON representation of a list of objects.

Note: this result is NOT compatible with an Ext.grid.GridPanel data protocol: see getListResponse instead.

Convert a list of javascript objects into its JSON representation: [&#8230;] and embed it to a &#8220;Ext.grid.GridPanel like&#8221; data representation, based on &#8220;valueObjectList&#8221;, &#8220;resultSetLength&#8221; and &#8220;moreRows&#8221; attributes.
## Syntax

```js
var json = utils.getListResponse(jsObjectsList, resultSetLength, moreRows);
```

## Details

* jsObjectsList &#8211; list of javascript objects to convert to JSON format
* resultSetLength &#8211; a number: list of objects (can be list.length)
* moreRows &#8211; flag used to specify
* Returns a JSON content compatible with Ext grids.


Replace all occurrences of the "specified" pattern within &#8220;text&#8221; with the new value.
## Syntax

```js
var newtext = utils.replaceAll(text, pattern, newValue)
```

## Details

* text &#8211; text to analyze
* pattern &#8211; pattern to search for
* newValue &#8211; value that replaces all occurrences of the pattern

Returns a new text where all occurrences of &#8220;pattern&#8221; have been replaced with &#8220;newValue&#8221;.

Execute an HTTP(s) connection and fetch the result, expressed as a String (e.g. a JSON or XML result content).
## Syntax

```js
var json = utils.getWebContent(uri, replaceVariables, httpMethod, contentType, requestBody, user, pwd);
```

## Details

* uri &#8211; URI, expressed as http:// or https:// with or without variables, expressed as :XXX
* replaceVariables &#8211; flag used to replace variables within the uri (variables are expressed as :XXX)
* httpMethod (optional: can be null); if specified, it defines the HTTP method: GET, POST
* contentType (optional: can be null); if specified, it defines the content type request (e.g. application/json)
* requestBody (optional: can be null); if specified, it defines the request body, expressed as a String (e.g. a JSON or XML content)
* user (optional: can be null); if specified, it defines the username for a BASIC authentication
* pwd (optional: can be null); if specified, it defines the password for a BASIC authentication
* Returns the HTTP response, expressed as a String (e.g. a JSON or XML result).

HTTP response codes included between 200 and 399 are managed as correct answers and the response is sent back throughthe &#8220;json&#8221; return variable.
In case of HTTP response codes above or equal to 400, an exception is fired and the exception content would contain the message sent back by the invoked web service; consequently, it would be better to surround this instruction between try-catch.
## Example

```js
try {

 var json = utils.getWebContentWithHeaders(...);

 ...

}

catch(e) {

 // e.message would containthe error message

}
```




Execute an HTTP(s) connection and fetch the result, expressed as a String (e.g. a JSON or XML result content).
## Syntax

```js
var json = utils.getWebContentWithHeaders(uri, replaceVariables, httpMethod, contentType, requestBody, user, pwd, charSet,  headers);
```

## Details

* uri &#8211; URI, expressed as http:// or https:// with or without variables, expressed as :XXX
* replaceVariables &#8211; flag used to replace variables within the uri (variables are expressed as :XXX)
* httpMethod (optional: can be null); if specified, it defines the HTTP method: GET, POST
* contentType (optional: can be null); if specified, it defines the content type request (e.g. application/json)
* requestBody (optional: can be null); if specified, it defines the request body, expressed as a String (e.g. a JSON or XML content)
* user (optional: can be null); if specified, it defines the username for a BASIC authentication
* pwd (optional: can be null); if specified, it defines the password for a BASIC authentication
*  **charSet**  (optional: can be null); if specified, it defines the char set to use for the request body (req property &#8220;Accept-Charset&#8221;); if not specified, it is autodefined as &#8220;UTF-8&#8221;
*  **headers** (optional: can be null); if specified, it defines a collection of attribute-values to pass as request headers; it is expressed as a javascript object: { attr1: value2, attr2: value2, &#8230; }
* Returns the HTTP response, expressed as a String (e.g. a JSON or XML result).


HTTP response codes included between 200 and 399 are managed as correct answers and the response is sent back throughthe &#8220;json&#8221; return variable.
In case of HTTP response codes above or equal to 400, an exception is fired and the exception content would contain the message sent back by the invoked web service; consequently, it would be better to surround this instruction between try-catch.
## Example


```js
try {

 var json = utils.getWebContentWithHeaders(...);

 ...

}

catch(e) {

 // e.message would containthe error message

}
```



Execute an HTTP(s) connection and fetch the result, expressed as a binary content and store it into the specified file.
## Syntax

```js
utils.getBinaryContent(toFile, uri, replaceVariables, httpMethod, contentType, requestBody, user, pwd);
```


* Details:
* toFile &#8211; absolute path including the file name, related to the local binary file to create and fill in with the result of this HTTP request
* uri &#8211; URI, expressed as http:// or https:// with or without variables, expressed as :XXX
* replaceVariables &#8211; flag used to replace variables within the uri (variables are expressed as :XXX)
* httpMethod (optional: can be null); if specified, it defines the HTTP method: GET, POST
* contentType (optional: can be null); if specified, it defines the content type request (e.g. application/json)
* requestBody (optional: can be null); if specified, it defines the request body, expressed as a String (e.g. a JSON or XML content)
* user (optional: can be null); if specified, it defines the username for a BASIC authentication
* pwd (optional: can be null); if specified, it defines the password for a BASIC authentication

Fetches the HTTP response, expressed as a binary content and stores in to the specified file.

Add an attribute (e.g. &#8220;member of&#8221;) to the entry identified by &#8220;filterDN&#8221;.
## Syntax

```js
var num = utils.addAttribute(host, port, filterDN, ldapUsername, ldapPassword, attributeNameToAdd, attributeValueToAdd);
```

## Details

* host &#8211; LDAP host
* port &#8211; LDAP port (optional: if not specified, 389 will be used)
* filterDN &#8211; base DN to apply as a filter
* ldapUsername &#8211; username to use to authenticate to the LDAP server
* ldapPassword &#8211; password to use to authenticate to the LDAP server
* attributeNameToAdd &#8211; attribute name to add to every entry matching the search criteria
* attributeValueToAdd &#8211; attribute value to add to every entry matching the search criteria
* Returns the number of entries found and updated.


Remove an attribute (e.g. &#8220;memberOf&#8221;) from the entry identified by &#8220;filterDN&#8221;.
## Syntax

```js
var num = utils.removeAttribute(host, port, filterDN, ldapUsername, ldapPassword, attributeNameToRemove, attributeValueToRemove);
```

## Details

* host &#8211; LDAP host
* port &#8211; LDAP port (optional: if not specified, 389 will be used)
* filterDN &#8211; base DN to apply as a filter
* ldapUsername &#8211; username to use to authenticate to the LDAP server
* ldapPassword &#8211; password to use to authenticate to the LDAP server
* attributeNameToRemove &#8211; attribute name to remove from every entry matching the search criteria
* attributeNameToRemove &#8211; attribute name to remove from every entry matching the search criteria
* Returns number of entries found and updated.



Get a list of records read from the LDAP server, where each record is expressed as a Javascript Object.
## Syntax

```js
var listOfObjects = utils.getEntriesList(host, port, baseDN, ldapUsername, ldapPassword, searchAttributes,attributesListToRead);
```

## Details

* host &#8211; LDAP host
* port &#8211; LDAP port (optional: if not specified, 389 will be used)
* baseDN &#8211; base DN to apply as a filter
* ldapUsername &#8211; username to use to authenticate to the LDAP server
* ldapPassword &#8211; password to use to authenticate to the LDAP server
* searchAttributes &#8211; attributes to apply as a filter
* attributesListToRead &#8211; list of attribute names to take into account when reading records from the LDAP server: these will be the only ones to use when creating the JSON result
* Returns a list of records read from the LDAP server, where each record is expressed as a Javascript object.


Get a list of Strings, related to multiple attribute values, starting from a specified attribute name of a specific entry read from the LDAP server.
## Syntax

```js
var listOfStrings = utils.getMultipleValuesList(host, port, baseDN, ldapUsername, ldapPassword, searchAttributes, attributeName);
```

## Details

* host &#8211; LDAP host
* port &#8211; LDAP port (optional: if not specified, 389 will be used)
* baseDN &#8211; base DN to apply as a filter
* ldapUsername &#8211; username to use to authenticate to the LDAP server
* ldapPassword &#8211; password to use to authenticate to the LDAP server
* searchAttributes &#8211; attributes to apply as a filter, in order to identity a single entry into the LDAP server
* attributeName &#8211; attribute name to read: each matching found will generate a row in the results list


Send a list of files stored in the server side file system to an FTP server, inside the specified remote folder.
## Syntax

```js
var ok = utils.sendFiles(host, port, useSSL, username, password, toDir, filePaths);
```

## Details

* host &#8211; FTP server host
* port &#8211; FTP server port (e.g. 21)
* useSSL &#8211; boolean flag, used to specify if FTPS must be used
* username &#8211; username to use to authenticate to the FTP server
* password &#8211; password to use to authenticate to the FTP server
* toDir &#8211; remote folder, within the FTP server, where files must be copied
* filePaths &#8211; list of files stored in the server side file system (expressed with absolute path) to copy within the FTP server


Send a single file to the FTP server and store it in the specified folder with the specified name.
## Syntax

```js
var ok = utils.sendFile(host, port, useSSL, username, password, destFile, sourceFile);
```

## Details

* host &#8211; FTP server host
* port &#8211; FTP server port (e.g. 21)
* useSSL &#8211; boolean flag, used to specify if FTPS must be used
* username &#8211; username to use to authenticate to the FTP server
* password &#8211; password to use to authenticate to the FTP server
* destFile &#8211; folder in the FTP server + destination file name where storing the file
* sourceFile &#8211; sourceFile absolute path in the server file system + file name, related to the file to read



read a remote file, stored within the FTP server and copy it into the specified absolute file, related to the server.
## Syntax

```js
var ok = getFile(host, port, useSSL, username, password, ftpDir, ftpFileName, localFile);
```

## Details

* host &#8211; FTP server host
* port &#8211; FTP server port (e.g. 21)
* useSSL &#8211; boolean flag, used to specify if FTPS must be used
* username &#8211; username to use to authenticate to the FTP server
* password &#8211; password to use to authenticate to the FTP server
* ftpDir &#8211; remote folder, within the FTP server, where the file to retrieve is currently stored
* ftpFileName &#8211; file name to retrieve, stored within the specified remote folder
* localFile &#8211; path+file name, where the remote file must be copied, in the server file system


read a list of remote file names, all stored in the same remote folder within the FTP server; file names are filtered according to the specified filter condition.
## Syntax

```js
var listOfFileNames = getFiles(host, port, useSSL, username, password, remoteDir, fileFilter);
```

## Details

* host &#8211; FTP server host
* port &#8211; FTP server port (e.g. 21)
* useSSL &#8211; boolean flag, used to specify if FTPS must be used
* username &#8211; username to use to authenticate to the FTP server
* password &#8211; password to use to authenticate to the FTP server
* remoteDir &#8211; remote folder, within the FTP server, where files are stored
* fileFilter &#8211; (optional) parameter to use to filter files to read (e.g. *.jpg)
* listOfFileNames &#8211; list of file names (String objects) which satisfy the filter condition.


create an URL which can be invoked later from another client (e.g. from an email message as a link) and which will be accepted by Platform, since it contains an authentication token; this URL can be used to invoke a server-side javascript action identified by the specific action id. The URL will show the approve.jsp web page containing the Accept/Reject buttons used to confirm or deny an action invoked when pressing the related button.
## Syntax

```js
var url = createAllowedUrl(baseUrl, actionId, aName, aValue, rName, rValue, params, expirationDays, maxTimes, message);
```

## Details

* baseUrl &#8211; base URL to pass, related to the host name and web context; it will represent the first part of the final URL (e.g. http://host:port/platform/)
* actionId &#8211; action identifier to execute when pressing the Accept/Reject button on the web page opened when clicking of the returning URL
* aName &#8211; parameter name related to the accept event, i.e. parameter passed to the js action when pressing the Accept button
* aValue &#8211; parameter value related to the accept event, i.e. parameter value passed to the js action when pressing the Accept button
* rName &#8211; parameter name related to the reject event, i.e. parameter passed to the js action when pressing the Reject button
* rValue &#8211; parameter name related to the accept event, i.e. parameter value passed to the js action when pressing the Reject button
* params &#8211; additional parameters to pass to the js action, for instance to identify a specific record to work with
* expirationDays &#8211; optional parameter (can be set to 0); if set, it represents the maximum number of days the URL is valid, starting from the URL creation date
* maxTimes &#8211; it represents the maximum number of times the URL can be used before it expires
* message &#8211; text to show on the approve.jsp web page, just above the Accept/Reject buttons.



Execute an Alfresco web script, starting with &#8220;service/xyz?&#8230;&#8221; and fetch the result, expresses as a String (e.g. a JSON or XML result content).
## Syntax

```js
var responseBody = utils.getAlfrescoWebScript(uri, replaceVariables, httpMethod, bodyRequest, charSet);
```

## Details

* uri &#8211; last part of the URI to pass to the Alfresco base URL, in order to invoke a webscript, i.e. from the webscript name to required parameters
* replaceVariables &#8211; flag used to define if :XXX value in the uri must be replaced by Platform defined variables
* httpMethod &#8211; optional: HTTP method to use: GET, POST, etc.
* bodyRequest &#8211; optional: body request to pass, expressed as a String
* charSet &#8211; optional: the request/response charset to use; if not specified, Unicode charset will be used (UTF-8); possible values: UTF-8, Windows-1252


Extract a file from Alfresco and save it to the specified local file path.
## Syntax

```js
var success = utils.getAlfrescoDocument(id, fileName, destPath);
```

## Details

* id &#8211; UUID value which identifies the file to retrieve from Alfresco CMS
* fileName &#8211; file name related to the specified if
* destPath &#8211; absolute path related to the A.S. file system, where the file will be saved, once extracted from Alfresco CMS


Get the current date; helpful when executing a SQL query and a bind variable should be filled out by a dynamic value which is the current date.
## Syntax

```js
var currentDate = utils.getCurrentDate();
```


Encrypt a password.
## Syntax

```js
var encryptedPassword = utils.encodePassword(password);
```



Get the whole conversation (list of messages), starting from the conversation id.
## Syntax

```js
var logMessages = utils.getConversation(conversationId);
```

## Details

* conversationId &#8211; conversation id which identifies a chain of messages


Get the whole conversation (list of messages), starting from a tag included at some point in the conversation.
## Syntax

```js
var logMessages = utils.getConversationFromTag(messageTag);
```

## Details

* messageTag &#8211; tag stored along with the messages and used to fetch the whole conversation, inclusing that messge too


Read the specified file from the source directory and extract signed data and the embedded document.
The embedded document is then saved in the destination directory
## Syntax

```js
var obj = utils.getCertMessage(srcDirectoryId, destDirectoryId, fileName);
```

## Details

* srcDirectoryId &#8211; id used to identify a source folder in the server file system where the file to read has been stored
* destDirectoryId &#8211; id used to identify a folder in the server file system when the extracted document will be saved
* fileName &#8211; file name inside the specified folder
* obj &#8211; embedded document, expressed as a javascript object having the following attributes:



Read the specified file and extract signed data and the embedded document.
The embedded document is then saved in the destination directory
## Syntax

```js
var obj = utils.getCertMessage(srcFileName, destFolder);
```

## Details

* srcFileName &#8211; path + file name to analyze
* destFolder &#8211; destination folder; if not specified, the srcFolder will be used
* obj &#8211; embedded document, expressed as a javascript object having the following attributes:



Create a zip file containing the list of passed files.
## Syntax

```js
var ok = utils.zipFiles(baseDir,files,zipFile,deleteFilesAfterZip);
```

## Details

* baseDir &#8211; base dir used to calculate the entry in the zip (i.e. &#8220;C:/xxx/yyy/&#8221;)
* files &#8211; files to zip (each including an absolute path, &#8220;C:/xxx/yyy/fileName.csv&#8221;)
* zipFile &#8211; zip file to create, including the absolute path (i.e. &#8220;C:/aaa/bbb/zipFileName.zip&#8221;)
* deleteFilesAfterZip &#8211; flag used to decide if input files must be deleted after the zip creation


Create a new company id, starting from the one specified as argument.
## Syntax

```js
var ok = utils.copyCompanyId(startingCompanyId, newCompanyId);
```

## Details

* startingCompanyId &#8211; company id to use when creating a new one, in order to duplicate its content
* newCompanyId &#8211; new company id value


Set the value for the specified attribute name, related to the input object.
## Syntax

```js
setAttributeValue(attributeName, value);
```

## Details
attributeName &#8211; attribute name contained in the input object
value &#8211; value to set

Read a list of messages from the email server.
## Syntax

```js
var emailMessages = utils.getEmails(server, port, username, password, protocol, useTLS, maxMessagesToRead, notReadFilter, startDateFilter, fromAddressFilter, subjectFilter, bodyFilter, withAttachments, attachmentsPath, folderName, moveToFolderOnceRead, setAsSeen, deleteEmailWhenRead, debug);
```

## Details

* server -server host
* port &#8211; server port (e.g. 995)
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server (e.g. imap, imaps, pop, pops)
* useTLS  flag used to enabled the TLS mode
* maxMessagesToRead &#8211; maximum number of messages to read
* notReadFilter &#8211;  flag used to filter only messages not read yet
* startSendDateFilter &#8211; optional parameter; if not null, messages to read will be filtered by sendingdate: only the ones next or equal to this date wil be returned
* fromAddressFilter &#8211; optional parameter; if not null, messages to read will be filtered by the &#8220;from address&#8221; specified
* subjectFilter &#8211; optional parameter; if not null, messages to read will be filtered and only the ones containing this value in their object will be returned
* bodyFilter &#8211; optional parameter; if not null, messages to read will be filtered and only the ones containing this value in their body content will be returned
* withAttachments &#8211; optional parameter; if not null, messages to read will be filtered and only the ones having at least one attachment will be returned
* attachmentsPath &#8211; absolute path where saving attachments
* folderName &#8211; folder to read; e.g. INBOX; if not specified, it will be set to INBOX
* moveToFolderOnceRead &#8211; move to the specified folder each message, once read; can be null
* setAsSeen &#8211; flag used to mark as &#8220;SEEN&#8221; a message just read
* deleteEmailWhenRead  &#8211; flag used to delete the email message once read
* debug &#8211; flag used to debug the communication with the server
* emailMessages &#8211; list of messages read from the mail box

Attributes contained in each message of the list:

* id &#8211; email identified, used to delete an email message later
* from &#8211; from email address
* to &#8211; to email address
* message &#8211; email body
* subject &#8211; email subject
* mimeType &#8211; e.g. &#8220;text/plain&#8221; or &#8220;text/html&#8221;
* list &#8211; list of absolute paths (strings) where the attachments have been saved
* sendDate -message sending date (since 5.0.1 version)
* receiveDate &#8211; message receiving date (since 5.0.1 version)
* replyTo &#8211; reply to addresses, separated by a comma (since 5.0.0 version)

Full list of attributes (as of September 2016)
to, returnReceipt, getPlainMessage, subject, getBcc, getTo, hashCode, from, setReturnReceipt, wait, getCc, getAttachments, setTo, id, notify, getFrom, attachments, mimeType, setId, notifyAll, getId, getClass, clone, setMessage, setHtmlMessage, getMessage, equals, plainMessage, setAttachments, bcc, getSubject, class, setFrom, getReturnReceipt, message, getPk, setMimeType, setBcc, setCc, toString, htmlMessage, cc, setPlainMessage, pk, getHtmlMessage, getMimeType, setSubject

Read a list of messages from the email server, with additional filtering conditions.
## Syntax

```js
var emailMessages = utils.getEmails(server, port, username, password, protocol, useTLS, maxMessagesToRead, notReadFilter, startSendDateFilter, endSendDateFilter, startReceiveDateFilter, endReceiveDateFilter, fromAddressFilter, subjectFilter, bodyFilter, withAttachments, attachmentsPath, folderName, moveToFolderOnceRead, setAsSeen, deleteEmailWhenRead, debug);
```

## Details

* server -server host
* port &#8211; server port (e.g. 995)
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server (e.g. imap, imaps, pop, pops)
* useTLS flag used to enabled the TLS mode
* maxMessagesToRead &#8211; maximum number of messages to read
* notReadFilter &#8211; flag used to filter only messages not read yet
* startSendDateFilter &#8211; optional parameter; if not null, messages to read will be filtered by sendingdate: only the ones next or equal to this date wil be returned
* endSendDateFilter &#8211; optional parameter; if not null, messages to read will be filtered by sendingdate: only the ones previousor equal to this date wil be returned
* startReceiveDateFilter &#8211; optional parameter; if not null, messages to read will be filtered by receiving date: only the ones next or equal to this date wil be returned
* endReceiveDateFilter &#8211; optional parameter; if not null, messages to read will be filtered by receiving date: only the ones previousor equal to this date wil be returned
* fromAddressFilter &#8211; optional parameter; if not null, messages to read will be filtered by the &#8220;from address&#8221; specified
* subjectFilter &#8211; optional parameter; if not null, messages to read will be filtered and only the ones containing this value in their object will be returned


* bodyFilter &#8211; optional parameter; if not null, messages to read will be filtered and only the ones containing this value in their body content will be returned
* withAttachments &#8211; optional parameter; if not null, messages to read will be filtered and only the ones having at least one attachment will be returned
* attachmentsPath &#8211; absolute path where saving attachments
* folderName &#8211; folder to read; e.g. INBOX; if not specified, it will be set to INBOX
* moveToFolderOnceRead &#8211; move to the specified folder each message, once read; can be null
* setAsSeen &#8211; flag used to mark as &#8220;SEEN&#8221; a message just read
* deleteEmailWhenRead &#8211; flag used to delete the email message once read
* debug &#8211; flag used to debug the communication with the server
* emailMessages &#8211; list of messages read from the mail box

Attributes contained in each message of the list:

* id &#8211; email identifier, used to delete an email message later
* messageNumber &#8211;index within the folder of the specific message
* from &#8211; from email addresss
* message &#8211; email body
* subject &#8211; email subject
* mimeType &#8211; e.g. &#8220;text/plain&#8221; or &#8220;text/html&#8221;
* list &#8211; list of absolute paths (strings) where the attachments have been saved
* sendDate -message sending date
* receiveDate &#8211; message receiving date


Move a list of email messages to another folder.
## Syntax

```js
var ok = utils.moveMessages(server,port, username, password, protocol, useTLS, messageIds,folderName, moveToFolder, setAsSeen, debug);
```

## Details

* server -server host
* port &#8211; server port
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server
* useTLS  &#8211; flag used to enabled the TLS mode
* messageIds &#8211; list of email message identifiers, related to emails to move
* folderName &#8211; source folder (e.g. INBOX), where the email messages are
* stored
* moveToFolder &#8211; destination folder (e.g. Archivio)
* setAsSeen &#8211; flag used to mark the email as seen
* debug &#8211; flag used to debug the process


Mark a list of email messages as seen or not seen.
## Syntax

```js
var ok = utils.markMessagesAsSeen(server,port, username, password, protocol, useTLS, messageIds,folderName, setAsSeen, debug);
```

## Details

* server -server host
* port &#8211; server port
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server
* useTLS  &#8211; flag used to enabled the TLS mode
* messageIds &#8211; list of email message identifiers, related to emails to move
* folderName &#8211; source folder (e.g. INBOX), where the email messages arestored
* setAsSeen &#8211; flag used to mark the email as seen or not seen
* debug &#8211; flag used to debug the process


Deletea list of email messages from the specified folder, by moving them to the trash folder, starting from a list of messages identified both by a list of email ids and a list of corresponding email indexes.
Both properties can retrieved through the message js object returned by the utils.getEmails method.
## Syntax

```js
var ok = utils.deleteMessages(server,port, username, password, protocol, useTLS,messageIdsToDelete, messagesNumbersToDelete,folderName,trashName);
```

## Details

* server -server host
* port &#8211; server port
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server
* useTLS  &#8211; flag used to enabled the TLS mode
* messageIdsToDelete &#8211; list of email message identifiers to delete; this value can be fetched from the email message js object
* messageNumbersToDelete &#8211; list of email message numbersto delete; this value can be fetched from the email message js object
* folderName&#8211;folder name where themessages to delete are located (e.g. INBOX)
* trashName&#8211;identifier of the Trash folder; since this name changes according to the specific email provider, it is not necessarely the value &#8220;Trash&#8221;. If you don&#8217;t know it, you can try with &#8220;Trash&#8221; and in case of errors, Platform would log the whole list of folders supported by the email provider.


Deletea list of email messages from the specified folder, by moving them to the trash folder, starting from a filtering condition. At least one filtering condition is required (one of the four date filters).
## Syntax

```js
var ok = utils.deleteMessages(server,port, username, password, protocol, useTLS, startSendDateFilter, endSendDateFilter, startReceiveDateFilter, endReceiveDateFilter,  messagesNumbersToDelete, folderName, trashName);
```

## Details

* server -server host
* port &#8211; server port
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server
* useTLS  &#8211; flag used to enabled the TLS mode
* startSendDateFilter&#8211;optional filter: if specified, only messages sent after the specified date will be deleted
* endSendDateFilter &#8211; optional filter: if specified, only messages sent beforethe specified date will be deleted
* startReceiveDateFilter&#8211; optional filter: if specified, only messages receviedafter the specified date will be deleted
* endReceiveDateFilter&#8211; optional filter: if specified, only messages received beforethe specified date will be deleted
* trashName&#8211;identifier of the Trash folder; since this name changes according to the specific email provider, it is not necessarely the value &#8220;Trash&#8221;. If you don&#8217;t know it, you can try with &#8220;Trash&#8221; and in case of errors, Platform would log the whole list of folders supported by the email provider.
* folderName&#8211;folder name where themessages to delete are located (e.g. INBOX)



Forward an email to the specified destination.
## Syntax

```js
var ok = utils.forwardEmail(server,port, username, password, protocol, useTLS,to, subject subject, text, messageId);
```

## Details

* server -server host
* port &#8211; server port
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server
* useTLS  &#8211; flag used to enabled the TLS mode
* to &#8211; destination address
* subject &#8211; additional title to add to the original one
* text &#8211; additional text to add to the body of the email
* messageId &#8211; list of email message identifiers to delete


Save a list of email messages in eml format on the server file system (since 5.2).
Messages to save are identified by a list of message id, so utils.getEmails() method mustbe invoked first, in order to get the identifiers needed here to fetch the messages to save.
## Syntax

```js
var ok = utils.saveEml(String server,Integer port, String username, String password, String protocol,Boolean useTLS,String folderName,String[] messageIds,String[] fileNames,Long directoryId);
```

## Details

* server -server host
* port &#8211; server port
* username &#8211; username to use when accessing the email server
* password &#8211; password to use when accessing the email server
* protocol &#8211; protocol to use when connecting to the email server
* useTLS  &#8211; flag used to enabled the TLS mode
* folderName&#8211;folder identifier, where the messages are located; the folder name changes according to the mail server; an example is INBOX
* messageIds&#8211;a list of message identifiers to save, previously fetched through a getEmails() method invokation
* fileNames&#8211;file names to use when saving the messages; this list must have the same length of the message ids list, one for each id
* directoryId&#8211;directory identifier, used to identify the path on the server file system, when all messages will be saved

The method returns the list of messages ids not found in the specified folder and, consequently, not saved.


Copy the source file to the destination file. Since &#8220;destFile&#8221; contains a file name too, the source file can be renamed when copied.
## Syntax

```js
var ok = utils.copyFile(srcFile, destFile, replaceExistingFile, deleteSourceFile);
```

## Details

* srcFile &#8211; absolute path + file name
* destFile &#8211; absolute path + file name
* replaceExistingFile &#8211; flag used to replace the already existing destination file; if set to false and the destination file already exists, the copy process would be interrupted and the returned value would be false
* deleteSourceFile &#8211; flag used to delete the source file, once the file has been copied to the destination path


Add a server-side JS action as a process to a specific queue.
The invoked action will receive in the reqParams variable two entries:

* applicationId &#8211; current application identifier
* queueId &#8211; the identifier in the queues table of the current execution

## Syntax

```js
var ok = utils.enqueueAction(queueName, actionId, params, priority, processWaitTime, logExecution);
```

## Details

* queueName &#8211; optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue
* actionId &#8211; server-side js action identifier to execute
* param &#8211; js object containing parameters to pass to the action
* priority &#8211; optional; if specified, processes within the same queue will be sorted according to the priority rathe than to the enqueing time
* processWaitTime &#8211; optional; if specified, the process will not be started before that time, expressed in seconds
* logExecution &#8211; true to log in LOG60_LOGS the execution of the process


Add a web service invocation as a process to a specific queue.
## Syntax

```js
var ok = utils.enqueueWebService(queueName, url, params, priority, processWaitTime, logExecution);
```

## Details

* queueName &#8211; optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue
* url &#8211; shell command to execute
* param &#8211; js object containing parameters to pass to the web service
* priority &#8211; optional; if specified, processes within the same queue will be sorted according to the priority rathe than to the enqueing time
* processWaitTime &#8211; optional; if specified, the process will not be started before that time, expressed in seconds
* logExecution &#8211; true to log in LOG60_LOGS the execution of the process


Add shell command as a process to a specific queue.
## Syntax

```js
var ok = utils.enqueueShellCommand(queueName, cmd, priority, processWaitTime, logExecution);
```

## Details

* queueName &#8211; optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue
* cmd &#8211; shell command to execute
* priority &#8211; optional; if specified, processes within the same queue will be sorted according to the priority rathe than to the enqueing time
* processWaitTime &#8211; optional; if specified, the process will not be started before that time, expressed in seconds
* logExecution &#8211; true to log in LOG60_LOGS the execution of the process


Force the starting of the specified enqueued process.
## Syntax

```js
var ok = utils.forceStartProcess(String queueName, Long progressive)
```

## Details

* queueName &#8211; optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue
* progressive &#8211; id of the enqueued process
* result: false if the process has been already terminated or does not exist


Remove the specified process instance from the queue.
## Syntax

```js
var ok = utils.dequeueProcess(queueName, progressive)
```

## Details

* queueName &#8211; optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue
* progressive &#8211; id of the enqueued process
* result: if the process has been already terminated or does not exist


How to get the printers list. Printers must be connected to the server machine (as local printers or network printers); local printers directly connected to the user PC are ignored.
## Syntax

```js
var list = utils.getPrintServices();
```

## Details

* result: javascript Array of printer names (String values)

## Example

```js
var list = utils.getPrintServices();
var json = "[";

for(var i=0;i&lt;list.length;i++){
    json += '"'+list[i]+'",';
}

json = json.substring(0,json.length-1)+"]";
utils.setReturnValue(json);
```

## Example

```js
json = new SyncRequest().send(contextPath+"/executeJs?applicationId=...&amp;actionId=...", "GET", null);
var stampanti = eval("("+json+")");
var stampantiDS = [];

for(var i=0;i&lt;stampanti.length;i++)
  stampantiDS.push([stampanti[i],stampanti[i]]);

var comboStampanti = new Ext.form.ComboBox({
  typeAhead: true,
  mode: 'local',
  allowBlank: false,
  forceSelection: true,
  triggerAction: 'all',
  name: 'stampante',
  itemId: 'stampante',
  store: new Ext.data.ArrayStore({
    id: 0,
    fields: [
    'code',
    'description'
    ],
    data: stampantiDS
  }),
  valueField: 'code',
  displayField: 'description'
});
var w = new Ext.Window({
  title: "Stampa documento",
  width: 500,
  height:150,
  minWidth: 500,
  maximizable: false,
  minimizable: false,
  closable: false,
  modal: true,
  layout:'absolute',
  plain:true,
  bodyStyle:'padding:5px',
  buttonAlign:'center',
  items: [{
    x: 5,
    y: 10,
    xtype: 'label',
    text: 'Stampante'
  },{
    x: 100,
    y: 5,
    width: 350,
    xtype: 'panel',
    border: false,
    layout: 'fit',
    items: comboStampanti
  }
  ],
  bbar: [{
    text: 'Annulla',
    xtype: 'button',
    handler: function() {
      w.close();
    }
  },
  {
    text: 'Stampa',
    xtype: 'button',
    handler: function() {
      var json = Ext.encode(vo);
      var form = w.items.get(0);
      var url =
      contextPath+"/executeJs?applicationId=TESTFUNZIONI&amp;actionId=..."+
      "&amp;stampante="+getComponentByItemId("stampante",w).getValue();
      json = new SyncRequest().send(url, "POST", json);
      var obj = eval("("+json+")");
      if (!obj.success) {
        showMessageDialog("Creazione Ambiente Demo",obj.message,function(){},true);
      }
    }
  }]
});
w.show();
```



How to print a report directly to a printer.
## Syntax

```js
var response = utils.printDocument( printerName, copies, mediaSize, printParams, reportName,dirReports, datastoreId, reportFormat, reportParams);
```

## Details

* printerName &#8211; printer name
* copies &#8211; number of copies; e.g. 1
* mediaSize &#8211; dimernsion of the paper, expressed as 1-10 values (i.e. A0-A10); can be null
* printParams &#8211; js object containing parameters specific for the selected printer; if not needed, set it to {}
* reportName &#8211;  .jasper file name, which must be stored with the folder
* /reports
* dirReports &#8211; optional subfolder where the .jasper file is located; it is a subfolder of the one described above; if not needed, you have to set it to ‘’
* datastoreId &#8211; optional, related to the data source used by the .jasper report to get data from the database; if the default repository is used, then set it to null
* reportFormat &#8211; report format, e.g. PDF
* reportParams &#8211; input parameters required vy the .jasper report file; if not needed, set it to {}
* result: outcome; it could contain an error message if no printers has been configured or if the specified printer name has not been recognized or if the .jasper file is not located in the required path or in case of a generic print error. If the report has been successfully genrated and it has been sent to the printer spooler, then the "&#8221;Report printed." message is sent back,


How to get the field names and types for every fields in the select clause of a SQL query to execute. This can be helpful when creating programmatically a grid and there is the need to know how to format data.
## Syntax

```js
var jsonList = utils.getQueryColumns(sql, dataStoreId, separatedTransaction, interruptExecution, pars);
```

## Details

* sql &#8211; SQL query to execute, in order to fetch information about each field in the select clause
* dataStoreId &#8211; optional parameter (can be null); it defines the additional datastore to use when executing the query
* separatedTransaction &#8211; boolean flag used to define if the SQL query must be execute on a separated transation or not
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an errore during the execution of the SQL query
* pars &#8211;  list of parameters required by the SQL query, one for each binding variable; if not needed, set to []
* jsonList: the list of select fields is expressed as a JSON string, having the following format:

[{ &#8220;fieldName&#8221;: &#8220;FIELDXX&#8221;, &#8220;fieldType&#8221;: 1|2|&#8230; }, { … } , …]
where the fieldType reports the field type according to the JDBC Java.sql.Types notation.

Execute a SQL insert instruction, starting from a javascript object, instead of defining explicitelly the SQL script.
## Syntax

```js
var ok = utils.insertObject(obj, tableName, dataSourceId, separatedTransaction, interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to save in the specified table; data is related to the table fields and each object attribute name is expressed in "camel" format, i.e. if the table field has name PRODUCT_CODE, the attribute name must be productCode
* tableName &#8211; table name to use when creating the SQL insert instruction; field names as retrieved starting from the data model linked to the current table name: that means that it is mandatory to define a (writable) data model for that table, before invoking this javascript method; values are fechted starting from the obj argument
* dataSourceId &#8211; optional parameter (can be null); it defines the additional datastore to use when executing the SQL insert
* separatedTransaction &#8211; boolean flag used to define if the SQL query must be execute on a separated transation or not
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an error during the execution of the SQL query
* ok: true in case of SQL instruction executed correctly, an exception otherwise


Execute a SQL update instruction, starting from a javascript object, instead of defining explicitelly the SQL script.
## Syntax

```js
var ok = utils.updateObject(obj, emptyAsNull, forceAttributesToNull, tableName, dataSourceId, separatedTransaction, interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to save in the specified table; data is related to the table fields and each object attribute name is expressed in "camel" format, i.e. if the table field has name PRODUCT_CODE, the attribute name must be productCode
* tableName &#8211; table name to use when creating the SQL update instruction; field names as retrieved starting from the data model linked to the current table name: that means that it is mandatory to define a (writable) data model for that table, before invoking this javascript method; values are fechted starting from the obj argument
* emptyAsNull &#8211; this boolean flag can be set to true to force the conversion of ‘’ string values to null; it can be helpful to clear up some table fields
* forceAttributesToNull &#8211; this boolean flag can be used to force to null every table field not referred in the javascript object but defined in the linked data model
* dataSourceId &#8211; optional parameter (can be null); it defines the additional datastore to use when executing the SQL update
* separatedTransaction &#8211; boolean flag used to define if the SQL query must be execute on a separated transation or not
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an errore during the execution of the SQL query
* ok: true in case of SQL instruction executed correctly, an exception otherwise


Execute a SQL delete instruction, starting from a javascript object, instead of defining explicitelly the SQL script.
## Syntax

```js
var ok = utils.deleteObject(obj, tableName, dataSourceId, separatedTransaction, interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to delete in the specified table; data is related to the table fields and each object attribute name is expressed in "camel" format, i.e. if the table field has name PRODUCT_CODE, the attribute name must be productCode; only fields which are part of the primary key will be taken into account
* tableName &#8211; table name to use when creating the SQL delete instruction; field names as retrieved starting from the data model linked to the current table name: that means that it is mandatory to define a (writable) data model for that table, before invoking this javascript method; values are fechted starting from the obj argument: only the attributes related to the primary key will be used
* dataSourceId &#8211; optional parameter (can be null); it defines the additional datastore to use when executing the SQL delete
* separatedTransaction &#8211; boolean flag used to define if the SQL query must be execute on a separated transation or not
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an errore during the execution of the SQL query
* ok: true in case of SQL instruction executed correctly, an exception otherwise


Convert the specified table field into an attribute, according to the camel format.
## Syntax

```js
var attributeName = utils.camel(fieldName, firstCharUpper);
```

## Details

* fieldName &#8211; table field to convert to an attribute; e.g. a TABLE_NAME.PRODUCT_NAME will be converted to productName
* firstCharUpper &#8211; boolean flag used to force the first character to be in upper case; if set to true the previous field (PRODUCT_NAME) would become ProductName
* attributeName &#8211; outcome; the converted field in camel mode


Convert the specified attribute name to a table field , starting from am attributed expressed in camel format.
## Syntax

```js
var fieldName = utils.uncamel(attributeName);
```

## Details

* attributeName &#8211; attribute name, expressed in camel mode
* fieldName &#8211; outcome; the attribute name passed as argument will be converted as a field; e.g. productName -&gt;PRODUCT_NAME


Get the list of fields which compose a foreign key between the two specified tables.
## Syntax

```js
var json = utils.getRelation(dataStoreId, fkTable, pkTable);
```

## Details

* dataStoreId &#8211; optional data store id
* fkTable &#8211; starting table, hosting the foreign key
* pkTable &#8211; final table, used by the foreign key
* json &#8211; a String containing a list of objects: field name in the foreign key table, field name in the primary key table, fk name; example:

[{ &#8220;fkColumnName&#8221;: &#8220;&#8230;&#8221;, &#8220;pkColumnName&#8221;: &#8220;&#8230;&#8221;, &#8220;fkName&#8221;: &#8220;&#8230;&#8221;},{}&#8230;]

Get the list of the application tables in the schema identified by the data store id.
## Syntax

```js
var json = utils.getTablesInDataStore(dataStoreId);
```

## Details

* dataStoreId &#8211; optional data store id
* json &#8211; a String containing a list of table names; example:

["tablename1","tablename2",&#8230;]

Get the list of the table columns in the schema identified by the data store id.
## Syntax

```js
var json = utils.getColumnsInTable(datastoreId, tableName);
```

## Details

* dataStoreId &#8211; optional data store id
* tableName &#8211; table name
* json &#8211; a String containing a list of columns names; example:

["columnsname1","columnsname2",&#8230;]

Export grid content and save data in a CSV file.
## Syntax

```js
var ok = utils.saveGridExportInCSV(platformBaseUrl, functionId, panelId, filters, orders, attributes, titles, title, toFile);
```

## Details

* platformBaseUrl &#8211; base URL of the 4WS.Platform installation; e.g. http://localhost:8080/platform
* functionId &#8211; function identifier, e.g. the grid title in lowercase
* panelId &#8211; panel identifier of the grid linked to this export
* filters &#8211; list of elements: ["attribute name","operator","value","case sensitive"]
* where:
* "operator" can be "=", "&gt;", "like", …
* "case sensitive" can be true|false
* orders &#8211; list of elements: ["attribute name","sorting order"]
* where:
* "sorting order" can be "ASC" or "DESC"
* attributes &#8211; list of attribute names
* titles &#8211; list of header titles
* title &#8211; title showed in the first row
* toFile &#8211; absolute path, including the file name, where the csv will be saved


Execute a GQL query into a Google Datastore.
The datastore must be already configured as a global parameter.Once done that, it is possible to execute a query statement, in order to fetch a list of entities.
The query language is GQL: filtering and sorting conditions are strinctly ruled by the Google datastore. That means that additional indexes could be defined before executing the query. For instance, = operators can be used without additional indexes, but it is not so for sorting conditions or filtering conditions having not equal operators (e.g. &lt;, &lt;=, etc.).
See Datastore syntaxto get detail information about the syntax to use when filtering entities.
## Syntax

```js
var json = utils.executeQueryOnGoogleDatastore(gql,dataModelId,interruptExecution, params);
```

## Details

* gql &#8211; string value: GQL queryto execute; it can contain ? or :XXX
*  **dataModelId**  &#8211; it identifies the data model having &#8220;datastore&#8221; type, related to the entity to enquiry, so the GQL query must refer the same entity name related to the specified data model
* interruptExecution &#8211; boolean value; if true, an erroneous GQL instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql statement.
* An :XXX variable can be replaced by vo or params values

## Example

```js
var json = utils.executeQueryOnGoogleDatastore(
"SELECT * FROM Products WHERE companyId=:COMPANY_ID AND enabled='Y' ",
XXX, // XXX must be the data model id
true, // fire an Execution in case of error
[]
);
```

Note: every GQL instruction will be logged.

Execute a GQL query into a Google Datastore: only a block of data is got back.This method can be coupled with a grid panel where the data loading is limited to a block of data. Optional filtering/sorting conditions coming from the grid are automatically applied to the base GQL query. Note that filterable/sortable columns should be carefully defined according to the limits come with the Google Datastore and custom indexes must be defined in the Datastore first.
The datastore must be already configured as a global parameter.Once done that, it is possible to execute a query statement, in order to fetch a list of entities.
The query language is GQL: filtering and sorting conditions are strinctly ruled by the Google datastore. That means that additional indexes could be defined before executing the query. For instance, = operators can be used without additional indexes, but it is not so for sorting conditions or filtering conditions having not equal operators (e.g. &lt;, &lt;=, etc.).
See Datastore syntaxto get detail information about the syntax to use when filtering entities.
## Syntax

```js
var json = utils.getPartialResultOnGoogleDatastore(gql,dataModelId,interruptExecution, params)
```

## Details

* gql &#8211; string value: GQL queryto execute; it can contain ? or :XXX
*  **dataModelId**  &#8211; it identifies the data model having &#8220;datastore&#8221; type, related to the entity toinsert
* interruptExecution &#8211; boolean value; if true, an erroneous insertinstruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql statement.
* An :XXX variable can be replaced by vo or params values

## Example

```js
var json = utils.getPartialResultOnGoogleDatastore(
"select * from Products where companyId=:COMPANY_ID and enabled='Y' ",
XXX, // XXX must be the data model id
true, // fire an Execution in case of error
[]
);
```


Note: every GQL instruction will be logged.

Insert a single entity into the Google Datastore. The entity is expressed as a Javascript object.
The datastore must be already configured as a global parameter.Once done that, it is possible to executeoperations on the Google Datastore.
## Syntax

```js
var json = utils.insertObjectOnGoogleDatastore(obj, dataModelId, interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to save in the specified Datastoreentity
*  **dataModelId**  &#8211; it identifies the data model having &#8220;datastore&#8221; type, related to the entity toinsert
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an error during the execution of theoperation
* ok: true in case of the operation has beenexecuted successfully, an exception otherwise


Updatea single entity into the Google Datastore. The entity is expressed as a Javascript object.
The datastore must be already configured as a global parameter.Once done that, it is possible to executeoperations on the Google Datastore.
## Syntax

```js
var json = utils.updateObjectOnGoogleDatastore(obj, dataModelId, interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to save in the specified Datastoreentity
*  **dataModelId**  &#8211; it identifies the data model having &#8220;datastore&#8221; type, related to the entity toupdate
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an error during the execution of theoperation
* ok: true in case of the operation has beenexecuted successfully, an exception otherwise


Deletea single entity fromthe Google Datastore. The entity is expressed as a Javascript object.
The datastore must be already configured as a global parameter.Once done that, it is possible to executeoperations on the Google Datastore.
## Syntax

```js
var json = utils.deleteObjectOnGoogleDatastore(obj, dataModelId, interruptExecution);
```

## Details

* obj &#8211; a Javascript object related to the entity stored in the Datastore and to remove
*  **dataModelId**  &#8211; it identifies the data model having &#8220;datastore&#8221; type, related to the entity toremove
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an error during the execution of theoperation
* ok: true in case of the operation has beenexecuted successfully, an exception otherwise


Execute a query into a Mongo DB.
The Mongo DBmust be already configured through theglobal parameters. Once done that, it is possible to execute a query statement, in order to fetch a list of documents.
The query language must fit the Mongo DB syntax: filtering and sorting conditions are as powerful as the ones available with the standard SQL language, but expressed with a different syntax. In order to get quick responses when executing enquires, it is important to define special indexes. These can be defined in the &#8220;Indexes&#8221; folder of the data model definition.
SeeMongo DB syntaxto get detail information about the syntax to use when filtering documents.
## Syntax

```js
var json = utils.executeQueryOnMongoDb(where,dataModelId,interruptExecution, params);
```

## Details

* where&#8211; string value: it represents only the where part of the query; it can contain ? or :XXX
*  **dataModelId**  &#8211; it identifies the data model having &#8220;Mongo DB&#8221; type, related to the collectionto enquiry, so the query must refer the same collectionname related to the specified data model
* interruptExecution &#8211; boolean value; if true, an erroneous instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql statement.
* An :XXX variable can be replaced by vo or params values

## Example

```js
var json = utils.executeQueryOnMongoDb(
"{ companyId: :COMPANY_ID }, { price: { gt: 1234.5 } } ",
XXX, // XXX must be the data model id
true, // fire an Execution in case of error
[]
);
```

Note: every query instruction will be logged.

Execute a query into a Mongo DB: only a block of data is got back.This method can be coupled with a grid panel where the data loading is limited to a block of data. Optional filtering/sorting conditions coming from the grid are automatically applied to the base query.
The Mongo DBmust be already configured through theglobal parameters. Once done that, it is possible to execute a query statement, in order to fetch a list of documents.
The query language must fit the Mongo DB syntax: filtering and sorting conditions are as powerful as the ones available with the standard SQL language, but expressed with a different syntax. In order to get quick responses when executing enquires, it is important to define special indexes. These can be defined in the &#8220;Indexes&#8221; folder of the data model definition.
SeeMongo DB syntaxto get detail information about the syntax to use when filtering documents.
## Syntax

```js
var json = utils.getPartialResultOnMongoDb(where,dataModelId,interruptExecution, params)
```

## Details

* where&#8211; string value: it represents only the where part of the query; it can contain ? or :XXX
*  **dataModelId**  &#8211; it identifies the data model having &#8220;Mongo DB&#8221; type, related to the collectionto enquiry, so the query must refer the same collectionname related to the specified data model
* interruptExecution &#8211; boolean value; if true, an erroneous instruction fires an exception that will interrupt the javascript execution; if false, the js execution will continue
* params &#8211; this is optional: you can omit it at all, or you can specify a series of arguments separated by a comma (do not use []); these additional parameters represent values which replace ? symbols in the sql statement.
* An :XXX variable can be replaced by vo or params values

## Example

```js
var json = utils.getPartialResultOnMongoDb(
"{ companyId: :COMPANY_ID},{ enabled: "Y" } ",
XXX, // XXX must be the data model id
true, // fire an Execution in case of error
[]
);
```

Note: every queryinstruction will be logged.

Insert a single documentinto the Mongo DB. The documentis expressed as a Javascript object.
The Mongo DBmust be already configured through theglobal parameters.Once done that, it is possible to executeoperations on it.
## Syntax

```js
var returnedObj = utils.insertObjectOnMongoDb(obj,dataModelId,interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to saveas a document in the Mongo DB collection specified through the data store id
*  **dataModelId**  &#8211; it identifies the data model having &#8220;Mongo DB&#8221; type, related to the collection whereinserting data
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an error during the execution of theoperation
*  **returnedObj** : the object passed as argumentin case of the operation has beenexecuted successfully, an exception otherwise

Note that the returned objectcontains additional data: the &#8220;id&#8221; atttribute represents the primary key of any document in Mongo DB and it is automatically generated by the database and got back by this method.
In case the defined data model includes unique keys, these are checked out before executing the instruction and an exception is fired in case of a unique key violation.
In case the defined data model includes a counter (e.g. internal counter), this is automatically reckoned internally and got back to the returned object, which would contained it as well.

Updatea single documentinto the Mongo DB. The documentis expressed as a Javascript object.
The Mongo DBmust be already configured through theglobal parameters.Once done that, it is possible to executeoperations on it.
## Syntax

```js
var ok = utils.updateObjectOnMongoDb(obj,dataModelId,interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to saveas a document in the Mongo DB collection specified through the data store id
*  **dataModelId**  &#8211; it identifies the data model having &#8220;Mongo DB&#8221; type, related to the collection where updatingdata
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an error during the execution of theoperation
*  **ok** : true in case of the operation has beenexecuted successfully, an exception otherwise

In case the defined data model includes unique keys, these are checked out before executing the instruction and an exception is fired in case of a unique key violation.

Deletean already existing document fromthe Mongo DB. The documentis expressed as a Javascript object.
The Mongo DBmust be already configured through theglobal parameters.Once done that, it is possible to executeoperations on it.
## Syntax

```js
var returnedObj = utils.deleteObjectOnMongoDb(obj,dataModelId,interruptExecution);
```

## Details

* obj &#8211; a Javascript object containing the data to removefromthe Mongo DB collection specified through the data store id
*  **dataModelId**  &#8211; it identifies the data model having &#8220;Mongo DB&#8221; type, related to the collection where deletingdata
* interruptExecution &#8211; boolean flag used to define if the executing of the current server-side javascript program must be interrupted in case of an error during the execution of theoperation
*  **ok** : true in case of the operation has beenexecuted successfully, an exception otherwise


Register a file (store it in CON55and if needed in CON54 as well) so that it can be linked to all the registered devices or only to devices linked to the specified username.
## Syntax

```js
utils.addFileToMobileDevices(String fullPathName,String fileName,String username)
```

## Details

*  **fullPathName**  &#8211;absolute path, in the central server, where the file is stored; it must include the file name too
*  **fileName**  &#8211;file name, without the path
*  **username**  &#8211;it can be null: if so, the file is linked to all registered devices; if this argument is not empty, then the file is linked to all devices binded to this username



Create a text file and fill in with the passed content.
## Syntax

```js
var outcome = utils.createTextFile(String fileName, String fileContent, Boolean overwrite, Long directoryId);
```

## Details

*  **fileName**  &#8211;file name; it can includes a subpath to append to the base path specified through directoryId
*  **fileContent**  &#8211; text content to save
*  **overwrite**  &#8211; true to overwrite the file content if already exists, falseto ignore this operation and returns false as result
*  **directoryId**  &#8211;directory id directory identifier, used to define the absolute path, in the central server, where the file will be stored; if null, there must be one only entry for this application
*  **outcome** : true in case of the operation has beenexecuted successfully, an exception otherwise




Read a text file located on the server

```js
var textString = utils.readTextFile(filePath);
```

## Details

*  **filePath** : Filepath + Filename of the file to read
*  **textString** : The content of the read file


Read a text file located on the server with a specific char-set.
A text file can be saved with different charset formats. You have to know in advance which format to use. Examples of formats are: UTF-8 or Windows-1252

```js
var textString = utils.readTextFile(filePath, charSet);
```

## Details

*  **filePath** : Filepath + Filename of the file to read
*  **charSet**  &#8211; the charset to use when reading the text file
*  **textString** : The content of the read file


Deletea file previously stored in a specific path.
## Syntax

```js
var outcome = utils.deleteFile(String fileName,Long directoryId);
```

## Details

*  **fileName**  &#8211;file name; it can includes a subpath to append to the base path specified through directoryId
*  **directoryId**  &#8211;directory id directory identifier, used to define the absolute path, in the central server, where the file will be stored; if null, there must be one only entry for this application
*  **outcome** : true in case of the operation has beenexecuted successfully, an exception otherwise



Get the path defined for the specific directory id.
## Syntax

```js
var path = utils.getDirectoryPath(Long directoryId);
```

## Details

*  **directoryId**  &#8211;directory id directory identifier, used to define the absolute path
*  **path** :the absolute path defined to that id



Get thedriver name used to create connection to the Platform main repository.
## Syntax

```js
var name = utils.getDriverNameDefaultConnection();
```

## Details

*  **name** :thedriver name related to the default database connection



Execute synchronously a server&#8211;side JS action. A new SQL transaction is created for this action.
## Syntax

```js
var json =utils.executeAction(Long actionId,Map vo,Map params,Map headers);
```

## Details

*  **actionId** :action id related to the action to execute
*  **vo** : value object to pass
*  **params** : request parameters to pass; read on the other side through reqParams.xxx
*  **header** : request headers; read on the other side through reqHeaders.xxx



Read the specified URL and convert the HTML content to an image and save it to the server file system.
## Syntax

```js
utils.convertUrlToImage(String url, String imagePath);
```

## Details

* 
 **url:**  URL to read, related to HTML content

* 
 **imagePath:**  absolute path + image file name where saving the image

* 
fire an exception in case of errors.




Read the HTML content and convert it to an image and save the image to the server file system.
## Syntax

```js
utils.convertHtmlToImage(String html, String imagePath);
```


## Details

* 
 **html:**  HTML content to read

* 
 **imagePath:**  absolute path + image file name where saving the image

* 
fire an exception in case of errors.




Generate a short URL.
## Syntax

```js
var url = utils.getShortUrl(String realUrl);
```

## Details

* 
 **realUrl:** the URL to shorten

* 
returns a new shorter URL




Send an SMS message through some carrier.
 **Important note** : an SMS provider must be configured first.
Two alternatives are allowed:

Twilio web service; you have to configure two parameters: TWILIO_ACCOUNT_ID and TWILIO_AUTH_TOKEN
an email gateway can be used; in that case, you have to configure the SMS_SMTP_xxx parameters and the phone numbers must be expressed appropriately.

## Syntax

```js
var json = utils.sendSmsMessage(String fromPhoneNr,String toPhoneNr,String text,Boolean logMessage);
```

## Details

* 
 **fromPhoneNr** : phone number used to identify the starting device

* 
 **toPhoneNr** : phone number where the message will be sent

*  **text** : text message to send
* returnan outcome, expressed as a JSON string, containing: { &#8220;success&#8221;: true } if the operation has been completed successfully, { &#8220;success&#8221;: false, &#8220;message&#8221;: &#8220;&#8230;&#8221; } otherwise

Pay attention to the phone number format, with should always include the international prefix:e.g. +0039&#8230;.


Read up to 10000 rows x 1000 columns from the xls file stored in the specified path and get back the content of a specific folder.
## Syntax

```js
var list = utils.getXlsContent(String dirId,String fileName,int sheetIndex,int fromRow,String... attributeNames);
```

## Details

 **dirId** : path identifier
  **f**  **ileName**  name of the xls file
 **sheetIndex**  sheet index inside the spreadsheet, starting from 0
 **fromRow**  the content will be read starting from the specified row index (the first row has index 0)
 **attributeNames** , list of attributes, assigned to each column, starting from leftmost column to the right
return a list of js objects, where each object is expressed as a set of couples &lt;attributename, related value&gt;

Values stored in each js object can be accessed as: object.get(&#8220;attributeName&#8221;)

Read up to the specified number of rows, starting from the specified index (0..x) from the csv file stored in the specified path and get back the content of a specific folder.
dirId path identifier
fileName name of the csv file
attributeNames, list of attributes, assigned to each column, starting from leftmost column to the right
## Syntax

```js
var list = utils.getCsvContent(String sep,String dirId,String fileName,Integer startRow,Integer blockSize,String... attributeNames);
```

## Details

 **sep**  tokens separator: ; or ,
 ** dirId** : path identifier; optional and helpful for files stored in the cloud; you can set it to null, to save temporarelly the uploaded file in the tmp dir of the application server
  **f**  **ileName**  name of the csvfile

 **startRow**  row index; if null it is the first row, i.e. 0


 **blockSize**  max number of rows to read, if available; if null it is set to 10000


attributeNames** , list of attributes, assigned to each column, starting from leftmost column to the right

return a list of js objects, where each object is expressed as a set of couples &lt;attributename, related value&gt;

A list of js objects, where each object is expressed as a set of couples &lt;attributename, related value&gt;; a 0 length list in case of no more rows available.
It supports also nested objects and list of objects: it depends on the definition of the attribute lists.
A few examples of attributes:
[ &#8220;attr1&#8221;, &#8220;subobject.attrsub1&#8221;, &#8220;subobject.attrsub2&#8221;, &#8220;sublist[0].subattr3&#8221;,&#8220;sublist[0].subattr4&#8221;,&#8220;sublist[1].subattr5&#8221; ]

Generate a report starting from a .jasper report template and save it to the server file system, in the specified path.
## Syntax

```js
var json = utils.saveDocument(reportName,dirReports, datastoreId, compId,reportFormat, reportParams,savePath);
```

## Details

 **reportName**  .jasper report name
 **dirReports**  optional folder where the .jasper file is located; thisis arelative pathand it is always contained within the subolder &lt;application-context-path&gt;/reports/
 **datastoreId**  optional data source id used by the .jasper template to read data from the database
 **compId**  optional value: business component id to use to fill in the report
 **reportFormat**  report format to use when creating the report; e.g. PDF
 **reportParams**  input parameters required by the report template
 **savePath**  path where the generated report will be saved; it must includes the file name
error message, in case of errors; &#8220;&#8221; if the generation has been successfully completed

It returns a JSON string containg:
{ &#8220;success&#8221;: true }
if the report has been created successfully, or a JSON string having this format otherwise:
{ &#8220;success&#8221;: false, &#8220;message&#8221;: &#8220;&#8230;&#8221;}
## Example
and the database schema to pass forward to the report is the Platform repository schema:

```js
var reportParams = new Object();

reportParams.paramxyz = "...";

...

var json = utils.saveDocument("mytemplate.jasper",null, null, null,"PDF", reportParams,"pathwheresavingthepdf/myreport.pdf");

```


Generate a screenshot of the first page of a PDF document. Useful when you need to create a documents gallery where showing a preview of every document.
## Syntax

```js
var json = utils.convertPdfToImage(pdfDirId, pdfFileName, imgDirId, imageExtension, scale);
```

## Details


 **pdfDirId**  &#8211; folder identifier, where the input PDF file is already stored


 **pdfFileName &#8211;**  PDF file name, stored in the folder identified by pdfDirId


 **imgDirId** &#8211; folder identifier, where the image will be saved


 **imgExtension** &#8211; image format; allowed formats: png


 **scale** &#8211; positive number &lt;= 1.0, used to define how much to reduce the PDF; e.g. 0.3; the more is reduced, the smaller the image is
The method returns the image name.


## Example

```js
var fileName = utils.convertPdfToImage(19,"a1.pdf",9,"png",0.3);
utils.log("FILE: "+fileName,"WARN");
```



Convert a TIFF image to a JPEG image.
## Syntax

```js
utils.convertTifToJpg(Long tifDirId,String tifFileName,Long jpgDirId,String jpgFileName,Float compressionFactor);
```

## Details


 **tifDirId**  &#8211; folder identifier, where the input TIFF imagefile is already stored


 **tifFileName &#8211;** TIFF image file name, stored in the folder identified by tifDirId


 **jpgDirId** &#8211; folder identifier, where the JPEG image will be saved


 **jpgFileName** &#8211; file name for the JPEG image to create


 **compressionFactor** &#8211; positive number &lt;= 1.0, used to define the compression factor theJPEG image




(From version 5.2) Import into the embedded CMS a single file found in the location identified by sourceDirId and load it into the location identified by destDirId.
The file in the original position will not be removed.
## Syntax

```js
var uuid = utils.importFileInCMS(
      Long sourceDirId,
      String fileName,
      Long destDirId,
      Long dataSourceId,String tableName);
```


## Details


 **sourceDirId**  &#8211; source location for the file to import


 **fileName** &#8211; file name to import, located in sourceDirId


 **destDirId** &#8211; destination location for the file to import


 **dataSourceId** &#8211; data source identified, where the specified &#8220;tableName&#8221; is defined


 **tableName** &#8211; table name for which a data model MUST have been defined for such a table: it is used to figure out whether the file is versioned or not (defined at model level)


Returns UUID related to the file uploaded





(From version 5.2) Import into the embedded CMS a single file found in the location identified by sourceDirId and load it into the location identified by destDirId.
The file in the original position will not be removed.
## Syntax

```js
var uuid = utils.importFileInCMS(
      String path,
      Long destDirId,
      Long dataSourceId, String tableName);
```


## Details


 **path**  &#8211; abs path + file name, related to the file to import


 **destDirId** &#8211; destination location for the file to import


 **dataSourceId** &#8211; data source identified, where the specified &#8220;tableName&#8221; is defined


 **tableName** &#8211; table name for which a data model MUST have been defined for such a table: it is used to figure out whether the file is versioned or not (defined at model level)


Returns UUID related to the file uploaded





(From version 5.2) Import into the embedded CMS a single file found in the location identified by sourceDirId and load it into the location identified by destDirId, by replacing the previous one.
The file in the original position will not be removed.
## Syntax

```js
utils.updateFileInCMS(String uuid,String path);
```


## Details


 **uuid**  -unique identifier for the already existing file, which will be replaced by the current one


 **path**  &#8211; abs path + file name, related to the file to import





(From version 5.2) Import into the embedded CMS a single file found in the location identified by sourceDirId and load it into the location identified by destDirId, by replacing the previous one.
The file in the original position will not be removed
## Syntax

```js
utils.updateFileInCMS(
      String uuid,
      Long sourceDirId,
      String fileName);
```


## Details


 **uuid**  &#8211; unique identifier for the already existing file, which will be replaced by the current one


 **sourceDirId**  &#8211; source location for the file to import


 **fileName**  &#8211; file name to import, located in sourceDirId





(From version 5.2) Remove a single file from the embedded CMS.
## Syntax

```js
utils.deleteFileFromCMS(String uuid);
```


## Details


 **uuid**  &#8211; unique identifier





(From version 5.2) Import all files found in the location identified by sourceDirId and load them into the location identified by destDirId.
If backupDirId is not null, input files are also moved (removed from the source folder) to the location identified by backupDirId.
If backupDirId is null, input files are simply deleted from the source folder.

In the same source location a .csv file could be found: if it exists and the &#8220;csvFileName&#8221; argument has been specified,
then it will be used to read metadata to map for each indexed file.
In order to use this csv file, the following conditions must be satisfied:

the first row in the csv file must contain the attribute names to use when loading its content in the table&#8217;s fields (attributes not found in the datamode/table will be ignored and a warning message will be logged)
one of the csv fields must be related to the corresponding file name; such field must be specified as this method argument

The csv file will be deleted after its processing (optionally moved along with the files in the backup destination, if specified)
## Syntax

```js
utils.bulkImport(
      Long sourceDirId,
      Long destDirId,
      Long backupDirId,
      Long dataSourceId,String tableName,
      String csvFileName,String csvFileNameField,String csvUniqueIdField, String csvSep,
      Map defaultValues,Map mapping,String nullString,
      Boolean skipWithErrors,Boolean skipFileNotInCSV,
      Long beforeInsertActionId,Long afterInsertActionId);
```


## Details




 **sourceDirId**  source location for files to import


 **destDirId**  destination location for files to read (to move)


 **backupDirId**  optional parameter: if specified, input files are not only copied to the destination dir but also here, before being deleted from the source location


 **dataSourceId**  data source identified, where the specified &#8220;tableName&#8221; is defined


 **tableName**  table name where files will be indexed (the uuid + destDirId); a datamodel MUST have been defined for such a table


 **csvFileName**  file name for the csv to process along with files


 **csvFileNameField**  field name in the first row of the csv file, related to file names, which allows to map each row in the csv with the corresponding file

 **csvUniqueIdField**  (optional) field name in the first row of the csv file, related to a value which identifies uniquelly a row/file in the file: it will be used when updating files already indexed; if not specified the &#8220;csvFileNameField&#8221; property will be used instead

 **csvSep**  ; or , symbol


 **defaultValues**  collection of attribute names + default values, to set in case the metadata does not provide a value for these attributes; :XXX variables are supported


 **mappingCsvToFields**  collection of attribute names defined as first row in csv vs field name in the table name (optional)


 **nullString**  string value representing a null value; e.g. NULL (optional)


 **skipWithErrors**  trueto undo any insert in case of errors


 **skipFileNotInCSV**  trueto skip file loading if the same file was not found in the CSV file


 **beforeInsertActionId**  (optional) action id to execute before inserting a csv row: the &#8220;vo&#8221; js variable will be passed to the action to get access to the row; a return false would skip the row inserting


 **afterInsertActionId**  (optional) action id to execute just after inserting a csv row: the &#8220;vo&#8221; js variable will be passed to the action to get access to the row






## Example

```js
var defaultValues = new Object();
var map = new Object();
map["ID_CORRISPONDENZA"] = "ID_Corrispondenza";
map["DATA_CONTABILE"] = "DataContabile";
map["FK_TIPOLOGIA_CORRISPONDENZA"] = "FK_TipologiaCorrispondenza";
map["DESCRIZIONE"] = "Descrizione";
map["NOME_FILE_FISICO"] = "NomeFile_Fisico";
map["DATA_FATTURA"] = "DataFattura";


utils.bulkImport(
      29, // directory id where files to import are located
      49, // directory id where files will be stored (base dir)
      39, // optional directory id where input files will be moved after being read (backup dir),
      null, // data source id related to the db schema where the application table has been defined
      "MY_DOCUMENTS", // table name where metadata read from the csv file will be imported, 
                      // for each file in input
      "index.csv", // csv file containing the matadata to import in the database table
      "FilaNameField", // the first line of the csv file must contain all column identifiers; 
                       // one of these must be this one, related to the column having the names 
                       // of files to import
      null,
      ";", // fields separator in the csv file
      defaultValues, // js object (a map) containing default values to apply to each record 
                     // to store in the specified table, in case no value has been defined for them; 
                     // entries are names for fields in table 
      map, // js object (a map) used to convert names in the first row of the csv file to names 
           // of fields in table 
      "NULL", // optional value to decode in the csv file: every occurrence found in the csv file 
              // with this value will be converted to null
      true, // true will skip the current processed row in the csv file in case of errors and 
            // continue with the next one; false will interrupt the processing of file:
            // previous rows have been already loaded in the table 
            // and corresponding files indexed
      true, // true will skip the processing of a file if not found inside the csv file
      1059, // optional action id related to a server-side js action to execute before 
            // every file to process: a "vo" variable is available, containing all metadata read from
            // the csv file; retuen false will skip the processing of the current row and file import
      1069  // optional action id related to a server-side js action to execute just after
            // the processing a row; the uuid value is available as part of the "vo" variable
            // passed to the action
);
```



(From version 5.2) Import all files found in the location identified by sourceDirId and load them into the location identified by destDirId.
If backupDirId is not null, input files are also moved (removed from the source folder) to the location identified by backupDirId.
If backupDirId is null, input files are simply deleted from the source folder.

In the same source location a .csv file could be found: if it exists and the &#8220;csvFileName&#8221; argument has been specified, then it will be used to read metadata to map for each indexed file.
In order to use this csv file, the following conditions must be satisfied:

the first row in the csv file must contain the attribute names to use when loading its content in the table&#8217;s fields(attributes not found in the data model /table will be ignored and a warning message will be logged)
one of the csv fields must be related to the corresponding file name; such field must be specified as this method argument

The csv file will be deleted after its processing (optionally moved along with the files in the backup destination, if specified)
## Syntax

```js
utils.bulkImportFromFTP(
      String host, Integer port, Boolean useSSL, String username, String password, String remoteDir, 
      String fileFilter,
      Long destDirId,
      Long backupDirId,
      Long dataSourceId,String tableName,
      String csvFileName,String csvFileNameField,String csvUniqueIdField, String csvSep,
      Map defaultValues,
      Map mappingCsvToFields,String nullString,
      Boolean skipWithErrors,Boolean skipFileNotInCSV,
      Long beforeInsertActionId,Long afterInsertActionId
);
```



## Details


 **host+&#8230;fileFilter source location in an FTP server for files to import** 


 **sourceDirId**  source location for files to import


 **destDirId**  destination location for files to read (to move)


 **backupDirId**  optional parameter: if specified, input files are not only copied to the destination dir but also here, before being deleted from the source location


 **dataSourceId**  data source identified, where the specified &#8220;tableName&#8221; is defined


 **tableName**  table name where files will be indexed (the uuid + destDirId); a datamodel MUST have been defined for such a table


 **csvFileName**  file name for the csv to process along with files


 **csvFileNameField**  field name in the first row of the csv file, related to file names, which allows to map each row in the csv with the corresponding file


 **csvUniqueIdField**  (optional) field name in the first row of the csv file, related to a value which identifies uniquelly a row/file in the file: it will be used when updating files already indexed; if not specified the &#8220;csvFileNameField&#8221; property will be used instead


 **csvSep**  ; or , symbol


 **defaultValues**  collection of attribute names + default values, to set in case the metadata does not provide a value for these attributes; :XXX variables are supported


 **mappingCsvToFields**  collection of attribute names defined as first row in csv vs field name in the table name (optional)


 **nullString**  string value representing a null value; e.g. NULL (optional)


 **skipWithErrors**  trueto undo any insert in case of errors


 **skipFileNotInCSV**  trueto skip file loading if the same file was not found in the CSV file


 **beforeInsertActionId**  (optional) action id to execute before inserting a csv row: the &#8220;vo&#8221; js variable will be passed to the action to get access to the row; a return false would skip the row inserting


 **afterInsertActionId**  (optional) action id to execute just after inserting a csv row: the &#8220;vo&#8221; js variable will be passed to the action to get access to the row



## Example

```js
var defaultValues = new Object();
var map = new Object();
map["ID_CORRISPONDENZA"] = "ID_Corrispondenza";
map["DATA_CONTABILE"] = "DataContabile";
map["FK_TIPOLOGIA_CORRISPONDENZA"] = "FK_TipologiaCorrispondenza";
map["DESCRIZIONE"] = "Descrizione";
map["NOME_FILE_FISICO"] = "NomeFile_Fisico";
map["DATA_FATTURA"] = "DataFattura";


utils.bulkImportFromFTP(
      "myFtpHost", 
      myFtpPort,
      true // use SSL for the FTP connection
      "ftpUsername", 
      "ftpPassword"
      "myFtpRemoteDirToWorkWith", 
      null, // optional filtering condition to apply when reading files from the specified remote dir
      29, // directory id where files to import are located
      49, // directory id where files will be stored (base dir)
      39, // optional directory id where input files will be moved after being read (backup dir),
      null, // data source id related to the db schema where the application table has been defined
      "MY_DOCUMENTS", // table name where metadata read from the csv file will be imported, 
                      // for each file in input
      "index.csv", // csv file containing the matadata to import in the database table
      "FilaNameField", // the first line of the csv file must contain all column identifiers; 
                       // one of these must be this one, related to the column having the names 
                       // of files to import
      null,
      ";", // fields separator in the csv file
      defaultValues, // js object (a map) containing default values to apply to each record 
                     // to store in the specified table, in case no value has been defined for them; 
                     // entries are names for fields in table 
      map, // js object (a map) used to convert names in the first row of the csv file to names 
           // of fields in table 
      "NULL", // optional value to decode in the csv file: every occurrence found in the csv file 
              // with this value will be converted to null
      true, // true will skip the current processed row in the csv file in case of errors and 
            // continue with the next one; false will interrupt the processing of file:
            // previous rows have been already loaded in the table 
            // and corresponding files indexed
      true, // true will skip the processing of a file if not found inside the csv file
      1059, // optional action id related to a server-side js action to execute before 
            // every file to process: a "vo" variable is available, containing all metadata read from
            // the csv file; retuen false will skip the processing of the current row and file import
      1069  // optional action id related to a server-side js action to execute just after
            // the processing a row; the uuid value is available as part of the "vo" variable
            // passed to the action
);
```


(From version 5.1.1) List of functions for users and roles management.
 **existUser(String companyId, Long siteId, String userCodeId)**  : check the user exist (true: exist; false: not exist)

```js
var exist = utils.existUser('00000', 100, 'TEST');
```

 **createUser(String companyId, Long siteId, String userCodeId, String description, String password, String languageId, Map userAttributes, Map[] rolesAttributes)**  : create the user

```js
utils.createUser('00000', 100, 'TEST', 'User of test', 'pwdtest', 'EN', 
 {siteIdSub02: 100}, 
 [{siteId: 100, roleId: 'TEST_ROLE', startDate: utils.addDate('DAY', 0)}]
);
```

 **updateUser(String companyId, Long siteId, String userCodeId, String languageId, Map userAttributes)**  : update the user attribute (example: description, expired date, locked etc)

```js
utils.updateUser('00000', 100, 'TEST', 'EN', {description: 'User of test', locked: 'N'});
```

 **updatePeopleData(String companyId, Long siteId, String userCodeId, Map peopleAttributes)**  : update the contact attributes

```js
utils.updatePeopleData('00000', 100, 'TEST', {eMail: 'test@domain.com'});
```

 **addUserRole(String companyId, Long siteId, String userCodeId, Map[] rolesAttributes)**  : add one or more roles at user

```js
utils.addUserRole('00000', 100, 'TEST', 
 [{siteId: 100, roleId: 'TEST_ROLE', startDate: utils.addDate('DAY', 0)}]
);
```

 **updateUserRole(String companyId, Long siteId, String userCodeId, Map[] rolesAttributes)**  : can change the end date of role for user

```js
utils.updateUserRole('GLOBO', 100, 'TEST', 
 [{siteId: 100, roleId: 'AGENTE', startDate: utils.addDate('DAY', 0), endDate: utils.addDate('DAY', 100)}]
);
```

 **userRoleActive(String companyId, Long siteId, String userCodeId, String roleId, Date activeDate)**  : check if the role is active for user in date

```js
utils.userRoleActive('00000', 100, 'TEST', 'TEST_ROLE', utils.addDate('DAY', 0));
```



Delete a single file to the FTP server.
## Syntax

```js
var ok = utils.deleteFTPFile(host, port, useSSL, username, password, remoteDir, fileName);
```

## Details

* host &#8211; FTP server host
* port &#8211; FTP server port (e.g. 21)
* useSSL &#8211; boolean flag, used to specify if FTPS must be used
* username &#8211; username to use to authenticate to the FTP server
* password &#8211; password to use to authenticate to the FTP server
* remoteDir &#8211; folder in the FTP server
* fileName &#8211; file name



Rename or move a single file to the FTP server.
## Syntax

```js
var ok = utils.renameFTPFile(host, port, useSSL, username, password, fromFileName, toFileName);
```

## Details

* host &#8211; FTP server host
* port &#8211; FTP server port (e.g. 21)
* useSSL &#8211; boolean flag, used to specify if FTPS must be used
* username &#8211; username to use to authenticate to the FTP server
* password &#8211; password to use to authenticate to the FTP server
* fromFileName &#8211; absolute path with file name in the FTP server
* toFileName &#8211; new absolute path with file name in the FTP server


                

---


