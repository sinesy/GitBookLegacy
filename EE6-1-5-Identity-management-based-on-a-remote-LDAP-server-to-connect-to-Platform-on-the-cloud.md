# Identity management based on a remote LDAP server to connect to Platform on the cloud

This scenario represents the case where the LDAP server is located inside the organization LAN whereas Platform has been installed in cloud.  
Consequently:  
the  **LDAP must be accessible though the Internet** , so that Platform can communicate with it; typically, a VPN is used to make them communicate with each other  
users must be extracted by the LDAP server and loaded into the Platform database

Platform must be configured in order to:  
import users from the LDAP on a regular basis  
access to the LDAP server remotelly, in order to authenticate users

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/identitymanagementusermanual/image09.png)

---



