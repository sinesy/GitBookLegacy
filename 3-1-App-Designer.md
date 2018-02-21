# App Designer

The App Designer is used to graphically define the functionalities. The whole system is based on the MVC paradigm: database tables and relations are mapped to models, these can then be showed through different kinds of views, such as grids, trees, detail forms, and so forth. Controllers can be defined to capture events and to manage actions linked to views.  
The main features provided by the app designer are:

* **Definition of additional data sources** , in case of metadata repository different from the application data schema
* **Definition of data models and relations** , through the reverse engineering from database tables/CMS documents metadata.
* **Definition of business components** , used to fetch data from data models, according to specific filters, including documents fetching from a CMS and web service calls.
* **Definition of the application menu** , organized hierarchically in folders, submenus, etc.
* Invocation of different features starting from a menu item, including: windows, web services, reports, shell commands \(e.g. Batches\).
* **Definition of different types of panels** , including: editable grid, form, folders/subpanes, tree, image, google map.
* **Grid columns and input controls definition** , with the support for the most common data types: text, textarea, number, data, time, datatime, check box, combo, code selector, image, file download/upload.
* **Panels can be combined together**  in any way, to create a complex window. Complex interactions among these components can be defined thanks to events linked to components and actions linked to them.
* **Custom extensions**  can be injected to components as well, through events and actions, expressed using several formats: javascript, SQL, web services.
* **Complex windows**  can be defined by combining not only interpreted components, but also embedding custom panels defined through traditional coding, both on the web tier \(javascript and ExtJS\) and on the server tier \(restful web services, EJB or Java Beans\).
* **Authorizations**  include a series of powerful features:

* Roles \(group of functionalities to enable as menu items, grids and forms to enable/disable in insert, update, delete mode\). The combination role-grid functionality can optionally define which grid colums to show/hide, make editable in insert/update, column mandatory.

* Association between a user and a list of roles

At grid level, it is optionally possible to store a  **user profile** , that is to say: columns positions, columns length, filters and sorted columns are stored and the same setting is then set next time the grid will be showed.

* **Multi-language support** . According to the logged user, each part of the GUI is showed using translations related to the language associated to the user. Up to 50 languages can be defined. Data coming from the database can be read according to the user language too.
* **Multi-database** . Several dbms are supported: Oracle, MS SqlServer, MySql, PostgreSQL. Moreover, for each defined application, it is possible to work with multiple database schema, even related to different dbms.

---



