# Automatic user and group provisioning

If the authentication is external from 4ws.Platform \(i.e. not based on internal DB structures\), for example is based on SSO or LDAP/AD, one option is to put in place the synchronization process, otherwise the automatic user and group provisioning can be used, as explained here.  
This option works as follows: after a proper initial setup, when a user attempts the login and the external authentication system returns a positive response among with other information, this information are used to create \(if it does not not already exist\) or update the user and possibly assign default groups to the user \( **only**  if the user is new\).  
Therefore two steps are required:

* setup a SSO or external authentication system like LDAP \(see doc\)
* setup the automatic provisioning as explained below

The parameters to setup for automatic provisioning are:  
 **AUTH\_AUTO\_CREATE\_USER** : true or false. If true, after successful authentication on the external system, create the user in the 4WS.Platform repository. Default: false. This parameter is available at installation level.  
 **AUTH\_AUTO\_UPDATE\_USER** : true or false. If true, after successful authentication on the external system, update the user in the 4WS.Platform repository. Default: false. This parameter is available at installation level.  
 **AUTH\_AUTO\_LINK\_USER\_ROLE** : specify a semicolon \(;\) separated list of role ids to automatically assign to the user after successful authentication  **only**  if the user does not exist and AUTH\_AUTO\_CREATE\_USER is true. This parameter is available at installation level \(in this case the roles are added for all available applications\) or at application level \(roles are added only for that application\).

---



