# Web Service

A service task can act as a web service caller by setting the folllowing task properties in this way:  
Id and Name: they identity the task and they are mandatory; be sure NOT to include accent characters in these fields \(only alphanumeric characters are allowed\).  
Documentation: an optional description of this task  
Class:  **it.sinesy.activiti.services.ExecuteComponentServiceTask**  
Class fields: in this list of fields, a set of properties must be defined, in order to correctly define the web service invocation:  
name: property name to refer  
string value: value to assign to that property  
expression: optional expression to set, e.g.  
 ${VARIABLE == ’Test’ ? YES : ’NO’}

A typical web service invocation available within 4WS.Platform would contain the following couples name-value:  
name = applicationId  
string value =

name = companyId  
string value =

name = url  
string value = [http://host:port/platform/getList?param1=val1](http://host:port/platform/getList?param1=val1)**&**param2=val2

**Important note:** pay attention to the URL definition: the Activiti workflow editor does not allow you to write the & symbol: if you do it, it is likely that the Service Task properties will not be opened any more; for each & to include in the URL definition, use

```
&amp;
```

A more detailed example related to the invocation of the executeJs service available in Platform is:  
ClassFields  
url = [http://host:port/platform/executeJs?applicationId=XXX&appId=XXX&actionId=xxx&userId=ADMIN](http://host:port/platform/executeJs?applicationId=XXX&amp;appId=XXX&amp;actionId=xxx&amp;userId=ADMIN)  
httpMethod = POST  
companyId = XXXXX  
applicationId = XXX

Note that  **no credentials are required**  in this kind of communication, since the utility class referred is automatically able to authenticate in 4WS.Platform, starting from the user currently associated to the Activiti process, since both products share the same identity management system \(users and roles\).

Optional parameters:

name = requestBody  
string value = { "attr": value, … }

name = httpMethod  
string value = GET \| POST \| …

name = username  
string value =

name = fireError  
string value = Y

**Important note**  
In order to make more portable a process, the defined tasks should not contain references to a specific environment, such as an host or port when invoking URLs in web services.  
This goal can be reached by omitting the whole URL and use a relative URL instead.  
This semplification can be done only if the first fixed part of any URL \([http://host:port/webcontextofPlatform](http://host:port/webcontextofPlatform)\)  has been defined as an installation parameter in Activiti-Rest db.properties file, where the "baseUrl" property must be set with that value.  
In this way, every installation would have its own ad hoc absolute path and all processes would remain portable, since they would not contain any more absolute URLs.

## Example

| … baseUrl=[http://localhost:8180/platform/](http://localhost:8180/platform/) … |
| :--- |


value of "url" class property within a web service Service Task:

| executeJs?applicationId=XXX&appId=XXX&actionId=xxx&userId=:ADMIN |
| :--- |


**Important note**  
Do NOT use the notation ${VARNAME} in the definition of a web service: you have to use the notation :VARNAME instead.

---



