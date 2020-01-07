# BPMN Introduction

BPMN or Business Process Model and Notation is a standard used to describe internal processes of an organization and to provide a graphical representation for a shared procedure, managed by the involved employees and services, in order to optimize the efficiency of the procedure.  
A Business Process Model can be applied to cover a variety of needs, including reminders, timeouts, replacements, email notifications, etc.  
Using a Business Process Model in a large and complex process makes it possible to get a high efficency, especially for these reasons:

* easy to use and learn
* higher execution speed of the procedure
* reduction in the execution time of the whole process.

In order to allow the definition and management of complex business processes using a unique front-end, the Activiti BPM engine and designer have been embedded into 4WS.Platform, a Rapid Application Development solution, available with an open source license and able to create web applications including BPM processes too.  
Activiti is considered one of the best BPM open source engines.  
However, if used as a stand alone product, it has a few weaknesses:

* lack of a document management system inside a process: there is not the support of document versioning, storing and searching for documents forwarded to an external CMS
* a poor and not very user friendly GUI: the provided user interface is quite rigid and not focused on the final user needs
* a poor data validation: the supported data format includes only text, numbers, fixed enumeration and dates, not validated data through a dynamic list of values, nor translated data.

These weak points have been already successfully addressed in 4WS.Platform, so that the embedding of Activiti takes advantage of the 4WS.Platform features, including a high level of customization at GUI and business logic level.  
The main advantages provided by this integration are:

* document storing and sharing can be delegated to 4WS.Platform or other extensions, including Alfresco CMS
* an alternative and better customizable user interface can replace the native GUI provided by Activiti
* a larger set of graphics components are available through 4WS.Platform, including data validation, mandatory fields, additional data types, supported both at the web GUI and at the database layer.

Thanks to this integration, 4WS.Platform allows to design and configure web and mobile applications with a high level of customization and this is due to the availability of the business processes too, managed at business and GUI levels.

---



