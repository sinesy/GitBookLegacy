# Shared contacts synchronizations

4WS.Platform has a DB table that can contain shared contacts and can be inquired by functionalities \(grids, lookups and so on\). The table can be filled from different sources, one of which is Google Apps for Work. In particular two sources are synced:

* the Google Apps Directory, which contains the contacts of the Google Apps Domian, i.e. all people in the same domain.
* the Google Domain GAL \(Global Access List\), which contains common contacts that do not belong to the Google Domain, i.e. contacts of general interest.

  **NOTE** : The Google Apps Domain is only a source of information, not a destination. This means that the Google Apps Domain in not updated, only read.  
  To synchronize the table, each application must be configured. In case of Google Apps as source, the following parameters must be specified:

* GOOGLE\_SERVACC\_ADMIN\_USER: the account of an admin user

* GOOGLE\_SERVACC\_EMAIL: the service account email address
* GOOGLE\_SERVACC\_KEY: the service account p12 public key, Base64 encoded
* CONTACTS\_SOURCE\_GOOGLE\_DOMAIN: must contain GOOGLE keyword.

To call the synchronization method, two ways can be used:

* call the web method sharedcontactssync with a GET call on the 4WS.Platform server, for example

```js
GET http://&lt;server&gt;/sharedcontactssync
```

* use the server side Javascript call from an action:

```js
utils.sharedContatctsSync()
```

---



