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
* copy the PlatformActiviti.jar file to WEB-INF/lib subfolder of both web applications 
* copy the following the files to the lib Tomcat's subfolder: jaxb-api-2.4.0-b180830.0359.jar
  jaxb-impl-2.4.0-b180830.0438.jar
  jaxb-impl.jar

Now the setup is completed and Activiti ready to be used.

**Note**: due to default security properties on Tomcat, escaped forward slashes \(%2F and %5C\) are not allowed by default \(400-result is returned\). This may have an impact on the deployment resources and their data-URL, as the URL can potentially contain escaped forward slashes.

When issues are experienced with unexpected 400-results, set the following system-property:

-Dorg.apache.tomcat.util.buf.UDecoder.ALLOW\_ENCODED\_SLASH=true.

---

### Configuring Activiti and Platform

Both Activiti web applications and Platform must be setup in order to work together. In the following sub-sections all steps neeeded are reported.

---

#### Configuration files for Activiti Explorer

Activiti Explorer uses a series of configuration files, described below.

#### WEB-INF/classes/db.properties

```
baseUrl=http://localhost:platformport/platformwebcontext
sql=select USER_CODE_ID FROM PRM01_USERS WHERE STATUS='E'
db=mysql
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://dbhostname:3306/databasename
jdbc.username=dbusername
jdbc.password=dbpassword
```

This file is used to connect Activiti Explorer to its database schema. Values to change are:

* platformport and platformwebcontext, related to the settings of the other Tomcat, the one used by Platform web app
* dbhostname and databasename \(the same used by Platform, since the database schema should be the same\)
* dbusername and password \(the same used by Platform, since the database schema should be the same\)

#### WEB-INF/activiti-ui-context.xml

Here it is important to define correctly the adminGroups and userGroups.

The adminGroups should always include the value 1, since Platform default admin role id is 1.

The userGroups should be all the others.

Anyway, PlatformActiviti.jar integration library should by-pass these default settings and automate the reading of Platform roles.

#### WEB-INF/activiti-standalone-context.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
    xmlns:tx="http://www.springframework.org/schema/tx" xmlns:jee="http://www.springframework.org/schema/jee"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.1.xsd
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.1.xsd
       http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.1.xsd
       http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.1.xsd">

  <!-- This Spring config file is NOT used in Alfresco, as the Activiti engine is wired in a different way there -->
  <!--       
  <bean id="demoDataGenerator" class="org.activiti.explorer.demo.DemoDataGenerator" init-method="init">
    <property name="processEngine" ref="processEngine" />

    <property name="createDemoUsersAndGroups" value="false" />
    <property name="createDemoProcessDefinitions" value="false" />
    <property name="createDemoModels" value="false" />
    <property name="generateReportData" value="false" />
  </bean>
  -->

      <bean id="utils"
        class="it.sinesy.activiti.util.Utils">
    </bean>

  <bean id="dbProperties" class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
    <property name="location" value="classpath:db.properties" />
    <!-- Allow other PropertyPlaceholderConfigurer to run as well -->
    <property name="ignoreUnresolvablePlaceholders" value="true" />
  </bean>

  <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
    <property name="driverClassName" value="${jdbc.driver}" />
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.username}" />
    <property name="password" value="${jdbc.password}" />
    <property name="defaultAutoCommit" value="false" />
  </bean>

  <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
      <property name="dataSource" ref="dataSource" />
  </bean>


  <bean id="processEngineConfiguration" class="org.activiti.spring.SpringProcessEngineConfiguration">
      <property name="dataSource" ref="dataSource" />
      <property name="transactionManager" ref="transactionManager" />
      <property name="databaseSchemaUpdate" value="true" />
      <property name="jobExecutorActivate" value="true" />
     <property name="mailServerHost" value="..." />
    <property name="mailServerPort" value="..." />
   <property name="customFormTypes">
      <list>
        <bean class="org.activiti.explorer.form.UserFormType"/>
        <bean class="org.activiti.explorer.form.ProcessDefinitionFormType"/> 
        <bean class="org.activiti.explorer.form.MonthFormType"/>   
      </list>
    </property>


    <property name="configurators">
      <list>
          <bean class="org.activiti.ldap.LDAPConfigurator">

            <!-- Server connection params -->
            <property name="server" value="..." />
            <property name="port" value="..." />
                <property name="user" value="cn=...,dc=..." />
            <property name="password" value="..." />

            <!-- Query params -->
            <property name="baseDn" value="dc=com" />
            <property name="queryUserByUserId" value="(&amp;(objectClass=person)(cn={0}))" />
            <!--
            <property name="queryUserByUserId" value="(&(objectClass=inetOrgPerson)(uid={0}))" />
            <property name="queryUserByFullNameLike" value="(&(objectClass=inetOrgPerson)(|({0}=*{1}*)({2}=*{3}*)))" />
            -->
            <!--
            <property name="queryGroupsForUser" value="(&(objectClass=groupOfUniqueNames)(uniqueMember={0}))" />
            -->
            <!-- Attribute config -->
            <property name="userIdAttribute" value="..." />
            <property name="userFirstNameAttribute" value="..." />
            <property name="userLastNameAttribute" value="..." />
            <!--
            <property name="groupIdAttribute" value="userPrincipalName" />
            <property name="groupNameAttribute" value="userPrincipalName" />
            -->
            <property name="groupIdAttribute" value="cn" />
            <property name="groupNameAttribute" value="cn" />

            <!--<property name="ldapQueryBuilder" ref="platform4WSLdap" />-->

            <property name="ldapGroupManagerFactory" ref="..."/>
            <property name="ldapUserManagerFactory" ref="..."/>


          </bean>
      </list>
    </property>




  </bean>


  <bean id="ldapConfigBean" class="org.activiti.ldap.LDAPConfigurator" />
  <bean id="platform4WSGroupManagerFactory" class="it.sinesy.activiti.authorizations.Platform4WSGroupManagerFactory" >
      <constructor-arg type="org.activiti.ldap.LDAPConfigurator" ref="ldapConfigBean" />
      <constructor-arg type="org.apache.commons.dbcp.BasicDataSource" ref="dataSource" />
  </bean>
  <bean id="platform4WSUserManagerFactory" class="it.sinesy.activiti.authorizations.Platform4WSUserManagerFactory" >
      <constructor-arg type="org.activiti.ldap.LDAPConfigurator" ref="ldapConfigBean" />
      <constructor-arg type="org.apache.commons.dbcp.BasicDataSource" ref="dataSource" />
  </bean>

  <bean id="processEngine" class="org.activiti.spring.ProcessEngineFactoryBean" destroy-method="destroy">
      <property name="processEngineConfiguration" ref="processEngineConfiguration" />
  </bean>

  <bean id="repositoryService" factory-bean="processEngine" factory-method="getRepositoryService" />
  <bean id="runtimeService" factory-bean="processEngine" factory-method="getRuntimeService" />
  <bean id="taskService" factory-bean="processEngine" factory-method="getTaskService" />
  <bean id="historyService" factory-bean="processEngine" factory-method="getHistoryService" />
  <bean id="managementService" factory-bean="processEngine" factory-method="getManagementService" />
  <bean id="identityService" factory-bean="processEngine" factory-method="getIdentityService" />

  <bean id="activitiLoginHandler" class="org.activiti.explorer.ui.login.DefaultLoginHandler">
    <property name="identityService" ref="identityService" />
  </bean>

</beans>
```

Here it is important to

* comment/remove the section related to the demo included by default in Activiti
* include the "utils" bean, used by a few Service Tasks provided by Platform \(web service, SQL execution\)
* define the SMTP settings, in order to allow sending email from automatic tasks
* define the LDAP settings, in order to inherit accounts from Platform embedded LDAP server or from an external LDAP server

The Platform embedded LDAP server can be used in case you do not have an LDAP server available in your organization but still want to manage the same users and groups \(roles\) managed in Platform. In such a scenario, Platform can be configured to provide an LDAP, so that Activiti can connect to and ask for authentication and user roles.

**Note**: you have to choose this choice also when you have an external LDAP server but this does not provide groups as well.

These are the right settings in this scenario:

```
<property name="server" value="ldap://localhost" />
<property name="port" value="3489" />
<property name="user" value="cn=ADMIN,dc=com" />
<property name="password" value="..." />

<property name="userIdAttribute" value="userPrincipalName" />
<property name="userFirstNameAttribute" value="givenName" />
<property name="userLastNameAttribute" value="sn" />

<property name="groupIdAttribute" value="cn" />
<property name="groupNameAttribute" value="cn" />

<property name="ldapGroupManagerFactory" ref="platform4WSGroupManagerFactory"/>
<property name="ldapUserManagerFactory" ref="platform4WSUserManagerFactory"/>
```

In case your organization already provides an external LDAP server \(and consequently Platform has been already configured to redirect the authentication task to it\), the same LDAP server must be configured here too.

In such a scenario, you have to fill in the same settings reported above, with values depending on the specific LDAP settings and related users/groups configurations.

#### WEB-INF/classes/stencilset.json

This file contains the palette content in the Worflow editor. It can be \(partially\) customized.

The default stencilset.json content includes the definition of the servicetask, with can be enhanced with what reported below, so that the Service Task \(the most used automatic task involving Plaform\) provides additional settings, helpful when using this kind of task. Using the content reported below, the Service Task provides 3 pre-defined uses of Service Tasks: SQL Statement \(execution of SQL writing instructions\), SQL Query \(execution of SQL queries\), Platform Web service \(public or not\).

In order to apply these changes, open with a text editor the stencilset.json file, find the "servicetaskbase" definition and replace the whole content was follows:

```
        {
            "name": "servicetaskbase",
            "properties": [{
                "id": "servicetaskclass",
                "type": "Choice",
                "title": "Class",
                "value": "",
                "items": [{
                    "id": "ExecuteSqlStmtServiceTask",
                    "title": "SQL Statement",
                    "value": "it.sinesy.activiti.services.ExecuteSqlStmtServiceTask"
                }, {
                    "id": "ExecuteSqlQueryServiceTask",
                    "title": "SQL Query",
                    "value": "it.sinesy.activiti.services.ExecuteSqlQueryServiceTask"
                }, {
                    "id": "ExecuteComponentServiceTask",
                    "title": "Platform Web Service",
                    "value": "it.sinesy.activiti.services.ExecuteComponentServiceTask"
                }],
                "description": "Class that implements the service task logic.",
                "popular": true
            }, {
                "id": "servicetaskexpression",
                "type": "String",
                "title": "Expression",
                "value": "",
                "description": "Service task logic defined with an expression.",
                "popular": true
            }, {
                "id": "servicetaskdelegateexpression",
                "type": "String",
                "title": "Delegate expression",
                "value": "",
                "description": "Service task logic defined with a delegate expression.",
                "popular": true
            }, {
                "id": "servicetaskresultvariable",
                "type": "String",
                "title": "Result variable name",
                "value": "",
                "description": "Process variable name to store the service task result.",
                "popular": true
            }, {
                "id": "servicetaskfields",
                "type": "Complex",
                "title": "Class fields",
                "value": "{ \"totalCount\": 11, \"items\": [{ \"servicetask_field_name\": \"sql\" },{ \"servicetask_field_name\": \"dataSourceName\" },{ \"servicetask_field_name\": \"result\" },{ \"servicetask_field_name\": \"companyId\" },,{ \"servicetask_field_name\": \"siteId\" },{ \"servicetask_field_name\": \"applicationId\" },{ \"servicetask_field_name\": \"httpMethod\" },{ \"servicetask_field_name\": \"url\" },{ \"servicetask_field_name\": \"requestBody\" },{ \"servicetask_field_name\": \"fireError\" },{ \"servicetask_field_name\": \"username\" }] }",
                "description": "Field extensions",
                "popular": true,
                "complexItems": [{
                    "id": "servicetask_field_name",
                    "name": "Name",
                    "type": "String",
                    "value": "",
                    "width": 100,
                    "optional": false
                }, {
                    "id": "servicetask_field_value",
                    "name": "String value",
                    "type": "String",
                    "value": "",
                    "width": 500,
                    "optional": true
                }, {
                    "id": "servicetask_field_expression",
                    "name": "Expression",
                    "type": "String",
                    "value": "",
                    "width": 200,
                    "optional": true
                }]
            }]
        }
```

#### explorer/src/css/custom-styles.css

Find the following 2 class definitions and replace them with the following content:

```
.north_view .x-panel-body,
.x-panel-editor-north .x-panel-body {
    /*height:0px !important;*/
    height:32px !important;
    top: 0px;
}


.x-panel-editor-north .x-panel .x-panel-body {
    /*height:40px !important;*/
    height:0px !important;
}


#editor_header {
  background:url("../img/signavio/smoky/header_background2.png") repeat-x scroll center -4px transparent !important;
  width: 100%;
  overflow:hidden; 
  position: relative;
/*  height: 40px;*/
  height: 0px;

}




/* new css classes */

.x-panel-editor-west .x-panel-body {
  background-color:#FEFEFE !important;
}

.x-tree-node {
  background-color:#FEFEFE !important;
  background: #FEFEFE url(../../libs/ext-2.0.2/resources/images/gray/panel/white-top-bottom.gif) repeat-x scroll 0 0 !important;
}

.x-grid3{position:relative;overflow:hidden;background-color: #FDFDFD !important;}
 

```

---

### Configuration files for Activiti Rest

Here there isa file to configure is WEB-INF/classes/db.properties, with the same content described in the previous section.

Apart from it, there is also the file WEB-INF/classes/activiti-context.xml to configure:

```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-2.5.xsd
http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.0.xsd">

    <!-- Comment this if you don't need demo data 
    <bean id="demoDataGenerator" class="org.activiti.rest.service.demo.DemoDataGenerator"
        init-method="init">
        <property name="processEngine" ref="processEngine" />
        <property name="createDemoUsersAndGroups" value="false" />
        <property name="createDemoProcessDefinitions" value="false" />
        <property name="createDemoModels" value="false" />
    </bean>
     -->
     <bean id="utils"
        class="it.sinesy.activiti.util.Utils">
    </bean>

    <bean id="dbProperties"
        class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
        <property name="location" value="classpath:db.properties" />
        <!-- Allow other PropertyPlaceholderConfigurer to run as well -->
        <property name="ignoreUnresolvablePlaceholders" value="true" />
    </bean>

    <bean id="dataSource"
        class="org.springframework.jdbc.datasource.SimpleDriverDataSource">
        <property name="driverClass" value="${jdbc.driver}" />
        <property name="url" value="${jdbc.url}" />
        <property name="username" value="${jdbc.username}" />
        <property name="password" value="${jdbc.password}" />
    </bean>

    <bean id="transactionManager"
        class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource" />
    </bean>

    <bean id="processEngineConfiguration" class="org.activiti.spring.SpringProcessEngineConfiguration">

                <property name="dataSource" ref="dataSource" />
                <property name="transactionManager" ref="transactionManager" />
                <property name="databaseSchemaUpdate" value="true" />
                <property name="mailServerPort" value="..." />
                <property name="jobExecutorActivate" value="false" />
                <property name="mailServerPassword" value="..." />
                <property name="mailServerUsername" value="..." /-->
                <property name="mailServerHost" value="..." />
                <property name="mailServerPassword" value="..." />
                <property name="mailServerUsername" value="..." />

                <property name="jobExecutorActivate" value="false" />
                <property name="configurators">

          <list>
              <bean class="org.activiti.ldap.LDAPConfigurator">

                <!-- Server connection params -->
                <property name="server" value="ldap://localhost" />
                <property name="port" value="3389" />
                        <property name="user" value="cn=ADMIN,dc=com" />
                    <property name="password" value="..." />    
                <!-- Query params -->
                <property name="baseDn" value="dc=com" />
                    <property name="queryUserByUserId" value="(&amp;(objectClass=person)(cn={0}))" />
                <!--
                <property name="queryUserByUserId" value="(&(objectClass=inetOrgPerson)(uid={0}))" />
                <property name="queryUserByFullNameLike" value="(&(objectClass=inetOrgPerson)(|({0}=*{1}*)({2}=*{3}*)))" />
                -->
                <!--
                <property name="queryGroupsForUser" value="(&(objectClass=groupOfUniqueNames)(uniqueMember={0}))" />
                -->
                <!-- Attribute config -->
                <property name="userIdAttribute" value="userPrincipalName" />
                <property name="userFirstNameAttribute" value="givenName" />
                <property name="userLastNameAttribute" value="sn" />

                <property name="groupIdAttribute" value="cn" />
                <property name="groupNameAttribute" value="cn" />

            <property name="ldapGroupManagerFactory" ref="platform4WSGroupManagerFactory"/>
            <property name="ldapUserManagerFactory" ref="platform4WSUserManagerFactory"/>


              </bean>
          </list>
        </property>
    </bean>



  <bean id="ldapConfigBean" class="org.activiti.ldap.LDAPConfigurator" />
  <bean id="platform4WSGroupManagerFactory" class="it.sinesy.activiti.authorizations.Platform4WSGroupManagerFactory" >
      <constructor-arg type="org.activiti.ldap.LDAPConfigurator" ref="ldapConfigBean" />
      <constructor-arg type="org.springframework.jdbc.datasource.SimpleDriverDataSource" ref="dataSource" />
    </bean>
    <bean id="platform4WSUserManagerFactory" class="it.sinesy.activiti.authorizations.Platform4WSUserManagerFactory" >
      <constructor-arg type="org.activiti.ldap.LDAPConfigurator" ref="ldapConfigBean" />
      <constructor-arg type="org.springframework.jdbc.datasource.SimpleDriverDataSource" ref="dataSource" />
  </bean>
    <bean id="processEngine" class="org.activiti.spring.ProcessEngineFactoryBean">
        <property name="processEngineConfiguration" ref="processEngineConfiguration" />
    </bean>

</beans>
```

**Note**: comment the section about the demo data.

**Note**: include the utils bean and the SMTP settings for sending emails.

**Note**: in the example above, the authentication process has been redirected to the embedded LDAP server in Platform.

### Configuration in Platform App Designer

In order to let Platform communicate with Activiti, at least 2 parameters must be defined:

* ACTIVITI - URL to Activiti Rest - the value for this parameter must be set with a local URL, since this web app must not be public, but only accessible from within Platform server, so the URL should be something like: [http://localhost:activitiport/](http://localhost:activitiport/)
* ACTIVITI - URL to Activiti Explorer - the value for this parameter must be set with a public URL, since the web editor must be opened remotelly, starting form the Platform App Designer, so the URL should be something like: [https://serverhost/activiti-explorer](https://serverhost/activiti-explorer)

Finally, in case you want to activate the Platform embedded LDAP server, you have also to fill in the parameter named "LDAP - Embedded  LDAP port", with the same value specified in WEB-INF/activiti-standalone-context.xml

