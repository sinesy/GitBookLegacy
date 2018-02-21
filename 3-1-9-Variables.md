# Variables

Variables \(or parameters\) are a way to dynamically define values to pass to business components on the server side or to windows/panes on the GUI.  
 **They are expressed as :VARIABLENAME.**

A user can specify variables in several components:

* **business components** : in the where clause, to specify a dynamic filter, such as the one needed to fetch a single record for a detail form
* **window titles** : a title could be composed as the concatenation of a static text plus a dynamic content, coming for instance from the parent window. Let’s take the case of a list of orders identified by year/docnr: a user could open the detail window starting from the selected row on the list and the detail window could have as a title the year/docnr coming from the data model of the grid’s row; in that case, two variables can be defined in the detail window parameters list: one for the year, the other of the docnr and the parent window who has the task to open the detail window should pass the values for these variables
* **panel titles** : these can be managed in the same way described for window titles
* **action content** :passed to the server side through Ajax requests.

There are a few default variables, that do not need to be defined and set by the user: they are system variables, declared automatically by 4WS.Platform and used anywhere; these are the predefined variables:  
 **:USERNAME**  – username of the logged user  
 **:LANGUAGE\_ID**  – the current language, binded to the logged user  
 **:APPLICATION\_ID**  – the current application identifier  
 **:TODAY**  – a date without time  
 **:NOW**  – a date+time

In addition, there are some other variables, available in case 4WS.Platform is used with the default implementation based on 4WS database tables \(for authentication, authorizations, menu\)  
 **:COMPANY\_ID**   
 **:COMPANY\_ID\_AS\_NUM**   
 **:SITE\_ID**   
 **:YEAR**   
 **:MONTH**   
 **:DAY**   
 **:DOW**

**How To: Add / Define variable on server**

```js
new SyncRequest().send(contextPath+"/wagutility/sendcustomappluservar?applicationId="+window.applicationId+"&amp;code=CODE&amp;value=VALUE", "POST",'',"application/json");
```

**How To: Removecustom variable on server**

```js
new SyncRequest().send(contextPath+"/wagutility/removecustomappluservar?applicationId="+window.applicationId+"&amp;code=CODE", "POST",'',"application/json");
```

Once the variable has been passed to the server and stored in the user session, you can access to it from within a server-side javascript action, through the instruction:

```js
utils.getVariable("variableName");
```

For the example above:utils.getVariable\(“CODE”\);

---



