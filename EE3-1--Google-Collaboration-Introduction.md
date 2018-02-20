# Introduction

GSuite module is composed of a bunch of features, both on the server-side and on the client-side, used to communicate with Google Apps:  
GMail integration  
Calendar integration  
GDrive integration

These Google services can be integrated in different ways, according to the layer:  
when connecting these services with the Platform front-end, the Google SSO is exploited: once logging on Platform using the Google SSO, any Google service is automatically accessed and can be embedded with the rest of Platform UI; that means that  **the Google Apps front-end is directly embedded into Platform windows**  
when connecting these services with the server layer of Platform, the Google API is internally invoked by Platform, in order to communicate with these services in a variety of different ways, according to the service to invoke:  
GMail –  **email messages can be read and sent; GMail contacts can be retrieved**  
Calendar –  **events in calendar can be created, changed, deleted**  
GDrive –  **folders can be created, changed, deleted; folder content can be read**

When using the Google SSO on the client-side, a specific user account is used and the content provided by Google depends on it.  
When using the Google API on the server-side, retrieved data can be filtered according to the user: the user currently connected or a "generic" account, used to manage data and documents for all users.

In both cases, a Google Domain is required in order to setup the environment.  
In the first case, many Google accounts are needed, one for each user.  
In the latter case, a single account could be used for all Platform users, for instance to manage documents stored in GDrive independently of the current connected user.

---



