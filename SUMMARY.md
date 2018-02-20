# Summary

* [Introduction](README.md)
* Overview
  * [About 4WS.Platform](1-1--Architecture.md)
  * [Creating a web application](creating-a-web-application.md)
* [Core features](core-features.md)
  * [Defining a data model and relations](3-1-4-Definition-of-Data-Models-and-Relations.md)
  * Defining business components
    * [What are business components](3-1-5-Business-Components.md)
    * [Business components to fill-in panels](EE1-3-6-Definition-of-business-components-to-fill-in-panels.md)
    * Creating business components
      * [By a datastore entity](EE4-4--How-to-create-business-components.md)
      * [By a MongoDB collection](EE8-4--How-to-create-business-components.md)
    * [Defining Custom Java Business component](EE9-2-2-How-to-define-a-Custom-Java-Business-component.md)
  * Defining the UI
    * [Translations about GUI components and internationalization settings](3-1-14-1-Translations-about-GUI-components-and-internationalization-settings.md)
  * [Working with users and roles](3-1-17-Users-and-Roles.md)
  * Wizard
  * Defining events
    * [Panel events](3-1-8-1-Panel-events.md)
    * [Column events](3-1-8-3-Column-events.md)
    * [Control events](3-1-8-5-Control-events.md)
    * [Filter events](3-1-8-7-Filter-events.md)
    * [Timer events](EE0-4-8-Timer-events.md)
    * [Start-End event](EE0-4-10-Start-End-Event.md)
  * Server-side Javascript & Web Service
    * [Server-side Javascript](3-1-12-Server-side-Javascript.md)
    * [Grid component filled by a server-side JS](3-1-5-3-Grid-component-filled-by-a-server-side-JS.md)
    * [Detail component filled by a server-side JS](3-1-5-4-Detail-component-filled-by-a-server-side-JS.md)
    * [How to define a server-side JavaScript action](EE9-2-4--How-to-define-a-server-side-Javascript-action.md)
    * [Web service](EE0-4-5-1-Web-service.md)
* Setting up the environment
  * [Application parameters](3-1-18-2-Application-parameters.md)
  * [Global parameters](3-1-18-1-Global-parameters.md)
* Modules
  * Reports & Charts
    * [Jasper Report + iReport](3-1-22-Reports.md)
    * [Online report](3-1-16-Reports-on-the-fly.md)
    * [Docx templating](3-2-8-Docx-Reports-from-a-template.md)
    * [Charts](3-1-6-10-Charts.md)
  * SSO
    * LDAP
      * [LDAP support](3-2-3-LDAP-support.md)
      * [Connecting an LDAP server to Activiti BPM](EE6-1-2-2-Connecting-an-LDAP-server-to-Activiti-BPM.md)
      * [Connecting an LDAP server to Alfresco ECM](EE6-1-2-1-Connecting-an-LDAP-server-to-Alfresco-ECM.md)
      * [Identity management based on LDAP and database](EE6-1-2-Identity-management-based-on-LDAP-and-database.md)
      * [Identity management based on an embedded LDAP server used by Alfresco and or Activiti](EE6-1-4-Identity-management-based-on-an-embedded-LDAP-server-used-by-Alfresco-and-or-Activiti.md)
      * [Identity management based on a remote LDAP server to connect to Platform on the cloud](EE6-1-5-Identity-management-based-on-a-remote-LDAP-server-to-connect-to-Platform-on-the-cloud.md)
    * Google SSO
      * [Google SSO](EE5-SSO.md)
      * [Identity management based on Google SSO](EE6-1-3-Identity-management-based-on-Google-SSO.md)
    * Custom SSO
  * Mobile
    * Mobile introduction

    * Offline vs Online
      * Server side features
      * Server side functionalities
      * Server side platform features
      * Mobile app features

    * Mobile side specifics
      * Customizations
        * Custom theme editor
      * App Menu
      * Window content
        * Detail scrollable form
        * Scrollable paginated grid
    * What mobile side not includes
    * Reference guide
      * Mobile Javascript utility methods
      * Global variables
      * Application settings
        * Synchronization folder
        * Application version
        * Files writing and reading
        * Import and Export commands
        * Import-export start time and wait time
        * Delete old data task
    * How to
      * How to create a new mobile app
      * How to download file stored remotelly
      * How to send an email
      * How to pass forward parameters
      * How to pass back parameters
      * How to share a document text on social media
      * Push notifications
      * How to scan a QRcode or barcode
      * How to get GPS coordinates
      * How to add a FAB button
      * How to define custom images
      * How to disable hide buttons in a toolbar
      * How to change color for input controls
      * How to change colors in grid
      * How to format data in grid
      * Files management
        * Prepare files through SQL
        * Prepare files through a zip based upload
      * Taking a photo and sending it to the server
      * Filtering a grid column without a filter panel
      * Adding a complex caption in the image gallery
      * Adding clickable content to a grid
      * How to show alternative content in a window
      * How to create a wizard to navigate through a series of panel with Previous-Next buttons
    * App deployment
      * App deployment for the iOS platform
      * App deployment for the Android platform
    * Appendix : Synchronization flow
  * [GSuite](gsuite.md)
    * [Gmail](EE5-GMail.md)
    * [Calendar](EE5-Google-Calendar.md)
    * [Drive](EE5-Google-Drive.md)
  * Google Cloud Platform
    * Datastore
      * [Google Datastore Introduction](EE4-1--Google-Datastore-Introduction.md)
      * [How to create Datastore entities](EE4-3--How-to-create-entities.md)
    * [Cloud Storage](EE5-Google-Cloud-Storage.md)
  * Scheduler
    * [Scheduler](3-2-2-Scheduler.md)
    * [Enterprise Scheduler](EE9-1--Scheduler-Introduction.md)
  * Queue Manager
  * [Log & Analysis](EE10-1--Log-and-analysis.md)
  * Audit
  * BPM
    * [BPMN Introduction](EE0-1--BPM-Introduction.md)
    * [BPMN main parts](EE0-2--BPMN-main-parts.md)
    * [Platform integration](EE0-3--Platform-integration.md)
      * [Processes](EE0-3-1-Processes.md)
      * [Models](EE0-3-2-Models.md)
      * [Process instances](EE0-3-3-Process-instances.md)
      * [To-do list](EE0-3-4-To-do-list.md)
      * [Process history](EE0-3-5-Process-history.md)
    * [Process Web Modeler](EE0-4--Process-Web-Modeler.md)
      * [Model Creation](EE0-4-1-Model-creation.md)
        * [Start-End Event](EE0-4-10-Start-End-Event.md)
        * [Gateways](EE0-4-11-Gateways.md)
      * [Supported objects](EE0-4-2-Supported-objects.md)
      * [Start tasks and user tasks](EE0-4-3-Start-Tasks-and-User-tasks.md)
      * [Form properties](EE0-4-4-Form-properties.md)
        * [Important notes](EE0-4-4-1-Important-notes.md)
        * [Property types](EE0-4-4-2-Property-types.md)
      * [Service tasks](EE0-4-5-Service-tasks.md)
        * [Web service](EE0-4-5-1-Web-service.md)
        * [SQL Query](EE0-4-5-2-SQL-Query.md)
        * [SQL statement](EE0-4-5-3-SQL-statement.md)
      * [Mail task](EE0-4-6-Mail-task.md)
      * [Script task](EE0-4-7-Script-task.md)
        * [Example : how to get a value previously read from a SQL query](EE0-4-7-1-Example-how-to-get-a-value-previously-read-from-a-SQL-query.md)
        * [Example : how to get the current process instance id](EE0-4-7-2-Example-how-to-get-the-current-process-instance-id.md)
      * [Timer events](EE0-4-8-Timer-events.md)
      * [Subprocess and Call Activiti](EE0-4-9-Subprocess-and-Call-activiti.md)
    * Utility methods available in Platform
      * [How to start a process from a JavaScript action](EE0-5-1-How-to-start-a-process-from-a-Javascript-action.md)
      * [How to complete a user task from a JavaScript action](EE0-5-2-How-to-complete-a-user-task-from-a-javascript-action.md)
    * An example
      * [From theory to practise](EE0-6-1-From-theory-to-practise.md)
      * [Processes](EE0-6-2-Processes.md)
      * [Instances](EE0-6-3-Instances.md)
      * [Activities](EE0-6-4-Activities.md)
      * [History](EE0-6-5-History.md)
  * ECM
    * Alfresco
      * [Alfresco Introduction](EE1-1--Alfresco-Introduction.md)
      * [Integration between 4WS.Platform and Alfresco](EE1-2--Integration-between-4WS-Platform-and-Alfresco.md)
        * [Integration at GUI level](EE1-2-1-Integration-at-GUI-level.md)
        * [Integration at model level](EE1-2-2-Integration-at-model-level.md)
        * [Integration at authentication and authorizations level](EE1-2-3-Integration-at-authentication-and-authorizations-level.md)
        * [Additional features](EE1-2-4-Additional-features.md)
      * [How to use 4WS.Platform and Alfresco together](EE1-3--How-to-use-4WS-Platform-and-Alfresco-together.md)
        * [Set the same Identity Management system](EE1-3-1-Set-the-same-Identity-Management-system.md)
        * [Define document types and aspects in Alfresco](EE1-3-2-Define-document-types-and-aspects-in-Alfresco.md)
        * [Import the document types and aspects definitions in 4WS.Platform](EE1-3-3-Import-the-document-types-and-aspects-definitions-in-4WS-Platform.md)
        * [Define document types and aspects in 4WS.Platform](EE1-3-4-Define-document-types-and-aspects-in-4WS-Platform.md)
        * [Reverse engineering of document types or aspects](EE1-3-5-Reverse-engineering-of-document-types-or-aspects.md)
        * [Definition of business components to fill-in panels](EE1-3-6-Definition-of-business-components-to-fill-in-panels.md)
        * [Definition of the GUI](EE1-3-7-Definition-of-the-GUI.md)
        * [Additional server-side services](EE1-3-8-Additional-server-side-services.md)
      * [Requirements](EE1-4-Requirements.md)
      * [Current limits in 4WS-Platform - Alfresco integration](EE1-5-Current-limits-in-4WS-Platform-Alfresco-integration.md)
  * [Lotus Notes Migration Tool](3-2-1-3-Lotus-Domino-Migration-Tool.md)
  * NoSQL databases
    * [MongoDB](mongodb.md)
    * [Google Datastore](EE5-1--Google-Datastore-Introduction.md)
* Troubleshootings
* Best practises



