# Google SSO

4WS.Platform CE/EE are able to make use of Google+ SSO.  
User flow  
The Google SSO is provided through the G+ application platform, currently suggested as preferred way by Google.  
Two steps are involved:

* **authentication** 
* **single sign on process** 

If the user is not logged in with a Google account, the 4WS.Platform login page shows \(if enabled\) the G+ login button.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadi4ws.platform-integrationwithgoogleforwork/image05.png)

Pressing the red buttong, a pop-up shows asking for Google credentials:

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadi4ws.platform-integrationwithgoogleforwork/image03.png)

Once the correct credential are specified, pressing the "Sign in" button, a form appears asking the user for permission to access some profile data. To proceed, accept and give permissions \(this option will be stored in the user’s account profile for future logins\).  
After this step, Google services notify 4WS.Platform that the authentication process is passed. Now 4WS.Platform verifies if the user is present in the internal directory and loads all the associated permissions, as in the built-in login process.  
If the user is already logged in Google \(for example in GMail\), the Google login process is skipped, and the user is redirected to the 4ws.Platform menù or application with no additional steps.  
The user can log out from 4WS.Platform without logging out from the Google account. On the next login attempt, the credentials are requested again.  
Configuration  
To enable the Google SSO, in the web.xml enable the portal mode setting the following init param:

```js
&lt;init-param&gt;
  &lt;param-name&gt;portalLogin&lt;/param-name&gt;
  &lt;param-value&gt;true&lt;/param-value&gt;
&lt;/init-param&gt;
```

This configuration is no more required: the Google SSO login works also in non-portal mode.  
Then, the following parameters must be specified:

* **AUTH\_BOXES**  must contain the value AUTH\_BOX\_GOOGLE
* **SSO\_MANAGER\_CLASS**  must be equal to org.warp4ws.common.web.SSOGoogleServer to specify we want to use Google SSO.

Next step is to create a Google API Project \(or use the same project if 4WS.Platform is installed on Google Cloud Platform\), and a "Client ID for Web Applications", under the "Credential" section. You must specify the exact URLs for origin and callback, in the form of

&lt;YOUR\_APP\_URL&gt;, for example [http://platform.mydomain.com](http://platform.mydomain.com), for origin  
&lt;YOUR\_APP\_URL&gt;/oauth2callback, for callback

Having the generated client secret and client id, you must specify this values in 4WS.Platform:

* AUTH\_GOOGLE\_CLIENT\_ID: Google client Id, like NNNNNNNNNN.apps.googleusercontent.com
* AUTH\_GOOGLE\_CLIENT\_SECRET: the secret 
* AUTH\_GOOGLE\_USER\_FORM: \(opt\) this parameter specifies how to extraxt the 4ws.Platform user id from the Google mail of the user. For example {u}@mydomain.com \(in this case the user id in 4WS.Platform must be equal to the part of the Google email before the domain\), or simply {u} \(in this case the user id in 4WS.Platform must be equal to the full Google email\), which is the default value.
* **AUTH\_GOOGLE\_USER\_SCOPES** : \(opt\) blank space separated list of scopes that the application needs to ask to the user to run correctly. See the complete list at [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes). This enables the client side authorization process that lets the application manage user’s data, not the Google Apps Domain.

Once the parameters are correctly specified and if the user name is in the 4WS.Platform internal DB, the SSO will work.

---



