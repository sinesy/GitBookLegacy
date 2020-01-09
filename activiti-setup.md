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

Replace the default content with the one reported below, so that the Service Task \(the most used automatic task involving Plaform\) provides additional settings, helpful when using this kind of task. Using the content reported below, the Service Task provides 3 pre-defined uses of Service Tasks: SQL Statement \(execution of SQL writing instructions\), SQL Query \(execution of SQL queries\), Platform Web service \(public or not\).

```
{
	"title": "BPMN 2.0",
	"namespace": "http://b3mn.org/stencilset/bpmn2.0#",
	"description": "This is the BPMN 2.0 stencil set specification.",
	"propertyPackages": [{
			"name": "elementbase",
			"properties": [{
				"id": "overrideid",
				"type": "String",
				"title": "Id",
				"value": "",
				"description": "Unique identifier of the element.",
				"popular": true
			}]
		}, {
			"name": "baseattributes",
			"properties": [{
				"id": "name",
				"type": "String",
				"title": "Name",
				"value": "",
				"description": "The descriptive name of the BPMN element.",
				"popular": true,
				"refToView": "text_name"
			}, {
				"id": "documentation",
				"type": "Text",
				"title": "Documentation",
				"value": "",
				"description": "The descriptive name of the BPMN element.",
				"popular": true
			}]
		}, {
			"name": "diagrambase",
			"properties": [{
				"id": "process_id",
				"type": "String",
				"title": "Process identifier",
				"value": "process",
				"description": "Unique identifier of the process definition.",
				"popular": true
			}, {
				"id": "process_author",
				"type": "String",
				"title": "Process author",
				"value": "",
				"description": "Author of the process definition.",
				"popular": false
			}, {
				"id": "process_executable",
				"type": "Choice",
				"title": "Executable",
				"value": "Yes",
				"description": "Define if the process is executable.",
				"popular": true,
				"items": [{
					"id": "no",
					"title": "No",
					"value": "No"
				}, {
					"id": "yes",
					"title": "Yes",
					"value": "Yes"
				}]
			}, {
				"id": "process_version",
				"type": "String",
				"title": "Process version string (documentation only)",
				"value": "",
				"description": "Version identifier for documentation purpose.",
				"popular": false
			}, {
				"id": "process_namespace",
				"type": "String",
				"title": "Target namespace",
				"value": "http://www.activiti.org/processdef",
				"description": "Target namespace for the process definition.",
				"popular": false
			}]
		}, {
			"name": "usertaskbase",
			"properties": [{
				"id": "formkeydefinition",
				"type": "String",
				"title": "Form key",
				"value": "",
				"description": "Form key of the user task.",
				"popular": true
			}, {
				"id": "duedatedefinition",
				"type": "String",
				"title": "Due date",
				"value": "",
				"description": "Due date of the user task.",
				"popular": true
			}, {
				"id": "prioritydefinition",
				"type": "String",
				"title": "Priority",
				"value": "",
				"description": "Priority of the user task.",
				"popular": true
			}]
		}, {
			"name": "usertaskassignment",
			"properties": [{
				"id": "usertaskassignment",
				"type": "Complex",
				"title": "Assignments",
				"value": "",
				"description": "Assignment definition for the user task",
				"popular": true,
				"complexItems": [{
					"id": "assignment_type",
					"name": "Type",
					"name_de": "Typ",
					"type": "Choice",
					"value": "",
					"width": 100,
					"optional": false,
					"items": [{
						"id": "c1",
						"title": "Assignee",
						"title_de": "Performer",
						"value": "assignee",
						"refToView": ""
					}, {
						"id": "c2",
						"title": "Candidate users",
						"title_de": "HumanPerformer",
						"value": "candidateUsers",
						"refToView": ""
					}, {
						"id": "c3",
						"title": "Candidate groups",
						"title_de": "PotentialOwner",
						"value": "candidateGroups",
						"refToView": ""
					}]
				}, {
					"id": "resourceassignmentexpr",
					"name": "Resource assignment expression",
					"name_de": "Zuordnungs-Ausdruck",
					"type": "String",
					"description": "This defines the expression used for the resource assignment.",
					"description_de": "Definiert den Ausdruck, der fr die Zordung von Ressourcen genutzt wird.",
					"value": "",
					"width": 200,
					"optional": true
				}]
			}]
		}, {
			"name": "formdefinition",
			"properties": [{
				"id": "formproperties",
				"type": "multiplecomplex",
				"title": "Form properties",
				"value": "",
				"description": "Definition of the form with a list of form properties",
				"popular": true,
				"complexItems": [{
					"id": "formproperty_id",
					"name": "Id",
					"name_de": "Typ",
					"type": "String",
					"description": "This defines the expression used for the resource assignment.",
					"description_de": "Definiert den Ausdruck, der fr die Zordung von Ressourcen genutzt wird.",
					"value": "",
					"width": 150,
					"optional": false
				}, {
					"id": "formproperty_name",
					"name": "Name",
					"name_de": "Typ",
					"type": "String",
					"description": "This defines the expression used for the resource assignment.",
					"description_de": "Definiert den Ausdruck, der fr die Zordung von Ressourcen genutzt wird.",
					"value": "",
					"width": 150,
					"optional": false
				}, {
					"id": "formproperty_type",
					"name": "Type",
					"name_de": "Typ",
					"type": "Choice",
					"value": "",
					"width": 100,
					"optional": false,
					"items": [{
						"id": "c1",
						"title": "String",
						"title_de": "String",
						"value": "string",
						"refToView": ""
					}, {
						"id": "c2",
						"title": "Date",
						"title_de": "Date",
						"value": "date",
						"refToView": ""
					}, {
						"id": "c3",
						"title": "Long",
						"title_de": "Long",
						"value": "long",
						"refToView": ""
					}, {
						"id": "c4",
						"title": "Boolean",
						"title_de": "Boolean",
						"value": "boolean",
						"refToView": ""
					}, {
						"id": "c5",
						"title": "Enum",
						"title_de": "Enum",
						"value": "enum",
						"refToView": ""
					}]
				}, {
					"id": "formproperty_expression",
					"name": "Expression",
					"name_de": "Typ",
					"type": "String",
					"description": "This defines the expression used for the resource assignment.",
					"description_de": "Definiert den Ausdruck, der fr die Zordung von Ressourcen genutzt wird.",
					"value": "",
					"width": 200,
					"optional": false
				}, {
					"id": "formproperty_variable",
					"name": "Variable",
					"name_de": "Typ",
					"type": "String",
					"description": "This defines the expression used for the resource assignment.",
					"description_de": "Definiert den Ausdruck, der fr die Zordung von Ressourcen genutzt wird.",
					"value": "",
					"width": 200,
					"optional": false
				}, {
					"id": "formproperty_required",
					"name": "Required",
					"name_de": "Typ",
					"type": "Choice",
					"value": "No",
					"width": 100,
					"optional": false,
					"items": [{
						"id": "yes",
						"title": "Yes",
						"value": "Yes"
					}, {
						"id": "no",
						"title": "No",
						"value": "No"
					}]
				}, {
					"id": "formproperty_readable",
					"name": "Readable",
					"name_de": "Typ",
					"type": "Choice",
					"value": "Yes",
					"width": 100,
					"optional": false,
					"items": [{
						"id": "yes",
						"title": "Yes",
						"value": "Yes"
					}, {
						"id": "no",
						"title": "No",
						"value": "No"
					}]
				}, {
					"id": "formproperty_writeable",
					"name": "Writeable",
					"name_de": "Typ",
					"type": "Choice",
					"value": "Yes",
					"width": 100,
					"optional": false,
					"items": [{
						"id": "yes",
						"title": "Yes",
						"value": "Yes"
					}, {
						"id": "no",
						"title": "No",
						"value": "No"
					}]
				}, {
					"id": "formproperty_formvalues",
					"name": "Form values",
					"name_de": "Typ",
					"type": "Complex",
					"width": 300,
					"optional": false,
					"complexItems": [{
						"id": "formproperty_formvalue_id",
						"name": "Id",
						"type": "String",
						"value": "",
						"width": 100,
						"optional": false
					}, {
						"id": "formproperty_formvalue_name",
						"name": "Name",
						"type": "String",
						"value": "",
						"width": 200,
						"optional": false
					}]
				}]
			}]
		}, {
			"name": "tasklistenersbase",
			"properties": [{
				"id": "tasklisteners",
				"type": "multiplecomplex",
				"title": "Task listeners",
				"value": "",
				"description": "Listeners for a user task",
				"popular": true,
				"complexItems": [{
					"id": "task_listener_event_type",
					"name": "Event",
					"type": "Choice",
					"value": "",
					"width": 100,
					"optional": false,
					"items": [{
						"id": "c1",
						"title": "Create",
						"value": "create",
						"refToView": ""
					}, {
						"id": "c2",
						"title": "Assignment",
						"value": "assignment",
						"refToView": ""
					}, {
						"id": "c3",
						"title": "Complete",
						"value": "complete",
						"refToView": ""
					}, {
						"id": "c4",
						"title": "All Events",
						"value": "all",
						"refToView": ""
					}]
				}, {
					"id": "task_listener_class",
					"name": "Class",
					"type": "String",
					"description": "Listener class.",
					"value": "",
					"width": 200,
					"optional": true
				}, {
					"id": "task_listener_expression",
					"name": "Expression",
					"type": "String",
					"description": "Listener expression definition.",
					"value": "",
					"width": 200,
					"optional": true
				}, {
					"id": "task_listener_delegate_expression",
					"name": "Delegate expression",
					"type": "String",
					"description": "Listener delegate expression definition.",
					"value": "",
					"width": 200,
					"optional": true
				}, {
					"id": "task_listener_fields",
					"name": "Fields",
					"type": "Complex",
					"width": 100,
					"optional": false,
					"complexItems": [{
						"id": "task_listener_field_name",
						"name": "Name",
						"type": "String",
						"value": "",
						"width": 200,
						"optional": false
					}, {
						"id": "task_listener_field_value",
						"name": "String value",
						"type": "String",
						"value": "",
						"width": 200,
						"optional": false
					}, {
						"id": "task_listener_field_expression",
						"name": "Expression",
						"type": "String",
						"value": "",
						"width": 200,
						"optional": false
					}]
				}]
			}]
		},
		
		
		
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
				"value": "{ \"totalCount\": 10, \"items\": [{ \"servicetask_field_name\": \"sql\" },{ \"servicetask_field_name\": \"dataSourceName\" },{ \"servicetask_field_name\": \"result\" },{ \"servicetask_field_name\": \"companyId\" },{ \"servicetask_field_name\": \"applicationId\" },{ \"servicetask_field_name\": \"httpMethod\" },{ \"servicetask_field_name\": \"url\" },{ \"servicetask_field_name\": \"requestBody\" },{ \"servicetask_field_name\": \"fireError\" },{ \"servicetask_field_name\": \"username\" }] }",
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
					"optional": false
				}, {
					"id": "servicetask_field_expression",
					"name": "Expression",
					"type": "String",
					"value": "",
					"width": 200,
					"optional": false
				}]
			}]
		}, {
			"name": "scripttaskbase",
			"properties": [{
				"id": "scriptformat",
				"type": "String",
				"title": "Script format",
				"value": "",
				"description": "Script format of the script task.",
				"popular": true
			}, {
				"id": "scripttext",
				"type": "Text",
				"title": "Script",
				"value": "",
				"description": "Script text of the script task.",
				"popular": true
			}]
		}, {
			"name": "ruletaskbase",
			"properties": [{
				"id": "ruletask_class",
				"type": "String",
				"title": "Class",
				"value": "",
				"description": "Class of the rule task.",
				"popular": true
			}, {
				"id": "ruletask_variables_input",
				"type": "String",
				"title": "Input variables",
				"value": "",
				"description": "Input variables of the rule task.",
				"popular": true
			}, {
				"id": "ruletask_result",
				"type": "String",
				"title": "Result variable",
				"value": "",
				"description": "Result variable of the rule task.",
				"popular": true
			}, {
				"id": "ruletask_rules",
				"type": "String",
				"title": "Rules",
				"value": "",
				"description": "Rules of the rule task.",
				"popular": true
			}, {
				"id": "ruletask_exclude",
				"type": "Choice",
				"title": "Exclude",
				"value": "No",
				"description": "Use the rules property as exclusion.",
				"popular": true,
				"items": [{
					"id": "no",
					"title": "No",
					"value": "No"
				}, {
					"id": "yes",
					"title": "Yes",
					"value": "Yes"
				}]
			}]
		}, {
			"name": "mailtaskbase",
			"properties": [{
				"id": "mailtaskto",
				"type": "Text",
				"title": "To",
				"value": "",
				"description": "The recipients if the e-mail. Multiple recipients are defined in a comma-separated list.",
				"popular": true
			}, {
				"id": "mailtaskfrom",
				"type": "Text",
				"title": "From",
				"value": "",
				"description": "The sender e-mail address. If not provided, the default configured from address is used.",
				"popular": true
			}, {
				"id": "mailtasksubject",
				"type": "Text",
				"title": "Subject",
				"value": "",
				"description": "The subject of the e-mail.",
				"popular": true
			}, {
				"id": "mailtaskcc",
				"type": "Text",
				"title": "Cc",
				"value": "",
				"description": "The cc's of the e-mail. Multiple recipients are defined in a comma-separated list",
				"popular": true
			}, {
				"id": "mailtaskbcc",
				"type": "Text",
				"title": "Bcc",
				"value": "",
				"description": "The bcc's of the e-mail. Multiple recipients are defined in a comma-separated list",
				"popular": true
			}, {
				"id": "mailtasktext",
				"type": "Text",
				"title": "Text",
				"value": "",
				"description": "The content of the e-mail, in case one needs to send plain none-rich e-mails. Can be used in combination with html, for e-mail clients that don't support rich content. The client will then fall back to this text-only alternative.",
				"popular": true
			}, {
				"id": "mailtaskhtml",
				"type": "Text",
				"title": "Html",
				"value": "",
				"description": "A piece of HTML that is the content of the e-mail.",
				"popular": true
			}, {
				"id": "mailtaskcharset",
				"type": "String",
				"title": "Charset",
				"value": "",
				"description": "Allows to change the charset of the email, which is necessary for many non-English languages. ",
				"popular": true
			}]
		}, {
			"name": "callactivitybase",
			"properties": [{
				"id": "callactivitycalledelement",
				"type": "String",
				"title": "Called element",
				"value": "",
				"description": "Process reference.",
				"popular": true
			}, {
				"id": "callactivityinparameters",
				"type": "Complex",
				"title": "In parameters",
				"value": "",
				"description": "Definition of the input parameters",
				"popular": true,
				"complexItems": [{
					"id": "ioparameter_source",
					"name": "Source",
					"type": "String",
					"value": "",
					"width": 200,
					"optional": false
				}, {
					"id": "ioparameter_sourceexpression",
					"name": "Source expression",
					"type": "String",
					"value": "",
					"width": 200,
					"optional": false
				}, {
					"id": "ioparameter_target",
					"name": "Target",
					"type": "String",
					"value": "",
					"width": 200,
					"optional": false
				}]
			}, {
				"id": "callactivityoutparameters",
				"type": "Complex",
				"title": "Out parameters",
				"value": "",
				"description": "Definition of the output parameters",
				"popular": true,
				"complexItems": [{
					"id": "ioparameter_source",
					"name": "Source",
					"type": "String",
					"value": "",
					"width": 200,
					"optional": false
				}, {
					"id": "ioparameter_sourceexpression",
					"name": "Source expression",
					"type": "String",
					"value": "",
					"width": 200,
					"optional": false
				}, {
					"id": "ioparameter_target",
					"name": "Target",
					"type": "String",
					"value": "",
					"width": 200,
					"optional": false
				}]
			}]
		}, {
			"name": "sequenceflowbase",
			"properties": [{
				"id": "conditionsequenceflow",
				"type": "Text",
				"title": "Flow condition",
				"value": "",
				"description": "The condition of the sequence flow",
				"popular": true
			}, {
				"id": "defaultflow",
				"type": "Choice",
				"title": "Default flow",
				"value": "None",
				"description": "Define the sequence flow as default",
				"popular": true,
				"items": [{
					"id": "none",
					"title": "Standard",
					"title_de": "Standard",
					"value": "None"
				}, {
					"id": "default",
					"title": "Default Flow",
					"title_de": "Standardfluss",
					"value": "Default",
					"icon": "connector/list/type.default.png",
					"refToView": "default"
				}]
			}, {
				"id": "conditionalflow",
				"type": "Choice",
				"title": "Conditional flow",
				"value": "None",
				"description": "Define the sequence flow with a condition",
				"popular": true,
				"items": [{
					"id": "none",
					"title": "Standard",
					"title_de": "Standard",
					"value": "None"
				}, {
					"id": "default",
					"title": "Conditional Flow",
					"value": "Conditional",
					"icon": "connector/list/type.expression.png",
					"refToView": "conditional"
				}]
			}]
		}, {
			"name": "cancelactivityattribute",
			"properties": [{
				"id": "cancelactivity",
				"type": "Choice",
				"title": "Cancel activity",
				"value": "yes",
				"description": "Define activity cancelation",
				"popular": true,
				"items": [{
					"id": "yes",
					"title": "Yes",
					"title_de": "Yes",
					"value": "yes"
				}, {
					"id": "no",
					"title": "No",
					"title_de": "No",
					"value": "no"
				}]
			}]
		}, {
			"name": "timerdefinition",
			"properties": [{
				"id": "timerdurationdefinition",
				"type": "String",
				"title": "Time duration (e.g. PT5M)",
				"value": "",
				"description": "Define the timer with a ISO-8601 duration.",
				"popular": true
			}, {
				"id": "timerdatedefinition",
				"type": "String",
				"title": "Time date in ISO-8601",
				"value": "",
				"description": "Define the timer with a ISO-8601 date definition.",
				"popular": true
			}, {
				"id": "timercycledefinition",
				"type": "String",
				"title": "Time cycle (e.g. R3/PT10H)",
				"value": "",
				"description": "Define the timer with a ISO-8601 cycle.",
				"popular": true
			}]
		}, {
			"name": "messagerefdefinition",
			"properties": [{
				"id": "messageref",
				"type": "String",
				"title": "Message reference",
				"value": "",
				"description": "Define the message name.",
				"popular": true
			}]
		}, {
			"name": "signalrefdefinition",
			"properties": [{
				"id": "signalref",
				"type": "String",
				"title": "Signal reference",
				"value": "",
				"description": "Define the signal name.",
				"popular": true
			}]
		}, {
			"name": "errorrefdefinition",
			"properties": [{
				"id": "errorref",
				"type": "String",
				"title": "Error reference",
				"value": "",
				"description": "Define the error name.",
				"popular": true
			}]
		}, {
			"name": "nonestarteventbase",
			"properties": [{
				"id": "initiator",
				"type": "String",
				"title": "Initiator",
				"value": "",
				"description": "Initiator of the process.",
				"popular": true
			}, {
				"id": "formkeydefinition",
				"type": "String",
				"title": "Form key",
				"value": "",
				"description": "Form key of the start event.",
				"popular": true
			}]
		}, {
			"name": "textannotationbase",
			"properties": [{
				"id": "text",
				"type": "String",
				"title": "Text",
				"value": "",
				"description": "The text of the text annotation.",
				"popular": true,
				"refToView": "text"
			}]
		}, {
			"name": "asynchronousbase",
			"properties": [{
				"id": "asynchronousdefinition",
				"type": "Choice",
				"title": "Asynchronous",
				"value": "No",
				"description": "Define the activity as asynchronous.",
				"popular": true,
				"items": [{
					"id": "no",
					"title": "No",
					"value": "No"
				}, {
					"id": "yes",
					"title": "Yes",
					"value": "Yes"
				}]
			}, {
				"id": "exclusivedefinition",
				"type": "Choice",
				"title": "Exclusive",
				"value": "Yes",
				"description": "Define the activity as exclusive.",
				"popular": true,
				"items": [{
					"id": "no",
					"title": "No",
					"value": "No"
				}, {
					"id": "yes",
					"title": "Yes",
					"value": "Yes"
				}]
			}]
		}, {
			"name": "executionlistenersbase",
			"properties": [{
				"id": "executionlisteners",
				"type": "multiplecomplex",
				"title": "Execution listeners",
				"value": "",
				"description": "Listeners for an activity, process, sequence flow, start and end event.",
				"popular": true,
				"complexItems": [{
					"id": "execution_listener_event_type",
					"name": "Event",
					"type": "Choice",
					"value": "",
					"width": 200,
					"optional": false,
					"items": [{
						"id": "c1",
						"title": "Start",
						"value": "start",
						"refToView": ""
					}, {
						"id": "c2",
						"title": "End",
						"value": "end",
						"refToView": ""
					}, {
						"id": "c2",
						"title": "Take (only sequence flows)",
						"value": "take",
						"refToView": ""
					}]
				}, {
					"id": "execution_listener_class",
					"name": "Class",
					"type": "String",
					"description": "Listener class.",
					"value": "",
					"width": 200,
					"optional": true
				}, {
					"id": "execution_listener_expression",
					"name": "Expression",
					"type": "String",
					"description": "Listener expression definition.",
					"value": "",
					"width": 200,
					"optional": true
				}, {
					"id": "execution_listener_delegate_expression",
					"name": "Delegate expression",
					"type": "String",
					"description": "Listener delegate expression definition.",
					"value": "",
					"width": 200,
					"optional": true
				}, {
					"id": "execution_listener_fields",
					"name": "Fields",
					"type": "Complex",
					"width": 100,
					"optional": false,
					"complexItems": [{
						"id": "execution_listener_field_name",
						"name": "Name",
						"type": "String",
						"value": "",
						"width": 200,
						"optional": false
					}, {
						"id": "execution_listener_field_value",
						"name": "String value",
						"type": "String",
						"value": "",
						"width": 200,
						"optional": false
					}, {
						"id": "execution_listener_field_expression",
						"name": "Expression",
						"type": "String",
						"value": "",
						"width": 200,
						"optional": false
					}]
				}]
			}]
		}, {
			"name": "customformdefinition",
			"properties": [{
				"id": "customformdefinition",
				"type": "Choice",
				"title": "Custom form",
				"value": "",
				"description": "Des A",
				"popular": true,
				"items": [{
					"id": "1",
					"title": "form 1",
					"value": "1"
				}, {
					"id": "2",
					"title": "form 2",
					"value": "2"
				}, {
					"id": "3",
					"title": "form 3",
					"value": "3"
				}]
			}]
		}, {
			"name": "loopcharacteristics",
			"properties": [{
				"id": "looptype",
				"type": "Choice",
				"title": "Loop type",
				"value": "None",
				"description": "Repeated activity execution (parallel or sequential) can be displayed through different loop types",
				"popular": false,
				"items": [{
					"id": "c1",
					"title": "None",
					"title_de": "Keine Schleife",
					"value": "None",
					"refToView": "none"
				}, {
					"id": "c2",
					"title": "Standard",
					"title_de": "Standard",
					"value": "Standard",
					"icon": "activity/list/looptype.standard.png",
					"refToView": "loop"
				}, {
					"id": "c3",
					"title": "MI Parallel",
					"title_de": "MI parallel",
					"value": "Parallel",
					"icon": "activity/list/mi.parallel.png",
					"refToView": "parallel"
				}, {
					"id": "c4",
					"title": "MI Sequential",
					"title_de": "MI sequentialisiert",
					"value": "Sequential",
					"icon": "activity/list/mi.sequential.png",
					"refToView": "sequential"
				}]
			}]
		}, {
			"name": "activity",
			"properties": [{
				"id": "multiinstance_sequential",
				"type": "Choice",
				"title": "Sequential (Multi-instance)",
				"value": "Yes",
				"description": "Define the multi instance as sequential.",
				"popular": true,
				"items": [{
					"id": "no",
					"title": "No",
					"value": "No"
				}, {
					"id": "yes",
					"title": "Yes",
					"value": "Yes"
				}]
			}, {
				"id": "multiinstance_cardinality",
				"type": "String",
				"title": "Cardinality (Multi-instance)",
				"value": "",
				"description": "Define the cardinality of multi instance.",
				"popular": true
			}, {
				"id": "multiinstance_collection",
				"type": "String",
				"title": "Collection (Multi-instance)",
				"value": "",
				"description": "Define the collection for the multi instance.",
				"popular": true
			}, {
				"id": "multiinstance_variable",
				"type": "String",
				"title": "Element variable (Multi-instance)",
				"value": "",
				"description": "Define the element variable for the multi instance.",
				"popular": true
			}, {
				"id": "multiinstance_condition",
				"type": "String",
				"title": "Completion condition (Multi-instance)",
				"value": "",
				"description": "Define the completion condition for the multi instance.",
				"popular": true
			}, {
				"id": "isforcompensation",
				"type": "Boolean",
				"title": "Is for compensation",
				"value": "false",
				"description": "A flag that identifies whether this activity is intended for the purposes of compensation.",
				"popular": false,
				"refToView": "compensation"
			}]
		}
	],
	"stencils": [{
		"type": "node",
		"id": "BPMNDiagram",
		"title": "BPMN-Diagram",
		"description": "A BPMN 2.0 diagram.",
		"view": "diagram.svg",
		"icon": "diagram.png",
		"groups": ["Diagram"],
		"mayBeRoot": true,
		"hide": true,
		"propertyPackages": ["baseattributes", "diagrambase", "executionlistenersbase"],
		"roles": []
	}, {
		"type": "node",
		"id": "StartNoneEvent",
		"title": "Start event",
		"description": "A start event without a specific trigger",
		"view": "startevent/none.svg",
		"icon": "startevent/none.png",
		"groups": ["Start Events"],
		"propertyPackages": ["elementbase", "baseattributes", "formdefinition", "nonestarteventbase", "executionlistenersbase"],
		"roles": ["Startevents_all", "sequence_start", "StartEventsMorph", "all"]
	}, {
		"type": "node",
		"id": "StartTimerEvent",
		"title": "Start timer event",
		"description": "A start event with a timer trigger",
		"view": "startevent/timer.svg",
		"icon": "startevent/timer.png",
		"groups": ["Start Events"],
		"propertyPackages": ["elementbase", "baseattributes", "timerdefinition", "executionlistenersbase"],
		"roles": ["Startevents_all", "sequence_start", "StartEventsMorph", "all"]
	}, {
		"type": "node",
		"id": "StartMessageEvent",
		"title": "Start message event",
		"description": "A start event with a message trigger",
		"view": "startevent/message.svg",
		"icon": "startevent/message.png",
		"groups": ["Start Events"],
		"propertyPackages": ["elementbase", "baseattributes", "messagerefdefinition", "executionlistenersbase"],
		"roles": ["Startevents_all", "sequence_start", "StartEventsMorph", "all"]
	}, {
		"type": "node",
		"id": "StartErrorEvent",
		"title": "Start error event",
		"description": "A start event that catches a thrown BPMN error",
		"view": "startevent/error.svg",
		"icon": "startevent/error.png",
		"groups": ["Start Events"],
		"propertyPackages": ["elementbase", "baseattributes", "errorrefdefinition", "executionlistenersbase"],
		"roles": ["Startevents_all", "sequence_start", "StartEventsMorph", "all"]
	}, {
		"type": "node",
		"id": "UserTask",
		"title": "User task",
		"description": "A manual task assigned to a specific person",
		"view": "activity/usertask.svg",
		"icon": "activity/list/type.user.png",
		"groups": ["Activities"],
		"propertyPackages": ["elementbase", "baseattributes", "usertaskbase", "usertaskassignment", "formdefinition", "tasklistenersbase", "asynchronousbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "ActivitiesMorph", "all"]
	}, {
		"type": "node",
		"id": "ServiceTask",
		"title": "Service task",
		"description": "An automatic task with service logic",
		"view": "activity/servicetask.svg",
		"icon": "activity/list/type.service.png",
		"groups": ["Activities"],
		"propertyPackages": ["elementbase", "baseattributes", "servicetaskbase", "asynchronousbase", "executionlistenersbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "ActivitiesMorph", "all"]
	},
	
	
	{
		"type": "node",
		"id": "ScriptTask",
		"title": "Script task",
		"description": "An automatic task with script logic",
		"view": "activity/scripttask.svg",
		"icon": "activity/list/type.script.png",
		"groups": ["Activities"],
		"propertyPackages": ["elementbase", "baseattributes", "scripttaskbase", "asynchronousbase", "executionlistenersbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "ActivitiesMorph", "all"]
	}, {
		"type": "node",
		"id": "BusinessRule",
		"title": "Business rule task",
		"description": "An automatic task with rule logic",
		"view": "activity/businessruletask.svg",
		"icon": "activity/list/type.business.rule.png",
		"groups": ["Activities"],
		"propertyPackages": ["elementbase", "baseattributes", "ruletaskbase", "asynchronousbase", "executionlistenersbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "ActivitiesMorph", "all"]
	}, {
		"type": "node",
		"id": "ReceiveTask",
		"title": "Receive task",
		"description": "An task that waits for a signal",
		"view": "activity/receivetask.svg",
		"icon": "activity/list/type.receive.png",
		"groups": ["Activities"],
		"propertyPackages": ["elementbase", "baseattributes", "asynchronousbase", "executionlistenersbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "ActivitiesMorph", "all"]
	}, {
		"type": "node",
		"id": "ManualTask",
		"title": "Manual task",
		"description": "An automatic task with no logic",
		"view": "activity/manualtask.svg",
		"icon": "activity/list/type.manual.png",
		"groups": ["Activities"],
		"propertyPackages": ["elementbase", "baseattributes", "asynchronousbase", "executionlistenersbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "ActivitiesMorph", "all"]
	}, {
		"type": "node",
		"id": "MailTask",
		"title": "Mail task",
		"description": "An mail task",
		"view": "activity/sendtask.svg",
		"icon": "activity/list/type.send.png",
		"groups": ["Activities"],
		"propertyPackages": ["elementbase", "baseattributes", "mailtaskbase", "asynchronousbase", "executionlistenersbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "ActivitiesMorph", "all"]
	}, {
		"type": "node",
		"id": "SubProcess",
		"title": "Sub process",
		"description": "A sub process scope",
		"view": "activity/subprocess.expanded.svg",
		"icon": "activity/expanded.subprocess.png",
		"groups": ["Structural"],
		"propertyPackages": ["elementbase", "baseattributes", "asynchronousbase", "executionlistenersbase", "loopcharacteristics"],
		"roles": ["sequence_start", "Activity", "sequence_end", "all"]
	}, {
		"type": "node",
		"id": "EventSubProcess",
		"title": "Event sub process",
		"description": "A event sub process scope",
		"view": "activity/event.subprocess.svg",
		"icon": "activity/event.subprocess.png",
		"groups": ["Structural"],
		"propertyPackages": ["elementbase", "baseattributes", "asynchronousbase", "executionlistenersbase"],
		"roles": ["sequence_start", "Activity", "sequence_end", "all"]
	}, {
		"type": "node",
		"id": "CallActivity",
		"title": "Call activity",
		"description": "A call activity",
		"view": "activity/callactivity.svg",
		"icon": "activity/task.png",
		"groups": ["Structural"],
		"propertyPackages": ["elementbase", "baseattributes", "callactivitybase", "asynchronousbase", "executionlistenersbase", "loopcharacteristics", "activity"],
		"roles": ["sequence_start", "Activity", "sequence_end", "all"]
	}, {
		"type": "node",
		"id": "ExclusiveGateway",
		"title": "Exclusive gateway",
		"description": "A choice gateway",
		"view": "gateway/exclusive.databased.svg",
		"icon": "gateway/exclusive.databased.png",
		"groups": ["Gateways"],
		"propertyPackages": ["elementbase", "baseattributes"],
		"roles": ["sequence_start", "sequence_end", "GatewaysMorph", "all"]
	}, {
		"type": "node",
		"id": "ParallelGateway",
		"title": "Parallel gateway",
		"description": "A parallel gateway",
		"view": "gateway/parallel.svg",
		"icon": "gateway/parallel.png",
		"groups": ["Gateways"],
		"propertyPackages": ["elementbase", "baseattributes"],
		"roles": ["sequence_start", "sequence_end", "GatewaysMorph", "all"]
	}, {
		"type": "node",
		"id": "InclusiveGateway",
		"title": "Inclusive gateway",
		"description": "An inclusive gateway",
		"view": "gateway/inclusive.svg",
		"icon": "gateway/inclusive.png",
		"groups": ["Gateways"],
		"propertyPackages": ["elementbase", "baseattributes"],
		"roles": ["sequence_start", "sequence_end", "GatewaysMorph", "all"]
	}, {
		"type": "node",
		"id": "EventGateway",
		"title": "Event gateway",
		"description": "An event gateway",
		"view": "gateway/eventbased.svg",
		"icon": "gateway/eventbased.png",
		"groups": ["Gateways"],
		"propertyPackages": ["elementbase", "baseattributes"],
		"roles": ["sequence_start", "sequence_end", "GatewaysMorph", "all"]
	}, {
		"type": "node",
		"id": "BoundaryErrorEvent",
		"title": "Boundary error event",
		"description": "A boundary event that catches a BPMN error",
		"view": "intermediateevent/error.svg",
		"icon": "catching/error.png",
		"groups": ["Boundary Events"],
		"propertyPackages": ["elementbase", "baseattributes", "errorrefdefinition"],
		"roles": ["sequence_start", "BoundaryEventsMorph", "IntermediateEventOnActivityBoundary"]
	}, {
		"type": "node",
		"id": "BoundaryTimerEvent",
		"title": "Boundary timer event",
		"description": "A boundary event with a timer trigger",
		"view": "intermediateevent/timer.svg",
		"icon": "catching/timer.png",
		"groups": ["Boundary Events"],
		"propertyPackages": ["elementbase", "baseattributes", "cancelactivityattribute", "timerdefinition"],
		"roles": ["sequence_start", "BoundaryEventsMorph", "IntermediateEventOnActivityBoundary"]
	}, {
		"type": "node",
		"id": "BoundarySignalEvent",
		"title": "Boundary signal event",
		"description": "A boundary event with a signal trigger",
		"view": "intermediateevent/signal.catching.svg",
		"icon": "catching/signal.png",
		"groups": ["Boundary Events"],
		"propertyPackages": ["elementbase", "baseattributes", "cancelactivityattribute", "signalrefdefinition"],
		"roles": ["sequence_start", "BoundaryEventsMorph", "IntermediateEventOnActivityBoundary"]
	}, {
		"type": "node",
		"id": "CatchTimerEvent",
		"title": "Intermediate timer catching event",
		"description": "An intermediate catching event with a timer trigger",
		"view": "intermediateevent/timer.svg",
		"icon": "catching/timer.png",
		"groups": ["Intermediate Catching Events"],
		"propertyPackages": ["elementbase", "baseattributes", "timerdefinition", "executionlistenersbase"],
		"roles": ["sequence_start", "sequence_end", "CatchEventsMorph", "all"]
	}, {
		"type": "node",
		"id": "CatchSignalEvent",
		"title": "Intermediate signal catching event",
		"description": "An intermediate catching event with a signal trigger",
		"view": "intermediateevent/signal.catching.svg",
		"icon": "catching/signal.png",
		"groups": ["Intermediate Catching Events"],
		"propertyPackages": ["elementbase", "baseattributes", "signalrefdefinition", "executionlistenersbase"],
		"roles": ["sequence_start", "sequence_end", "CatchEventsMorph", "all"]
	}, {
		"type": "node",
		"id": "CatchMessageEvent",
		"title": "Intermediate message catching event",
		"description": "An intermediate catching event with a message trigger",
		"view": "intermediateevent/message.catching.svg",
		"icon": "catching/message.png",
		"groups": ["Intermediate Catching Events"],
		"propertyPackages": ["elementbase", "baseattributes", "messagerefdefinition", "executionlistenersbase"],
		"roles": ["sequence_start", "sequence_end", "CatchEventsMorph", "all"]
	}, {
		"type": "node",
		"id": "ThrowNoneEvent",
		"title": "Intermediate none throwing event",
		"description": "An intermediate event without a specific trigger",
		"view": "intermediateevent/none.svg",
		"icon": "throwing/none.png",
		"groups": ["Intermediate Throwing Events"],
		"propertyPackages": ["elementbase", "baseattributes", "executionlistenersbase"],
		"roles": ["sequence_start", "ThrowEventsMorph", "sequence_end", "all"]
	}, {
		"type": "node",
		"id": "ThrowSignalEvent",
		"title": "Intermediate signal throwing event",
		"description": "An intermediate event with a signal trigger",
		"view": "intermediateevent/signal.throwing.svg",
		"icon": "throwing/signal.png",
		"groups": ["Intermediate Throwing Events"],
		"propertyPackages": ["elementbase", "baseattributes", "signalrefdefinition", "executionlistenersbase"],
		"roles": ["sequence_start", "ThrowEventsMorph", "sequence_end", "all"]
	}, {
		"type": "node",
		"id": "EndNoneEvent",
		"title": "End event",
		"description": "An end event without a specific trigger",
		"view": "endevent/none.svg",
		"icon": "endevent/none.png",
		"groups": ["End Events"],
		"propertyPackages": ["elementbase", "baseattributes", "executionlistenersbase"],
		"roles": ["EndEventsMorph", "sequence_end", "all"]
	}, {
		"type": "node",
		"id": "EndErrorEvent",
		"title": "End error event",
		"description": "An end event that throws an error event",
		"view": "endevent/error.svg",
		"icon": "endevent/error.png",
		"groups": ["End Events"],
		"propertyPackages": ["elementbase", "baseattributes", "errorrefdefinition", "executionlistenersbase"],
		"roles": ["EndEventsMorph", "sequence_end", "all"]
	}, {
		"type": "edge",
		"id": "SequenceFlow",
		"title": "Sequence flow",
		"description": "Sequence flow defines the execution order of activities.",
		"view": "connector/sequenceflow.svg",
		"icon": "connector/sequenceflow.png",
		"groups": ["Connecting Objects"],
		"layout": [{
			"type": "layout.bpmn2_0.sequenceflow"
		}],
		"propertyPackages": ["elementbase", "baseattributes", "sequenceflowbase"],
		"roles": ["ConnectingObjectsMorph", "all"]
	}, {
		"type": "edge",
		"id": "Association",
		"title": "Association",
		"description": "Associates a text annotation with an element.",
		"view": "connector/association.undirected.svg",
		"icon": "connector/association.undirected.png",
		"groups": ["Connecting Objects"],
		"layout": [{
			"type": "layout.bpmn2_0.sequenceflow"
		}],
		"propertyPackages": ["elementbase", "baseattributes"],
		"roles": ["ConnectingObjectsMorph", "all"]
	}, {
		"type": "node",
		"id": "TextAnnotation",
		"title": "Text annotation",
		"description": "Annotates elements with description text.",
		"view": "artifact/text.annotation.svg",
		"icon": "artifact/text.annotation.png",
		"groups": ["Artifacts"],
		"propertyPackages": ["elementbase", "baseattributes", "textannotationbase"],
		"roles": ["all"]
	}],
	"rules": {
		"cardinalityRules": [{
			"role": "Startevents_all",
			"incomingEdges": [{
				"role": "SequenceFlow",
				"maximum": 0
			}]
		}, {
			"role": "Endevents_all",
			"outgoingEdges": [{
				"role": "SequenceFlow",
				"maximum": 0
			}]
		}],
		"connectionRules": [{
			"role": "SequenceFlow",
			"connects": [{
				"from": "sequence_start",
				"to": ["sequence_end"]
			}]
		}, {
			"role": "Association",
			"connects": [{
				"from": "sequence_start",
				"to": ["TextAnnotation"]
			}]
		}, {
			"role": "Association",
			"connects": [{
				"from": "TextAnnotation",
				"to": ["sequence_end"]
			}]
		}, {
			"role": "IntermediateEventOnActivityBoundary",
			"connects": [{
				"from": "Activity",
				"to": ["IntermediateEventOnActivityBoundary"]
			}]
		}],
		"containmentRules": [{
			"role": "BPMNDiagram",
			"contains": ["all"]
		}, {
			"role": "SubProcess",
			"contains": ["sequence_start", "sequence_end", "from_task_event", "to_task_event", "EventSubprocess", "TextAnnotation"]
		}, {
			"role": "EventSubProcess",
			"contains": ["sequence_start", "sequence_end", "from_task_event", "to_task_event", "TextAnnotation"]
		}],
		"morphingRules": [{
			"role": "ActivitiesMorph",
			"baseMorphs": ["UserTask"],
			"preserveBounds": true
		}, {
			"role": "GatewaysMorph",
			"baseMorphs": ["ExclusiveGateway"]
		}, {
			"role": "StartEventsMorph",
			"baseMorphs": ["StartNoneEvent"]
		}, {
			"role": "EndEventsMorph",
			"baseMorphs": ["StartNoneEvent"]
		}, {
			"role": "CatchEventsMorph",
			"baseMorphs": ["CatchTimerEvent"]
		}, {
			"role": "ThrowEventsMorph",
			"baseMorphs": ["ThrowNoneEvent"]
		}, {
			"role": "TextAnnotation",
			"baseMorphs": ["TextAnnotation"]
		}]
	}
}
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

