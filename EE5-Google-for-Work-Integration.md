# Google for Work Integration

This document covers the integration of 4WS.Platform, in particular the Enterprise Edition \(EE\) but also in the Community Edition \(CE\), with the Google for Work products, namely:  
Google Apps for Work  
Google Cloud Platform  
It is possible to integrate in different ways, depending on the goals you want to achieve:

* **client authentication with Google SSO** : in this way the user can authenticate through Google SSO that acts as a federated authentication server. In general the user must already be present in the 4WS.Platform internal authorization system in order to pass the login process. This feature is available in CE and EE versions.
* **client side authorization** : if the application has the need to access Google for Work APIs \(for example GMail, Contacts, Calendar, Drive, but also Google Cloud Platform resources\) that are owned by the user, you can use this kind of authorization process, that is automatically enabled when Google SSO is correctly configured. This flavor of authorization is ideal for the Google free account \(i.e. your GMail free account\).
* **server side authorization** : if the application needs to access domain wide data \(documents, calendars or other resources not belonging to the logged in user\), a service account can be used. This means that you must create a service account in the Google API/Cloud Console and put it in your Google Apps Admin console and enable specific scopes.

---



