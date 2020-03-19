# Identity management based on LDAP and database

Platform Enterprise Edition includes a synchronization module used to automatically import users stored in an LDAP server; this module must be configured in order to:  
automatically start the process through the Platform Scheduler  
import users from the LDAP server, based on specific filters defined through LDAP queries  
In this scenario, users come from:  
an LDAP server, used to manage the organization employees; users are then authenticated in the LDAP Server  
the Platform local database, used to manage external users, not defined in the LDAP server, as for clients, suppliers, as so forth.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/identitymanagementusermanual/image13.png)

This scenario involves the definition of an authentication chain, where both the LDAP and Platform authentication sub-system must be defined.

After the standard Platform installation, including the Platform database authentication, a second sub-system must be added, in order to define the LDAP authentication.

The required settings must be defined in the "Application parameters" window, which can be accessed starting from the App Designer -&gt; Application detail.  
These are the settings to define:

LDAPxxx\_AUTH\_LDAP\_ACTIVE = true  
LDAPxxx\_AUTH\_LDAP\_SERVER = ip LDAP server  
LDAPxxx\_AUTH\_LDAP\_PORT = porta LDAP server  
LDAPxxx\_AUTH\_LDAP\_USER\_FORM = example: {u}@sinesy.it  
LDAPxxx\_AUTH\_LDAP\_GRPS\_BASE = example: ou=xxx,dc=yyy,dc=zzz  
LDAPxxx\_AUTH\_LDAP\_USERNAME = username LDAP server  
LDAPxxx\_AUTH\_LDAP\_PASSWORD = password LDAP server  
LDAPxxx\_AUTH\_LDAP\_USERS\_BASE = example: ou=xxx,dc=yyy,dc=zzz  
LDAPxxx\_AUTH\_LDAP\_USERS\_FILTERS = example: \(&\(objectClass=_\)\(cn=_utente\*\)\)  
Sources related to a synchronization process for groups/users = LDAPxxx  
Logical deleting of users before the sync process = true  
Sorted list of authentication systems = LDAP;4WS

where xxx = 1,2,etc.

---



