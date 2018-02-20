# App Designer

SETTING UP AN APPLICATION  
The starting point for the web or mobile application is the home page, which lists all the configured applications and includes the link to the App Designer.  
Through this menu it is possible to access to the App Designer or to any of the interpreted applications.In any case, when clicking on one of these links, the Login Page is showed: once authenticated into the system, the user can access to the functionalities provided by the selected application.

![](http://4wsplatform.org/wp-content/uploads/2013/10/Login-300x165.jpeg)

Since the default authentication & authorization system is based on the module provided with 4WS.Platform, the Login Page requires: "Company Id", "Site Id", "Username" and "Password". Typically the "Company Id" and "Site Id" values are defined initially, when creating and filling out the database schema.  
Before using an application, the application must be defined inside the app designed.

BASED ON MVC AND MODEL-DRIVEN DEVELOPMENT  
Model-View-Controller: Platform is based on the MVC paradigm. The main components of a configured application are:

* the  **Model**  – a representation of a set of tables
* the  **View**  – the User Interface
* the  **Controller**  – based on events fired by theUser Interface, can communicate with the Model

![](http://4wsplatform.org/wp-content/uploads/2018/02/mvc.png)

Moreover, building an app is based on the  **Model Driven Development** : you have first to define a model and then move forward to the creation of the rest of the application, including the UI and the events working with Model and UI. UI and events depend on the model definition: you can work at UI level starting from what you have first defined through the model.

STEPS TO FOLLOW DURING THE DEFINITION OF A NEW APPLICATION

* **Login**  into the app designer, without selecting any application. This will allow to define a new application.
* **Main application settings**  must be defined in the app detail windows, including its name, subcontext path, theme, logo, background image, menu layout and many other settings, specific for each application.

![](http://4wsplatform.org/wp-content/uploads/2013/10/Details-300x165.jpeg)

* Once defined the look and feel of the new application, it is time to define the  **data model** , in terms of objects and relations among them. Objects are usually defined through a few mouse clicks, starting from the list of the already existing database tables, for whom the object will be automatically created, through a reverse engineering task.

![](http://4wsplatform.org/wp-content/uploads/2013/10/DBObj-300x165.jpeg)

* **Views**  can be configured, again through a few clicks. Windows can be created starting from the list of objects previously defined: it is possible to create any number of windows and panels, for each object and its outgoing relations. A wizard leads the user through the definition task, by choosing the right panel \(grid, detail form, filter panel, tree, image panel, map or their combination\), which is defined using the metadata extracted from the selected object.

![](http://4wsplatform.org/wp-content/uploads/2013/10/NewWindow-300x165.jpeg)

* **Ad hoc business components** can be created, based on objects and their relations, by adding additional filter conditions, by adding or removing inner/outer join relations. Furthermore, business components to feed grids or forms or trees can be defined starting from web services or lists of documents coming from a CMS.

![](http://4wsplatform.org/wp-content/uploads/2013/10/BC-300x165.jpg)

---



