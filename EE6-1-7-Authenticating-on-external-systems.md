# Authenticating on external systems

4WS.Platform supports external/SSO/federated SSO authentication mechanisms, that hold usernames and passwords and let the credential to be stored in a central system, without replication. Anyway, to make 4WS.Platform work correctly the users and roles must be synchronized or provisioned.  
The following authentication providers are currently available:

* 4WS.Platform internal DB
* external LDAP or Active Directory
* Google SSO
* Tibbr SSO

**4WS.Platform authentication**  
The 4WS.Platform authentication works out of the box without further settings and is the default method. To add or use other systems, some steps are required. The authentication process works in chain on more systems: the first system that returns a positive authentication result wins and the login process goes on.  
To specify the chain a parameter must be filled:  
AUTH_CHAIN: semicolon \(;\) separated list of authentication system codes.  
For example a valid values isLDAP;4WS. First LDAP is checked then 4WS internal DB. In this way some user can log in even if the remote LDAP is not accessible for some reason.  
It is possibile to specify more than one authentication service of the same type, everyone with its own parameters, for example: LDAP1;LDAP2;LDAP3;4WS. See below to understand how to configure single LDAP sources.  
 **AUTH\_BOXES** : semicolon \(;\) separated list of authentication boxes. Lets the administrator to enable SSO on external systems \(like Google SSO\) on the login form.  
Possible values are:  
AUTH\_BOX\_GOOGLE: to add Google SSO button  
AUTH\_BOX\_DEFAULT: to show username and password fields \(and possibly company id and site id fields\).  
The Google Box is used to authenticate through Google SSO, while the default box let authenticate against 4WS.Platform DB, LDAP or AD and is not intended as a SSO system: credentials must be always specified.  
 **SSO\_MANAGER\_CLASS** : in case of SSO, specify the full name name of the managing class \(see below\).  
LDAP or Active Directory authentication  
To enable the LDAP authentication set the parameters:  
 **AUTH\_LDAP\_ACTIVE** : \(opt.\) true \(default\). The parameter is useful to disable the authentication against this source even for specific applications.  
 **AUTH\_LDAP\_SERVER** :\(required\) IP or server name od the LDAP/AD server.  
 **AUTH\_LDAP\_PORT** : \(opt.\) the port where the service is bound. Default 389.  
 **AUTH\_LDAP\_USER\_FORM** : \(opt.\) if the format of the login username is different from the one used in the LDAP/AD system, this parameter enables an automatic conversion. For example if the username id “john\_doe” and the LDAP id is “john\_doe@domain.local”, specifying {u}@domain.local the conversion is performed before submitting to LDAP the authentication request. If the LDAP id is “uid=john\_doe,dn=office,cn=domain”, use“uid={u},dn=office,cn=domain”. {u} is the place holder for the 4WS.Platform user name and is also the default value of the parameter. This parameter can be used also in thesynchronizationprocess.  
All this parameters are used for the default LDAP authentication source, called LDAP. To specify more than one LDAP source, name it LDAP1, LDAP2, etc…, the parameter must be specified as follow:  
LDAP1\_AUTH\_LDAP\_ACTIVE  
LDAP1\_AUTH\_LDAP\_SERVER  
LDAP1\_AUTH\_LDAP\_PORT  
LDAP1\_AUTH\_LDAP\_USER\_FORM  
LDAP2\_AUTH\_LDAP\_ACTIVE  
LDAP2\_AUTH\_LDAP\_SERVER  
LDAP2\_AUTH\_LDAP\_PORT  
LDAP2\_AUTH\_LDAP\_USER\_FORM  
using the source id followed by underscore \(_\) followed by the parameter name.

**Google SSO authentication**  
See the Google for Work documentation [here](/EE5-SSO.md).

**Tibbr SSO authentication**  
Specify the value “org.warp4ws.common.web.SSOTibbrServer” for theparameter SSO\_MANAGER\_CLASS.

---



