# Additional server-side services

The integration between Alfresco and Platform does not finish with the exchange of metadata and documents.  
A very common customization carried out inside Alfresco is the development of web scripts. Web scripts can be easily invoked by Platform: GUI events can be listened by Platform and can invoke actions. A server-side javascript action can be linked to events and used to invoke web scripts.

This is an example of ** how to invoke an Alfresco Web Scripts**  from a server-side javascript:

```js
var success = utils.getAlfrescoWebScript(url, false, "GET", null);
```

Other examples are:

* Set ACL for a document

```js
service/createFileACLs?applicationId=...&amp;appId=...&amp;uuid=... &amp;roleId=...&amp;canRead=..&amp; canAdd=&amp; canEdit=...&amp; canDelete=...
```

Parameters:

* **Application ID** 
* **AppId** 
* **Folder/Document UUID**  \(Unique Identification\)
* **Platform Role ID** 
* **CanRead** : Y/N value that indicates wether the file/folder is  **visible**  for the specified role
* **CanAdd** : Y/N value that indicates wether the specified role  **can add**  files/subfolders in the selected folder
* **CanEdit** : Y/N value that indicates wether the file is  **editable**  by the specified role
* **CanDelete** : Y/N value that indicates wether the file/folder is  **deletable**  by the specified role **Response** : JSON object with  **true/falce success property** .

* Inherit ACL settings for the specified file/folder

```js
service/setInheritPermission?applicationId=...&amp;appId=...&amp;id=...&amp;enabled=...
```

Parameters:

* **Application ID** 
* **Folder/Document UUID**  \(Unique Identification\)
* **Enabled** : Y/N value to  **inherit ACL settings**  from the parent folder

* Changes metadata for a document \(one or more metadata\)
  **Note** : This method must be called via  **POST request** 

```js
service/setMetadataForOneFile?applicationId=...&amp;appId=..
```

Parameters:

* **Application ID** 
* **AppID** 
* In the  **request body**  there must be a JSON string with all the metadata for the record. Usually it is the stringified VO with some modified values, for example

```js
/* .. previous code .. 
I expect to have a vo here, for example

vo['name'] = 'John';
vo['surname'] = 'Dooe';
*/

vo['surname'] = 'Doe';  /* Here I modify the value of a property */

vo = JSON.stringify(vo); /* Stringified object */

var result = .... /* Request, pass vo as the body parameter */
```

* Changes a single metadata of a document

```js
service/setAttributeValue?applicationId=...&amp;appId=..&amp;attributeName=...&amp;attributeValue=...&amp;uuid=...
```

Parameters:

* **Application ID** 
* **AppID** 
* **Folder/Document UUID**  \(Unique Identification\)
* **AttributeName** : Name of the attribute to change
* **AttributeValue** : The new value for the specified attribute

* Programmatically downloads a file

```js
service/downloadfile?applicationId=...&amp;appId=..&amp; name=...&amp;id=...&amp; path=..&amp;log=...&amp;userId=...
```

Parameters:

* **Application ID** 
* **AppID** 
* **Name** : Filename of the file to download
* **Folder/Document UUID**  \(Unique Identification\)
* **Path** : Optional parameter used to  **execute a web call to Alfresco** 
* **Log** : true/false optional parameter used to  **store the download event**  in the  **CON60\_LOGS**  DB table
* **UserID** : true/false optional parameter used in the  **CON60\_LOGS**  DB table

In case the Web Script returned a JSON response, this can be sent back to the Platform UI through this final instruction:

```js
utils.setReturnValue(success);
```

Server-side javascript actions can be invoked starting from the Platform GUI in different ways:

* by linking that action to a custom button
* by linking that action to a loading/saving event in grids/forms
* by linking that action to a generic event.

A common scenario is when a server-side javascript action must be manually invoked from some point in the GUI. This is an example of how to do that:

```js
var result = new SyncRequest().send(contextPath + '/executeJs?actionId=...&amp;applicationId=' + applicationId + '&amp;id=' + vo.id, 'GET', null, 'application/json');

var obj = JSON.parse(result);
```

In this example, a specific server-side action is invoked \(through the actionId parameter\) and a parameter named id is also passed to the server, filled with a corresponding id attribute contained in the vo. Some kind of result, expressed in JSON format is also sent back.

---



