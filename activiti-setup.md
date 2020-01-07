# Activiti Setup

Platform has been tested with Activiti 5 version, which is composed of 2 distinct web applications:

* Activiti Explorer, used to graphically define business processes \(workflows\); this web application is embedded into the Platform App Designer
* Activiti Rest, which is the engine, able to execute any number of processed; this web app does not provide any UI, but it provides a Rest API used by Platform to manage processes.

In the following section is described the manual steps needed to correctly setup such integration.

* create an empty database schema which will be used by Activiti to store its content. It is recommended to re-use the same schema used by Platform as repository
* download Activiti Explorer and Activiti Rest, release 5 from the following link: [https://github.com/Activiti/Activiti/releases/download/activiti-5.22.0/activiti-5.22.0.zip](https://github.com/Activiti/Activiti/releases/download/activiti-5.22.0/activiti-5.22.0.zip)
* decompress the downloaded zip file and find the 2 .war files, related to Activiti Explorer and Activiti Rest
* rename the .war into .zip file and decompress the 2 .war files and remove the previous .war file, not any more needed; be sure that the unzip process has created the corresponding subfolders: activiti-explorer and activiti-rest
* once decompressed the 2 files, a few configuration files must be modified, in order to correctly set up the database connection and LDAP connection; this task is described in detail in the following section
* prepare an ad hoc Tomcat 9, distinct from the one used by Platform and change the bin/catalina.sh file in order to set the JAVA\_HOME variable to your JDK 11 path
* copy the 2 subfolders activiti-explorer and activiti-rest into the webapps Tomcat's subfolder
* copy the JDBC driver used by Platform into the lib Tomcat's subfolder
* copy the PlatformActiviti.jar file to the lib Tomcat's subfolder
* copy the following the files to the lib Tomcat's subfolder: jaxb-api-2.4.0-b180830.0359.jar  jaxb-impl-2.4.0-b180830.0438.jar  jaxb-impl.jar

Now the setup is completed and Activiti ready to be used.



### Configuring Activiti and Platform

Both Activiti web applications and Platform must be setup in order to work together. In the following sub-sections all steps neeeded are reported.

#### Configuration files for Activiti Explorer

#### WEB-INF/classes/db.properties

```
platform.url=http://localhost:platformport/platformwebcontext
sql=select USER_CODE_ID FROM PRM01_USERS WHERE STATUS='E'
db=mysql
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://dbhostname:3306/databasename
jdbc.username=dbusername
jdbc.password=dbpassword
```

This file is used to connect Activiti Explorer to its database schema



activiti-standalone-context.xml

activiti-ui-context.xml

applicationContext.xml



Configuration files for Activiti Explorer



Configuration in Platform App Designer



