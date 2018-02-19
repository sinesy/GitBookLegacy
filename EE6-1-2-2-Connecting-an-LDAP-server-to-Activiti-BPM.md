When using the Activiti BPM together with Platform, an LDAP server is required and must be configured in order to be used both with Platform and Activiti.
In case an LDAP server is not available in an organization, an embedded LDAP server included with Platform can be activated and used by Activiti. This sub-case is reported in another section.



![](http://4wsplatform.org/wp-content/plugins../../uploads/media/identitymanagementusermanual/image10.png)
p>

After installing Platform and Activiti (i.e. 2 war files + tables creation + setting of the 2 files db.properties + web.xml + additional jar files to connect Activiti to Plaform), additional settings must be added in order to use the LDAP.

The required settings must be defined in the "Application parameters" window, which can be accessed starting from the App Designer -&gt; Application detail.
These are the settings to define:

Activiti Designer base URL = example: http://host:porta/
Activiti Rest base URL = example: http://hostinterno:tomcatport/


Once completed the previous steps, another Activiti file must be re-defined: the file  **activiti-explorer/WEB-INF/classes/activiti-standalone-context.xml** 
The following lines must be added within the bean having id = processEngineConfiguration

| …        …      &lt; **property name=&#8221;server&#8221; value=&#8221;ldap://host&#8221; /&gt;**                                       **&#8230;**     **class=&#8221;it.sinesy.activiti.util.Utils&#8221;&gt;**   |
| :--- |

As reported above, outside the bean having id = processEngineConfiguration, there are 3 other beans to set.

Important notes:
pay attention to the use of the  **&amp;**  symbol within the XML (for instance when definying the LDAP query ); the pattern  **&amp;**  must be used instead.
the value to set for queryUserByUserId must refer the username, otherwise the authentication will fail.
{0} represents the username; therefore, a possible value could be also {0}domain.com

In the application classpath (WEB-INF/classes of both Activiti web applications) additional classes must be included as well (Platform4WSGroupManagerFactory class and the ones referred by the first one).

Change the file  **WEB-INF/classes/activity-ui-context.xml** 
and add the following instructions within the bean having name = &#8220;explorerApp&#8221;:

|   admin  **1**      user    |
| :--- |


Note: the 1 value identifies the admin role used by Platform and must be included in the list of roles.
In fact, Activiti Explorer has two kind of roles: admin and basic, reported in the previous schema.


Open the file  **activiti-rest/WEB-INF/classes/activiti-context.xml** 

| …       &#8230;                         **ref=&#8221;platform4WSGroupManagerFactory&#8221;/&gt;**                    **class=&#8221;it.sinesy.activiti.util.Utils&#8221;&gt;**    &#8230; |
| :--- |


As reported above, outside the bean having id = processEngineConfiguration, 3 other beans must be defined.

Important notes:
pay attention to the use of the  **&amp;**  symbol within the XML (for instance when definying the LDAP query ); the pattern  **&amp;**  must be used instead.
the value to set for queryUserByUserId must refer the username, otherwise the authentication will fail.
{0} represents the username; therefore, a possible value could be also {0}domain.com
                

---


