# Authenticating on external systems

4WS.Platform supports external/SSO/federated SSO authentication mechanisms, that hold usernames and passwords and let the credential to be stored in a central system, without replication. Anyway, to make 4WS.Platform work correctly the users and roles must be synchronized or provisioned.  
The following authentication providers are currently available:

* 4WS.Platform internal DB
* external LDAP or Active Directory
* Google SSO
* Custom SSO

**Tibbr SSO authentication**  
Specify the value “org.warp4ws.common.web.SSOTibbrServer” for theparameter SSO\_MANAGER\_CLASS.

---



