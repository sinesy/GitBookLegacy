# Google OAuth2

4WS.Platoform provides methods to get Google OAuth2 credentials based on a Google Developer Console service account.  
As already explained above, it is necessary di create a service account in the cloud project where 4WS.Platform is installed or in the project target of our Google API requests.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadi4ws.platform-integrationwithgoogleforwork/image04.png)

First of all, go to the "Credentials" section and "Create a new Client Id". Choose "Service Account" and then "Generate new P12 key". This will cause the download of a file with extension .p12.  
Then this file must be base64 encoded in order to store it in the parameters tables \(CON07 or CON44\) of 4ws.Platform. In Linux/OSX environments this can be done in the following way:  
openssl base64 -in &lt;orig file&gt;.p12 -out &lt;orig file&gt;.p12.base64  
After this, the "Email Address" above and the base64 encoded p12 key must be saved in 4WS.Platform.  
If the project target of the Google API requests is the current cloud project, save them in the default Google parameters:

* Google Service Account Email – GOOGLE\_SERVACC\_EMAIL
* Google Service Account Key \(p12 key Base64 encoded\) – GOOGLE\_SERVACC\_KEY

If the project target of requests is antoher project, it is better to specify the same parameters under the custom section, with a signicative suffix in upper case:

* GOOGLE_SERVACC\_EMAIL_
* GOOGLE_SERVACC\_KEY_

For example:

* GOOGLE\_SERVACC\_EMAIL\_MYGOOGLEPROJECT
* GOOGLE\_SERVACC\_KEY\_MYGOOGLEPROJECT

The second step is to enable the APIs we want to call, going in the "APIs" section of the projects. For example if we want to call Cloud SQL API, enable "Google Cloud SQL API" in this section. This step is fundamental, instead we can get an authorization error.  
Now that the service account credetianls are in place, it is possible to call the Bean methods in GoogleOAuth2Bean:

```js
public Credential getCredential(ServerCommand sc, String serviceAccountEmail, String privateKeyString, String[] scopes);

public String getAccessToken(ServerCommand sc, String serviceAccountEmail, String privateKeyString, String[] scopes) throws Exception;
```

More frequently, the JS utils wrapper will be used from 4WS.Platform designer.  


## Get the access token for required scopes

###  To get the access token for the current Cloud Project

#### Syntax

```js
utils.getGoogleOAuth2AccessToken(scopes)
```

#### Details

**scopes**  – a list of strings containing the API scopes for the request. Every API has its own scopes, see more at [https://developers.google.com/oauthplayground/](https://developers.google.com/oauthplayground/).

### To get the access token for required scopes, for a specific Cloud Project

#### Syntax

```js
utils.getGoogleOAuth2AccessToken(projectId,scopes)
```

#### Details

**projectId**  – the project ID of the target project. Must match in UPPER CASE with the suffix of the parameters stored as explained above.  
 **scopes**  – a list of strings containing the API scopes for the request. Every API has its own scopes, see more at [https://developers.google.com/oauthplayground/](https://developers.google.com/oauthplayground/).

What can I do with the access token?  
When the access token is generated, HTTP requests to Google APIs are possible.  
For example to enquiry Google Cloud SQL see:

* [https://cloud.google.com/sql/docs/admin-api/index](https://cloud.google.com/sql/docs/admin-api/index)
* [https://cloud.google.com/sql/docs/admin-api/v1beta4/](https://cloud.google.com/sql/docs/admin-api/v1beta4/)

If we want to get Cloud SQL instance information we can create a server side JS action like this:

```js
var accessToken = utils.getGoogleOAuth2AccessToken(
     "&lt;Google Developer Console Project ID&gt;",
     "https://www.googleapis.com/auth/sqlservice.admin");
```

and then make HTTP requests towards  
[https://www.googleapis.com/sql/v1beta4/projects/instances](https://www.googleapis.com/sql/v1beta4/projects/instances)  
with the following HTTP headers

```js
Authorization: Bearer &lt;GENERATED ACCESS TOKEN&gt;
Content-Type: application/json
```

The answer is a JSON containing the requested information, for example:

```js
{

 "kind": "sql#instance",
 "selfLink": "https://www.googleapis.com/sql/v1beta4/projects/&lt;ID&gt;/instances/&lt;INST NAME&gt;",
 "name": "&lt;INST NAME&gt;",
 "etag": "\"t-4nX9ZybnnnnzzmT9atE_WwaU/OA\"",
 "project": "&lt;PROJ ID&gt;",
 "state": "RUNNABLE",
 "databaseVersion": "MYSQL_5_5",
 "region": "europe-west1",
 "currentDiskSize": "589145557",
 "maxDiskSize": "268435456000",
 "settings": {
  "kind": "sql#settings",
  "settingsVersion": "8",
  "authorizedGaeApplications": [
  ],
  "tier": "D0",
  "backupConfiguration": {
   "kind": "sql#backupConfiguration",
   "startTime": "12:00",
   "enabled": true,
   "binaryLogEnabled": false
  },
. . .
```

---



