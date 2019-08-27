# Global parameters

Global parameters are accessible starting from the menu **Administration** -&gt; **Global Parameters**. Once opened it, a list of parameters can be defined.  
Some parameters are global only, i.e. applied to all applications defined in the environment, others can be redefined at application level; some others can be defined at application level only.  
The followings are global parameters, grouped per topic:

**4WS.Platform** - generic parameters, not linked to a specific module

**Activiti** - parameters related to the BPM module

* Base Rest URL
* Base Designer URL

**Alfresco - **parameters related to the ECM module

* Admin Password when connecting to Alfresco Server
* Admin Username when connecting to Alfresco Server
* URL when connecting to Alfresco Server
* sync user in Alfresco
* sync roles in Alfresco
* sync user roles in Alfresco

**App Analysis** - parameters related to the tool used to perform an assessment of the app

**Docx conversion** - parameters related to the services which allow to convert documents to the PDF format

**Export** - parameters related to the xls export module

**File upload **- parameters used to manage the file upload 



**Google - **parameters used to integrate the application with the Google Cloud Platform and the Google Domain \(GSuite\)

* Apps domain admin user for Google Service Account
* Service Account Email
* Service Account Key
* Google SSO
* Client id for web application
* Client secret for web application
* Format to extract username from email
* Apps domain to use for synchronization
* Apps customer id used for sync
* Google Sync
* User query for synchronization
* Format to extract username from email for sync
* Fields extracted from user accounts
* Type of fields extracted from user accounts for sync
* Fields extracted from group information for sync
* Type of fields extracted from group information for sync
* Sync: company, site to use when creating records from Google

**LDAP - **parameters used to integrate the app with an LDAP server, like MS Active Directory

* Autocreate user from LDAP
* Autoupdate user from LDAP
* Autoassign current role to new LDAP user
* checking enabled
* port
* server
* account auth format
* Sync: company, site to use when creating records from LDAP
* LDAP synchronization
* Password to use when connecting to LDAP
* Username to use when connecting to LDAP
* Base LDAP path when searching for users
* \(optional\) Users LDAP filter
* \(optional\) fields to manage in LDAP users
* \(optional\) field types to manage in LDAP users
* \(optional\) LDAP attribute for user id
* Base LDAP path when searching from groups
* \(optional\) Groups LDAP filter
* \(optional\) fields to manage in LDAP groups
* \(optional\) field types to manage in LDAP groups
* \(optional\) LDAP attribute for group id

**Email notification system**

* SMTP host when sending email
* \(optional\) SMTP port when sending email
* \(optional\) SMTP protocol when sending email
* \(optional\) SMTP username when sending email
* \(optional\) SMTP password when sending email
* \(optional\) Use TLS when sending email: E/F

**Mobile** - parameters used to integrate a mobile app with Firebase notification system

**Password** - parameters used to define the password policy

* Password regular expression: you can define a regular expression for users password
* Password: number of days to use for the password expiration
* Password: number of erroneous login attempts

**Permissions - **parameters used to define the authentication process

* Login controls to hide
* Encript all passwords
* Authentication chain
* Authentication types in login dialog
* Destination for the sync process groups/users
* LDAP sync also groups
* Synchronization
* Logical delete of users before sync
* Company, site couples to use when creating records
* Fields to manage in 4WS users table
* Fields to manage in 4WS groups table
* LDAP user name/surname for email format
* SSO
* URL server
* Manager class name
* Parameter name id user SSO
* Parameter name token SSO

**Redis** - parameters used to manage the integration with a shared cache for user sessions, based on Redis

* Server host name - required in case of a fixed Redis server
* Server host port - required in case of a fixed Redis server
* Instance name - in case of auto creation/destroy of the Google service based on Redis, this value represents the name used to identify the cache name in the Redis server
* Region name - in case of auto creation/destroy of the Google service based on Redis, this value represents the region name where the Redis instance will be created in the Google Cloud project
* Rest comand to create an instance  - in case of auto creation/destroy of the Google service based on Redis, this is an optional value, espressed in JSON format, related to the BODY content to send to GPC to create the instance
* Interval when Redis is not working - in case of auto creation/destroy of the Google service based on Redis, this optional value represents the interval \[0-24\] expressed with hours, where the service is not operating
* VPC name - in case of auto creation/destroy of the Google service based on Redis, this value represents the VPN name used by Redis and by the Compute Engine instances where Platform is running

**Scheduler - **parameters used by the scheduler module

* "From email address" when sending email from Scheduler
* * Collaboration
* URL 4WSMonitor
* Show role id
* Show site id in users/user roles
* show/edit site id in user detail
* day number of log

**UI** - parameters used by the UI

* Disable GoogleMaps libs loading
* Hide Platform logo
* Max number of exportable row in grid
* Enable users
* Access unavailable message
* Duplicate data per company
* Application activation key path





---



