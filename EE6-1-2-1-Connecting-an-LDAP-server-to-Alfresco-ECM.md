# Connecting an LDAP server to Alfresco ECM

When using the Alfresco ECM together with Platform, an LDAP server is required and must be configured in order to be used both with Platform and Alfresco.  
In case an LDAP server is not available in an organization, an embedded LDAP server included with Platform can be activated and used by Alfresco. This sub-case is reported in another section.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/identitymanagementusermanual/image12.png)

These are the steps needed to activate the embedded LDAP server and to configure Alfresco to use it.  
The required settings must be defined in the "Application parameters" window, which can be accessed starting from the App Designer -&gt; Application detail.  
These are the settings to define:

Alfresco: admin username = …  
Alfresco: admin password = …  
Alfresco: server URL = esempio: [http://host:porta/alfresco](http://host:porta/alfresco)  
Alfresco: xml model name = example: xxxModel.xml  
Alfresco: xml model UUID = example: c1067705-5ac6-495b-b6ca-1d517f7bd7b3  
Alfresco: xml model namespace name = example: [http://www.sinesy.it/model/content/1.0](http://www.sinesy.it/model/content/1.0)  
Alfresco: xml model namespace prefix = example: demo1

Moreover, the  **alfresco-global.properties**  file must be changed, in order to use the righr LDAP server; this file is stored in the  **tomcat/shared/classes**  folder; the following instructions must be added to connect to the LDAP server, in order to \(i\) enable the use of the LDAP and to \(ii\) import \(sync\) users from the LDAP server.

The default authentication chain

`authentication.chain=alfrescoNtlm1:alfrescoNtlm,ldap1:ldap-ad ntlm.authentication.sso.enabled=false `

To configure external authentication subsystems see: http://wiki.alfresco.com/wiki/Alfresco\_Authentication\_Subsystems

`ldap.authentication.active=true ldap.authentication.allowGuestLogin=false ldap.authentication.userNameFormat=%s @dominio ldap.authentication.java.naming.provider.url=ldap:// host:porta ldap.authentication.defaultAdministratorUserNames=Administrator,alfresco ldap.synchronization.active=true ldap.synchronization.synchronizeChangesOnly=false ldap.synchronization.allowDeletions=true # ogni ora ldap.synchronization.import.cron=0 0 ldap.synchronization.java.naming.security.principal= xxx ldap.synchronization.java.naming.security.credentials= yyy ldap.synchronization.groupSearchBase= dc=…. ldap.synchronization.userSearchBase= dc=… ldap.synchronization.modifyTimestampAttributeName=whenChanged ldap.synchronization.userEmailAttributeName= userPrincipalName # The query to select all objects that represent the users to import. ldap.synchronization.personQuery=(&(objectClass= user )(objectCategory= person )(!(userAccountControl:1.2.840.113556.1.4.803:=2))) # per fare la sincronizzazione full ogni volta ldap.synchronization.userIdAttributeName= sAMAccountName ldap.synchronization.userFirstNameAttributeName= givenName ldap.synchronization.userLastNameAttributeName= sn`

Note: the values reported in bold are an example: they do not represent the right value in any scanario.

---



