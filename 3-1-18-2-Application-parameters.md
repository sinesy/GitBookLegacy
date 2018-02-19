# Application parameters

When opening the detail window of a new application, there are two folders available: one contains the settings for the selected application, the other the application parameters, which is an editable grid, where the user can add, change and delete common parameters.  
When saving parameters, these will be accessible from an application when the user will re-logon to the application.  
These parameters are used by specific functionalities of the interpreted application and they are reported in the following list:

* Google Maps

* Start Point Latitude

* Start Point Longitude
* Start Point Name

* Remote Server URL to use in case of 4WS.Platform used on Google App Engine and reports generated remotely in another server
* UI

* Top menubar

* First level menu height \(pixel\)
* Second level menu height \(pixel\)
* Filter button position \(LEFT/RIGHT\)
* Main UI
* Number of menu levels
* Flag to show/hide the menu filter \(true/false\)
* Status bar height \(pixel\)
* Top bar height \(pixel\)
* Menu tree width
* Show window icon \(Y/N\)
* Show menu icon \(Y/N\)
* Buttons menu
* autosize buttons
* width/height for buttons
* width/height for images
* number of columns to use for buttons layout
* round border radix for buttons

* Alfresco

* Alfresco: Admin Password when connecting to Alfresco Server

* Alfresco: Admin Username when connecting to Alfresco Server
* Alfresco: URL when connecting to Alfresco Server
* Alfresco: model file name when connecting to Alfresco Server

* Permissions

* Login controls to hide

* Authentication
* \(optional def. ‘4ws’\) Authentication chain
* \(optional def. true\) LDAP checking enabled
* \(optional def. 389\) LDAP port
* LDAP server
* LDAP account format \(e.g. {u}@domain\)
* Destinations for the sync process groups/users
* Sources for the sync process groups/users
* \(optional def. false\) Logical delete of users before sync
* \(optional def. tutte\) company/site couples to use when creating records
* \(optional\) fields to manage in 4WS users table
* \(optional\) fields to manage in 4WS groups table
* LDAP synchronization
* Password to use when connecting to LDAP
* Username to use when connecting to LDAP
* Base LDAP path when searching for users
* \(optional\) Users LDAP filter
* \(optional\) fields to manage in LDAP users
* \(optional\) field types to manage in LDAP users
* \(optional\) LDAP attribute for user id
* Base LDAP path when searching from groups
* \(optional\) Groups LDAP filter
* \(optional\) fields to manage in LDAP groups
* \(optional\) field types to manage in LDAP groups
* \(optional\) LDAP attribute for group id

* Scheduler

* "From email address" when sending email from Scheduler

* Email notification system
* SMTP host when sending email
* \(optional\) SMTP port when sending email
* \(optional\) SMTP protocol when sending email
* \(optional\) SMTP username when sending email
* \(optional\) SMTP password when sending email
* \(optional\) Use TLS when sending email: E/F

* Application Access

* Enable users

* \(optional\) Access Unavailable message

* Password management

* Password regular expression: you can define a regular expression for users password.

  ## Example

  Translation **:**

* matches a string of six or more characters;

* that contains at least one digit \(d is shorthand for \[0-9\]\);
* at least one lowercase character; and
* at least one uppercase character.

First, create a server side js action when defining the custom logic; this action receive in input the dataStoreId value \(in the reqParams input object\) and the current user and other user information \(contained in the userInfo input object\). You can use this information to decide which datasource to return back, through the setReturnValue\(\);Additional datasource management: it is possible to define a custom logic to figure out which additional datasource to use, according to the user. For instance, if you have a table reporting a which datasource to use for each user, you can define a server-side javascript action and use it to dynamically decide the additional datasource to use.Password: Password: number of days to use for the password expiration

* Password: number of erroneous login attempts
* Order of Grid Export: ordered list of types export for grids

* Example: XLS\|CSV \(;\)\|CSV \(,\)\|HTML\|PDF\|RTF\|XML \(small format\)\|XML \(large format\)

Second, report the action id just defined as the “Customize Datastore” application parameter.

## Example

```js
if (reqParams.dataStoreId==null || reqParams.dataStoreId==0 || reqParams.dataStoreId==-1) {
    utils.setReturnValue("");
}
else {
    var json = utils.executeQuery(
        "SELECT DATASTORE_ID FROM CON04_ADDITIONAL_DATASTORES WHERE DESCRIPTION IN "+
        "(SELECT COD_SOCIETA FROM SOCIETA WHERE USERCODE_ID=:USERNAME)",
        null,false,true,
        []
        );
    var list = eval("("+json+")");
    if (list.length==1) {
        utils.setReturnValue(list[0].datastoreId);
    }
    else {
        utils.setReturnValue("");
    }
}
```

---



