# LDAP support

The authentication task can be delegated to the default implementation provided with 4WS.Platform, based on a set of database tables or can be forwarded to an authentication chain, including the LDAP authentication to an external LDAP server.  
The LDAP module provided with the Enterprise Edition, can synchronize with and LDAP server to copy users and roles to the local tables, so that the authentication and roles definition are always up to date with the ones defined in the central LDAP server.  
In that case, users and roles cannot be modified within 4WS.Platform, if the come from the LDAP server. It is always possible to insert additional users and roles from 4WS.Platform, which will be editable.

---



