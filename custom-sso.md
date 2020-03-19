# Custom SSO

Platform supports external SSO servers, with a variety of different solutions:

* support for Google SSO server
* support for Tibbr SSO server
* support for a generic SSO server, where the auth checking is performed in some other way

In the next sections each scenario is reported.

---

#### Support for Google SSO server

This scenario is described in another dedicated section.

---

#### Support for Tibbr SSO server

This SSO server provides a web service for checking out the correct user authentication, working with an URL where the auth token + user id are passed as request parameters.

These are the required steps:

* the global parameter named "**SSO manager class name**" \(having code SSO\_MANAGER\_CLASS\) must be filled with the value “**org.warp4ws.common.web.SSOTibbrServer**” 
* the global parameter named "**SSO: URL Server**" \(SSO\_\_AU\_TH\_URL\) must be filled with the URL where the SSO server web service is available
* optionally, you can also define the global parameter named "**SSO: parameter name for user id**" \(SSO\_USER\_ID\), in case the SSL server you want to connect to will pass forward a HTTP request parameter containing the user id expressed with a particular parameter name
* optionally, you can also define the global parameter named "**SSO: parameter for SSO token**" \(SSO\_\_AU\_TH\_TOKEN\), in case the SSL server you want to connect to will pass forward a HTTP request parameter containing the token expressed with a particular parameter name.

---

#### Support for a generic SSO server

In case of very complex scenarios, you can always define your own server-side javascript class and manage the communication with the SSO server through it.

These are the required steps:

* the global parameter named "**SSO manager class name**" \(having code SSO\_MANAGER\_CLASS\) must be filled with the value "**org.warp4ws.common.web.SSOJsActionServer**"
* he global parameter is the parameter named "**SSO: list of app ids + actions ids, used by the custom SSSO server**" \(having name SSO\_\_JS\_\_ACTION\_IDS\) must be filled with a list of couples separated by a ; \(semicolon\). Each app id and action id are separated by a , \(comma\)

Example: MYAPP1,123;MYAPP2,456

where MYAPP1 is the app id for a Platform application where there is a server-side js action having id 123

where MYAPP2 is the app id for a Platform application where there is a server-side js action having id 456

The server-side js action wil receive as input the "reqParams" and "reqHeaders" js objects containing all request/header parameters passed forward by an external link to access Platform. The external link should include any data needed to check out the user in the SSO server \(e.g. token, userid, etc.\)

Next, the action can  use this data to contact the SSO server and manage the authentication. The action must always return one of the following outcomes:

**Successful authentication**

```js
 { "success": true, "username": "xxx" }
```

Note that the action must always get back the username, since the external link could pass a malware username, instead of the correct authenticated username, so it is up to the action/SSO server to figure out which is the right user to authenticate and use since then.

**Failed authentication**

```js
 { "success": false }
```

An example of external URL which can be invoked to logon into a Platform app, which will use the SSO behind the scenes is:

```
http://host/webcontext/4ws/index_app.jsp?applicationId=...&appTitle=...&autoLogin=true&ssoToken=...&password=UNDEFINED&username=UNDEFINED
```



