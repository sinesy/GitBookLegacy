# Identity management based on Google SSO

This section is obsolete. Please refer to this document.  
Google Authentication can be connected to Platform, in case Google users \(emails\) are used to authenticate into Platform.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/identitymanagementusermanual/image04.png)

This authentication mode can be coupled to the "portal mode" operation set in Platform. In order to activate it, change the web.xml Platform file and add these lines of code:

`JerseyFilter … portalLogin true`

Once restarted Platform, the Platform home page would ask for the user credentials and only after logging on, the list of allowed applications are showed.  
In order to show the Google authentication in the first login dialog, the Google SSO server must be connected to Platform, though the client\_id private key defined inside the Google Domain.  
When the adimistrative settings have been completed on the Google domain side, the App Designer can be used to set the additional parameters required.  
The required settings must be defined in the "Application parameters" window, which can be accessed starting from the App Designer -&gt; Application detail.  
These are the settings to define:

AUTH\_BOXES = AUTH\_BOX\_GOOGLE,AUTH\_BOX\_DEFAULT  
Google Client id for web application = …  
Google Client secret for web application = …  
Format to extract the user from the Google email = example: {u}@sinesy.it  
Admin user of Google domain = x@y  
Email Google for service account = …  
Google key for service account = a p12 encoded key in base64  
Sources for sync process to use for groups/users = GOOGLE  
Class name for SSO Google = org.warp4ws.common.web.SSOGoogleServer  
Sync Google Client id = …  
Sync Google Client secret = …  
Google Apps domain to use when synchronizing = …

---



