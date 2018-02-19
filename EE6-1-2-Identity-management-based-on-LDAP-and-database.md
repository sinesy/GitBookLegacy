Platform Enterprise Edition includes a synchronization module used to automatically import users stored in an LDAP server; this module must be configured in order to:
automatically start the process through the Platform Scheduler
import users from the LDAP server, based on specific filters defined through LDAP queries
In this scenario, users come from:
an LDAP server, used to manage the organization employees; users are then authenticated in the LDAP Server
the Platform local database, used to manage external users, not defined in the LDAP server, as for clients, suppliers, as so forth.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/identitymanagementusermanual/image13.png)
p>

This scenario involves the definition of an authentication chain, where both the LDAP and Platform authentication sub-system must be defined.


After the standard Platform installation, including the Platform database authentication, a second sub-system must be added, in order to define the LDAP authentication.

The required settings must be defined in the "Application parameters" window, which can be accessed starting from the App Designer -&gt; Application detail.
These are the settings to define:

LDAPxxx_AUTH_LDAP_ACTIVE = true
LDAPxxx_AUTH_LDAP_SERVER = ip LDAP server
LDAPxxx_AUTH_LDAP_PORT = porta LDAP server
LDAPxxx_AUTH_LDAP_USER_FORM = example: {u}@sinesy.it
LDAPxxx_AUTH_LDAP_GRPS_BASE = example: ou=xxx,dc=yyy,dc=zzz
LDAPxxx_AUTH_LDAP_USERNAME = username LDAP server
LDAPxxx_AUTH_LDAP_PASSWORD = password LDAP server
LDAPxxx_AUTH_LDAP_USERS_BASE = example: ou=xxx,dc=yyy,dc=zzz
LDAPxxx_AUTH_LDAP_USERS_FILTERS = example: (&amp;(objectClass=*)(cn=*utente*))
Sources related to a synchronization process for groups/users = LDAPxxx
Logical deleting of users before the sync process = true
Sorted list of authentication systems = LDAP;4WS

where xxx = 1,2,etc.
                

---


