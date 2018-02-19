# Identity management based on an embedded LDAP server used by Alfresco or Activiti

In case an LDAP server is not available, Alfresco and Activiti can be connected to an embedded LDAP server provided by Platform. These two products would then authenticate users on it, which is based on the Platform local users defined in the Platform database.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/identitymanagementusermanual/image05.png)

In order to activate the embedded LDAP server provided by Platform, a few settings must be defined in the "Application parameters" window, which can be accessed starting from the App Designer -&gt; Application detail.  
These are the settings to define:

EMBEDDED\_LDAP\_SERVER\_PORT = example: 3389  
EMBEDDED\_LDAP\_SERVER\_USERNAME = example:ADMIN  
EMBEDDED\_LDAP\_SERVER\_PASSWORD = example: admin

Finally, Activiti and/or Alfresco must be configured in order to communicate to the embedded LDAP server; the baseDN to set must be:  **dc=com**  and the users must be identified by  **cn=** …

**Activiti Rest configuration:**

open the file  **webapps/activiti-rest/WEB-INF/classes/activiti-context.xml**  and add the following lines:

```
class=”it.sinesy.activiti.util.Utils”> <property… “(&(objectClass=person)(cn={0}))” />
```

**Activiti Explorer configuration:**

Open the file  **webapps/activiti-explorer/WEB-INF/activiti-standalone-context.xml ** and add the following lines:

```
class=”it.sinesy.activiti.util.Utils”> “cn=ADMIN,dc=com” /> “(&(objectClass=person)(cn={0}))” /> -->
```

**Alfresco configuration:**

Open the file  **tomcat/shared/classes/alfresco-global.properties**  and add the following lines:

The default authentication chain 

`authentication.chain= alfrescoNtlm1:alfrescoNtlm,ldap1:ldap-ad ntlm.authentication.sso.enabled= false `

To configure external authentication subsystems see: http://wiki.alfresco.com/wiki/Alfresco\_Authentication\_Subsystems 

`ldap.authentication.active= true ldap.authentication.allowGuestLogin= false ldap.authentication.userNameFormat= cn=%s,dc=com ldap.authentication.java.naming.provider.url= ldap://localhost:…. ldap.authentication.defaultAdministratorUserNames= Administrator,alfresco ldap.synchronization.active= true ldap.synchronization.synchronizeChangesOnly= false ldap.synchronization.allowDeletions= true # ogni ora ldap.synchronization.import.cron=0 0 ldap.synchronization.java.naming.security.principal= cn=ADMIN,dc=com ldap.synchronization.java.naming.security.credentials=… ldap.synchronization.groupSearchBase= dc=com ldap.synchronization.userSearchBase= dc=com ldap.synchronization.modifyTimestampAttributeName= whenChanged ldap.synchronization.userEmailAttributeName= cn # The query to select all objects that represent the users to import. ldap.synchronization.personQuery= (objectClass=person) # per fare la sincronizzazione full ogni volta ldap.synchronization.userIdAttributeName= cn ldap.synchronization.userFirstNameAttributeName= sn ldap.synchronization.userLastNameAttributeName= sn`

