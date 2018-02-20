# Users and groups synchronization

In the previous paragraph the SSO feature is described. In particular the users must be present in the 4WS.Platform internal DB to make the SSO work. You can create manually the users, or in case of EE, you can set up the directory synchronization.  
In order to give 4WS.Platform the permission to read Google Directory users and groups, a service account user must be created in the Google Developer Console.  
In the credential section of the project, create a service account and download the .p12 file containing the encrypted password.  
Then go to the Google Apps for Work admin console, choose Security → Advanced Settings → Manage API client access. Insert in the client id fiels the client id generated above and the following scopes, comma separated:

```js
https://www.googleapis.com/auth/admin.directory.group.member.readonly
https://www.googleapis.com/auth/admin.directory.group.readonly
https://www.googleapis.com/auth/admin.directory.user.readonly
```

Now in 4WS.Platform the following parameters must be specified \(for all applications or for single applications\):

* **GOOGLE\_SERVACC\_ADMIN\_USER** : the email of a user in the Google Apps domain with Super Admin privileges
* **GOOGLE\_SERVACC\_EMAIL** : the service account e-mail, in the form of xxxxxxxxx-xxxxxxxxxxxx@developer.gserviceaccount.com
* **GOOGLE\_SERVACC\_KEY** : the p12 public key, BASE64 encoded. This key can be downloaded from the API console, when creating the service account. You must encode the key in BASE64 by yourself.
* **SYNC\_GOOGLE\_DOMAIN** : the Google Apps domain name \(for example mygoogleappsdomain.com\) from which users and groups must be read. In case of multidomain Google Apps, only the objects of this domain are read. This parameter takes precedence over the next one, customer id.
* **SYNC\_GOOGLE\_CUSTOMER\_ID** : in case of multidomain Google Apps, specify the customer id of the Google Apps installation.
* **SYNC\_GOOGLE\_USER\_QUERY** : \(opt\) a filter query for users list, as specified in the documentation: [https://developers.google.com/admin-sdk/directory/v1/reference/users/list](https://developers.google.com/admin-sdk/directory/v1/reference/users/list). For example: eMail:a\* to extract only users whose e-mail address starts with "a".
* **SYNC\_GOOGLE\_USER\_FORM** : \(opt\) specify this to convert the user email in 4WS.Platform user id. It works like the similar parameter user for SSO. In case of multidomain pay attention that only one parameter can be specified. Default value is {u}.
* **SYNC\_GOOGLE\_USER\_FIELDS** : user fields that will be mapped in the destination fields. The default value is "primaryEmail;description;;;". The available fields name are specified in Google API documentation \([https://developers.google.com/admin-sdk/directory/v1/reference/users\#resource](https://developers.google.com/admin-sdk/directory/v1/reference/users#resource). Use the first level attributes, nested attributes are not supported\) and the following custom values: description, name, surname.
* **SYNC\_GOOGLE\_USER\_FIELD\_TYPES** : user field types used to extract the date. The default value is "UserFormatType;;;;", where the first type indicates that the first field is the user name, in string format. The default are string fields.
* **SYNC\_GOOGLE\_GROUP\_FIELDS** : group fields that will be mapped in the destination fields. The default value is "name;description".
* **SYNC\_GOOGLE\_GROUP\_FIELD\_TYPES** : user field types used to extract the date. The default value is ";", indicating two string fields.

Finally the synchronization can be fired pointing the browser to http\[s\]://&lt;platform url&gt;/secursync

---



