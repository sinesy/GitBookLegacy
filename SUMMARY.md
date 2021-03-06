# Summary

* [Introduction](README.md)
* [Overview](overview.md)
  * [About 4WS.Platform](about-4wsplatform.md)
    * [Architecture](1-1--Architecture.md)
    * [Enterprise Edition](1-1-1-Enterprise-Edition.md)
    * [Tech specs and requirements](1-1-2-Tech-specs-and-requirements.md)
    * [Warp SDK](1-1-3-Warp-SDK.md)
  * [Creating a web application](3-1-1-A-quick-guide-to-create-an-application.md)
* [Core features](core-features.md)
  * [Tables](3-1-20-Tables.md)
  * [SqlTool](3-1-21-SqlTool.md)
  * [Definition of Data models and Relations](3-1-4-Definition-of-Data-Models-and-Relations.md)
    * [Relations](3-1-4-1-Relations.md)
    * [Reverse Engineering](3-1-4-2-Reverse-Engineering.md)
    * [Custom Fields](custom-fields.md)
  * [Defining business components](defining-business-components.md)
    * [What are business components](3-1-5-Business-Components.md)
    * [Business components to fill-in panels](EE1-3-6-Definition-of-business-components-to-fill-in-panels.md)
    * [Creating business components](creating-business-components.md)
      * [By a datastore entity](EE4-4--How-to-create-business-components.md)
      * [By a MongoDB collection](EE8-4--How-to-create-business-components.md)
    * [Defining Custom Java Business component](EE9-2-2-How-to-define-a-Custom-Java-Business-component.md)
  * [Defining the UI](defining-the-ui.md)
    * [App Designer](3-1-App-Designer.md)
      * [App Designer Menu](3-1-2-App-Designer-Menu.md)
      * [Definition of additional data sources](3-1-3-Definition-of-additional-data-sources.md)
      * [Panel containers and layouts](layout.md)
        * [Tab panel](layout/tab-panel.md)
        * [Alternative panel](layout/alternative-panel.md)
        * [Accordion panel](layout/accordion-panel.md)
        * [Vertical orientation panel](layout/vertical-orientation-panel.md)
        * [Horizontal orientation panel](layout/horizontal-orientation-panel.md)
        * [Table panel](layout/table-panel.md)
        * [Generic panel](layout/ggeneric-panel.md)
        * [Responsive panel](layout/responsive-panel.md)
      * [Creation of a window](3-1-6-Creation-of-a-Window.md)
        * [Grid Panel](3-1-6-1-Grid-Panel.md)
        * [Form Panel](3-1-6-3-Form-Panel.md)
        * [Filter Panel](3-1-6-4-Filter-Panel.md)
        * [Tree Panel](3-1-6-5-Tree-Panel.md)
        * [Google Map Panel](3-1-6-6-Google-Map-Panel.md)
        * [Image Panel](3-1-6-7-Image-Panel.md)
        * [Tree + Grid Panel](3-1-6-8-Tree+Grid-Panel.md)
        * [Image Gallery](3-1-6-9-Image-Gallery.md)
      * [Windows list](3-1-7-Windows-list.md)
      * [Panel definition](3-1-8-Panels-list.md)
        * [Columns properties](3-1-8-2-Columns-properties.md)
        * [Controls properties](3-1-8-4-Controls-properties.md)
        * [Filter properties](3-1-8-6-Filter-properties.md)
      * [Variables](3-1-9-Variables.md)
      * [Code selectors](3-1-10-Code-Selectors.md)
        * [When not to use a dynamic combo-box](3-1-10-1-When-not-to-use-a-dynamic-combo-box.md)
      * [Buttons](3-1-13-Buttons.md)
      * [Translations](3-1-14-Translations.md)
        * [Translations about GUI components and internationalization settings](3-1-14-1-Translations-about-GUI-components-and-internationalization-settings.md)
        * [Data coming from database](3-1-14-2-Data-coming-from-database.md)
        * [Custom code and translations](3-1-14-3-Custom-code-and-translations.md)
      * [Application Menu](3-1-15-Application-Menu.md)
      * [Bulk import binded to a grid](3-1-24-Bulk-import-binded-to-a-grid.md)
    * [Web Interpreter](3-3-Web-Interpreter.md)
      * [Grid components](3-3-1-Grid-components.md)
      * [Detail forms](3-3-2-Detail-forms.md)
      * [Other components](3-3-3-Other-components.md)
      * [Other features](other-features.md)
        * [Chat](3-3-4-1-Chat.md)
      * [Global variables](3-3-5-Global-variables.md)
        * [Client-side global variables](3-3-5-1-Client-side-global-variables.md)
        * [Server global variables](3-3-5-2-Server-global-variables.md)
      * [Forgot Password](3-3-6-Forgot-Password.md)
  * [Working with users and roles](3-1-17-Users-and-Roles.md)
    * [Rule for roles](3-1-17-1-Rule-for-roles.md)
    * [Permissions Administrator](3-1-17-2-Permissions-Administrator.md)
  * [Wizard](3-1-25-Other-wizards.md)
    * [How to add a checkbox grid to select one or more rows](3-1-25-1-How-to-add-a-checkbox-grid-to-select-one-or-more-rows.md)
    * [How to load a second grid when clicking on a row from the first grid](3-1-25-2-How-to-load-a-second-grid-when-clicking-on-a-row-of-the-first-grid.md)
    * [How to load a form when clicking on a row of the grid](3-1-25-3-How-to-load-a-form-when-clicking-on-a-row-of-the-grid.md)
    * [How to open a window when double clicking on a row of the grid](3-1-25-4-How-to-open-a-window-when-double-clicking-on-a-row-of-the-grid.md)
    * [How to open a window with right click on the popup menu](3-1-25-5-How-to-open-a-window-with-right-click-on-the-popup-menu.md)
    * [How to open a window when pressing a button on the grid toolbar](3-1-25-6-How-to-open-a-window-when-pressing-a-button-on-the-grid-toolbar.md)
    * [How to load a grid after loading a form](3-1-25-7-How-to-load-a-grid-after-loading-a-form.md)
    * [How to open a window when pressing a button on the form toolbar](3-1-25-8-How-to-open-a-window-when-pressing-a-button-on-the-form-toolbar.md)
    * [How to load a grid when clicking on a tree node](3-1-25-9-How-to-load-a-grid-when-clicking-on-a-tree-node.md)
    * [How to load a form when clicking on a tree node](3-1-25-10-How-to-load-a-form-when-clicking-on-a-tree-node.md)
  * [Defining events](defining-events.md)
    * [Panel events](3-1-8-1-Panel-events.md)
    * [Column events](3-1-8-3-Column-events.md)
    * [Control events](3-1-8-5-Control-events.md)
    * [Filter events](3-1-8-7-Filter-events.md)
    * [Timer events](EE0-4-8-Timer-events.md)
    * [Start-End event](EE0-4-10-Start-End-Event.md)
  * [Server-side Javascript & Web Service](server-side-javascript-and-web-service.md)
    * [Server-side Javascript](3-1-12-Server-side-Javascript.md)
    * [Grid component filled by a server-side JS](3-1-5-3-Grid-component-filled-by-a-server-side-JS.md)
    * [Detail component filled by a server-side JS](3-1-5-4-Detail-component-filled-by-a-server-side-JS.md)
    * [How to define a server-side JavaScript action](EE9-2-4--How-to-define-a-server-side-Javascript-action.md)
    * [Web service](EE0-4-5-1-Web-service.md)
* [Setting up the environment](setting-up-the-environment.md)
  * [How to install](EE2-How-to-install.md)
  * [Application parameters](3-1-18-2-Application-parameters.md)
  * [Global parameters](3-1-18-1-Global-parameters.md)
* [Modules](modules.md)
  * [Reports & Charts](reports-and-charts.md)
    * [Jasper Report + iReport](3-1-22-Reports.md)
    * [Online report](3-1-16-Reports-on-the-fly.md)
    * [Docx templating](3-2-8-Docx-Reports-from-a-template.md)
    * [Charts](3-1-6-10-Charts.md)
    * [Pivot Grid](3-1-6-2-Pivot-Grid-Panel.md)
    * [Multidimensional pivot grid](multidimensional-pivot-grid.md)
    * [Data Export from SQL query](data-export.md)
  * [SSO](sso.md)
    * [Identity management in Platform](EE6-1--Identity-management-in-Platform.md)
      * [Identity management on the internal Platform database](EE6-1-1-Identity-management-based-on-the-internal-Platform-database.md)
      * [Identity management based on Google SSO](EE6-1-3-Identity-management-based-on-Google-SSO.md)
    * [LDAP](ldap.md)
      * [LDAP support](3-2-3-LDAP-support.md)
      * [Identity management based on LDAP and database](EE6-1-2-Identity-management-based-on-LDAP-and-database.md)
      * [Identity management based on an embedded LDAP server used by Alfresco and or Activiti](EE6-1-4-Identity-management-based-on-an-embedded-LDAP-server-used-by-Alfresco-and-or-Activiti.md)
      * [Identity management based on a remote LDAP server to connect to Platform on the cloud](EE6-1-5-Identity-management-based-on-a-remote-LDAP-server-to-connect-to-Platform-on-the-cloud.md)
      * [Connecting an LDAP server to Activiti BPM](EE6-1-2-2-Connecting-an-LDAP-server-to-Activiti-BPM.md)
      * [Connecting an LDAP server to Alfresco ECM](EE6-1-2-1-Connecting-an-LDAP-server-to-Alfresco-ECM.md)
    * [Google SSO](google-sso.md)
      * [Google SSO](EE5-SSO.md)
      * [Google OAuth2](EE5-Google-OAuth2.md)
      * [Identity management based on Google SSO](EE6-1-3-Identity-management-based-on-Google-SSO.md)
    * [Custom SSO](custom-sso.md)
  * [Mobile](mobile.md)
    * [Mobile introduction](EE7-1--Mobile-Introduction.md)
    * [Offline vs Online](EE7-2--Main-features.md)
      * [Server side features](EE7-1-1-Server-side-features.md)
      * [Server side functionalities](EE7-1-2-Server-side-functionalities.md)
      * [Server side Platform features](EE7-2-2-Server-side-Platform-features.md)
      * [Mobile app features](EE7-2-1-Mobile-app-features.md)
    * [Mobile side specifics](mobile-side-specifics.md)
      * [Customizations](EE7-2-3-Customizations.md)
        * [Custom theme editor](EE7-2-3-1-Custom-theme-editor.md)
      * [App Menu](EE7-2-4-App-Menu.md)
      * [Window content](EE7-2-5-Window-content.md)
        * [Detail scrollable form](EE7-2-5-1-Detail-scrollable-form.md)
        * [Scrollable paginated grid](EE7-2-5-2-Scrollable-paginated-grid.md)
        * [Collection grid view](collection-grid-view.md)
    * [Reference guide](EE7-3--Reference-Guide.md)
    * [Cleaning up data](cleaning-up-data.md)
    * [How to](EE7-4--How-to.md)
    * [App deployment](EE7-5--App-deployment.md)
      * [App deployment for the iOS platform](EE7-5-1-App-deployment-for-the-iOS-platform.md)
      * [App deployment for the Android platform](EE7-5-2-App-deployment-for-the-Android-platform.md)
    * [Constraint Layout](constraint-layout.md)
    * [Style properties](style-properties.md)
    * [Appendix : Synchronization flow](EE7-A1--Appendix-Synchronization-flow.md)
    * [Translations](translations.md)
  * [GSuite](gsuite.md)
    * [Introduction](EE3-1--Google-Collaboration-Introduction.md)
    * [Client-side integration](EE3-2--Client-side-integration.md)
    * [GMail](EE5-GMail.md)
    * [Calendar](EE5-Google-Calendar.md)
    * [Drive](EE5-Google-Drive.md)
    * [Contacts](EE5-Google-Contacts.md)
  * [Google Cloud Platform](google-cloud-platform.md)
    * [Datastore](datastore.md)
      * [Google Datastore Introduction](EE4-1--Google-Datastore-Introduction.md)
      * [How to create Datastore entities](EE4-3--How-to-create-entities.md)
    * [Google Cloud Storage](EE5-Google-Cloud-Storage.md)
  * [Scheduler](scheduler.md)
    * [Scheduler Introduction](EE9-1--Scheduler-Introduction.md)
    * [Process settings](EE9-2--Process-settings.md)
      * [How to define a sequence of consecutive processes](EE9-2-1-How-to-define-a-sequence-of-consecutive-processes.md)
      * [How to define a Custom Java Business component](EE9-2-2-How-to-define-a-Custom-Java-Business-component.md)
      * [How to define a Grid Data Import](EE9-2-3-How-to-define-a-Grid-Data-Import.md)
      * [How to define a server-side Javascript action](EE9-2-4--How-to-define-a-server-side-Javascript-action.md)
    * [Email notifications](EE9-3--Email-notifications.md)
    * [Process executions](EE9-4--Process-executions.md)
    * [Process input parameters](EE9-5--Process-input-parameters.md)
  * [Queue Manager](queue-manager.md)
  * [Log & Analysis](EE10-1--Log-and-analysis.md)
    * [Application Log](EE10-1--Log-and-analysis/application-log.md)
    * [Log statistics](EE10-1--Log-and-analysis/log-statistics.md)
    * [App analyzer](EE10-1--Log-and-analysis/app-analyzer.md)
    * [Table log](EE10-1--Log-and-analysis/table-log.md)
    * [Heap memory analysis](EE10-1--Log-and-analysis/heap-memory-analysis.md)
    * [Service Monitoring](EE10-1--Log-and-analysis/service-monitoring.md)
      * [Introduction](EE10-1--Log-and-analysis/service-monitoring/introduction.md)
      * [Defining a service to monitor](EE10-1--Log-and-analysis/service-monitoring/defining-a-service-monitoring.md)
      * [Notifications setup](EE10-1--Log-and-analysis/service-monitoring/notification-setup.md)
      * [Events automatically managed by Platform](EE10-1--Log-and-analysis/service-monitoring/events-automatically-managed-by-platform.md)
      * [Remote Platform servers](EE10-1--Log-and-analysis/service-monitoring/remote-platform-servers.md)
      * [Knowledge base](EE10-1--Log-and-analysis/service-monitoring/knowledge-base.md)
      * [Adding log programatically](EE10-1--Log-and-analysis/service-monitoring/adding-log-programatically.md)
      * [Searching for logged data](EE10-1--Log-and-analysis/service-monitoring/searching-for-logged-data.md)
      * [Use cases](EE10-1--Log-and-analysis/service-monitoring/use-cases.md)
  * [File Management](3-1-19-1-File-Management.md)
  * [Export and Import of Metadata](3-1-19-Export-and-Import-of-Metadata.md)
    * [Application Metadata Management](3-1-19-2-Application-Metadata-Management.md)
  * [Audit](audit.md)
  * [BPM](bpm.md)
    * [BPMN Introduction](EE0-1--BPM-Introduction.md)
    * [BPMN main parts](EE0-2--BPMN-main-parts.md)
    * [Activiti Setup](activiti-setup.md)
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
    * [Utility methods available in Platform](utility-methods-available-in-platform.md)
      * [How to start a process from a JavaScript action](EE0-5-1-How-to-start-a-process-from-a-Javascript-action.md)
      * [How to complete a user task from a JavaScript action](EE0-5-2-How-to-complete-a-user-task-from-a-javascript-action.md)
    * [An example](an-example.md)
      * [Processes](EE0-6-2-Processes.md)
      * [Instances](EE0-6-3-Instances.md)
      * [Activities](EE0-6-4-Activities.md)
      * [History](EE0-6-5-History.md)
  * [Embedded CMS](EE2-Embedded-CMS.md)
  * [ECM](ecm.md)
    * [Alfresco](ecm/alfresco.md)
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
      * [Current limits in 4WS.Platform - Alfresco integration](EE1-5-Current-limits-in-4WS-Platform-Alfresco-integration.md)
    * [Archiflow](ecm/archiflow.md)
      * [Setup](ecm/archiflow/setup.md)
      * [Archiflow artifacts](ecm/archiflow/archiflow-artifacts.md)
      * [How to](ecm/archiflow/how-to.md)
  * [Lotus Notes Migration Tool](3-2-1-3-Lotus-Domino-Migration-Tool.md)
  * [NoSQL databases](nosql-databases.md)
    * [MongoDB](nosql-databases/mongodb.md)
      * [MongoDB Introduction](EE8-1--Mongo-Introduction.md)
      * [Setting up the environment](EE8-2--Setting-up-the-environment.md)
      * [How to create collections](EE8-3--How-to-create-collections.md)
      * [How to create business components](EE8-4--How-to-create-business-components.md)
      * [How to create windows filled with data coming from MongoDB collections](EE8-5--How-to-create-windows-filled-with-data-coming-from-Mongo-DB-collections.md)
      * [Design rules](EE8-6--Design-rules.md)
    * [Google Datastore](nosql-databases/google-datastore.md)
      * [Google Datastore Introduction](EE4-1--Google-Datastore-Introduction.md)
      * [Setting up the environment](EE4-2--Setting-up-the-environment.md)
      * [How to create entities](EE4-3--How-to-create-entities.md)
      * [How to create business components](EE4-4--How-to-create-business-components.md)
      * [How to create windows filled with data coming from Datastore entities](EE4-5--How-to-create-windows-filled-with-data-coming-from-datastore-entities.md)
      * [Design rules](EE4-6--Design-rules.md)
  * [TensorFlow](tensorflow.md)
  * [Web Page Development](web-page-development.md)
    * [Pure Web Page Development](web-page-development/pure-web-page-development.md)
    * [Google Material Design development](web-page-development/google-material-design-development.md)
    * [Appendix A - a complete example without any lib](web-page-development/appendix-a-a-complete-example-without-any-lib.md)
    * [Appendix B - a complete example with Google MD](web-page-development/appendix-b-a-complete-example-with-google-md.md)
  * [Jira Integration](jira-integration.md)
  * [Platform for GAE](platform-for-gae.md)
  * [SQL errors management](sql-errors-management.md)
  * [Multidimensional pivot grid](multidimensional-pivot-grid.md)
  * [Automated Testing](automated-testing.md)
* [Troubleshootings](troubleshootings.md)
* [Best practises](best-practises.md)
  * [Database design](/2-1-Database-design.md)
  * [Database maintenance](database-maintenance.md)
  * [Creating a Web app : common use cases](/2-3-Creating-a-web-app-common-use-cases.md)
  * [Creating a mobile app : common use cases](/2-4-Creating-a-mobile-app-common-use-cases.md)

