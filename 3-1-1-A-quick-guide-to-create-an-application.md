# A quick guide to create an application

Before using an application, the application must be defined inside the app designer.  
Typically, the steps to follow during the definition of a new application includes:

* **Logging on**  the app designer, without selecting any application. This will allow you to define a new application.
* Defining the  **Application Settings**  required to create an empty application
* Creating the  **Data Model** 
* Creating the **Business Logic** based on the Data Model
* Creating the **User Interface**  **and events** , connected to the Data Model and Business Logic.

In the rest of this section, these steps will be described in depth.

Application Settings  
After logging on, the App Designer requires a few data in order to correctly set up a new empty application. Mandatory data include the  **application identifier** ,the  **application title**  and  **sub-context path** .

![](http://4wsplatform.org/wp-content/uploads/2016/11/Schermata-2016-11-04-alle-15.23.27.png)

An  **application identifier**  represents a unique id used to partition any data per application. The user interface of a specific mobile or web application can communicate with the server-side through that id, so that it is possible to work with a specific application on the server layer.  
The  **application title**  issetasthe web page title of the web application to run. The Platform Home page reports all the applications configured and the App Designer. Each application in the Home pageis identified by its title.  
Finally, the ** sub-context path** represents a public web folder, specific for application, used to store a set of static contentlike images, documents, CSS, report templates.  
You can uploaded such content once created an empty application and then refer them in any other part of the application.  
After settings these mandatory fields, you can press the Save button to confirm the creation of the application.  
This is what is needed in order to create a new web application.  
In case of a mobile application, you have to change the default setting “Device Type” from “Browser” to “Mobile”. In that case, some fields in the application detail window are replaced by others, specific for a mobile app.

Once confirmed the choice, the rest of the App Designerwill be unlocked and you can access to any other feature provided by Platform for that application.

This is a good time to upload in the application some external content \(static content\).

![](http://4wsplatform.org/wp-content/uploads/2016/11/Schermata-2016-11-04-alle-15.16.11.png)

You can upload images or any other content through the functionality:  **Application Management -&gt; Import / Export Application** . The window prompted allows you to upload a compressed .zip file. The content of that .zip file will be automatically decompressed in your application sub-context: you have just to select your local .zip file in the “ **File Management** ” folder and press the “ **Import Files** ” button.

Typically, the next step is to fine tune the application theme.  
You can customize the UI for your application at different levels:

* **changing menu type**  – you can access again to the Application detail window by clicking on the “Application Management” menu item and then to “Application detail”. Here you can change the “Menu type” combo box and select another menu type.Three menu types are supported:

* **Left popup menu**  – the menu is accessible by clicking on the top left button, through which you can access to the menu items, organized hierarchically, in folders. On the topbar there are also a few common commands: Exit, Reload, About, Change Language, which are independent from the application content or the user roles

* **Topbar menu**  – the menu items are reported in the topbar, from left to right; no hierarchy of folders is supported. Inthe same topbar there are also a few common commands: Exit, Reload, About, Change Language, which are independent from the application content or the user roles
* **Buttons + Popup menu and tabs**  – the menu is accessible by clicking on the top right button, through which you can access to the menu items showed in the popup menu, which are organized hierarchically. Just below those items, there are also a few common commands: Exit, Reload, About, Change Language, which are independent from the application content or the user roles

![](http://4wsplatform.org/wp-content/uploads/2016/11/Schermata-2016-11-04-alle-15.15.34.png)

* **about content**  – the About area can contain HTML rich content, related to your company or application: it is up to you deciding which content to include

![](http://4wsplatform.org/wp-content/uploads/2016/11/Schermata-2016-11-04-alle-15.15.46.png)

* **images / application logo**  – the combo-box allows you to select an image and use it as your application logo. Such alogo will be displayed on the top left corner of the web application, on the topbar. Platform comes with a series of predefined images that you can use all around the App Designer. Anyway, you can include your own images through the **Application Management -&gt; Import / Export Application** feature described above and, after that, your images will be automatically visible in the combobox, next time the Application detail window will be opened.
* **images / background image**  – the combo-box allows you to select an image and use it as the background of your application. As for the application logo, images reported in the combobox are a mix between predefined images and optional images that you can import through the upload file function described above.

![](http://4wsplatform.org/wp-content/uploads/2016/11/Schermata-2016-11-04-alle-15.15.58.png)

* **theme customization**  – Platform allows you to easily customize the most common parts of your web application, through the Palette provided in the “Theme customization” area. In case of a mobile app, such area includes a wide range of properties that you can customize. When you press the Save button, Platform asksyou whethersaving also the the palette or not: only if you confirm to save also the custom them, then it will be applied to the application. This choice is provided to the user because there is also a full control access to the application theme, described below. If you choose to save also the custom theme, this will override any manual change to the theme you previously appliedto it.
* **full control theme**  – Platform allows you to fine tune the web application theme. Behind the scenes, there are a series of predefined CSS files, used to control the application UI. These files are automatically created by Platform when you create a new application. The CSS files work on the top-bar, status bar and the main area of the web application They are saved in the sub-context area, as long as your custom files. You can access to the sub-context area if needed, through the  **Administration -&gt; File Manager**  feature: it shows the content of that folder and any other subfolder.Here you can find: css/topbar.css, css/xtheme.css, bar/topbar.html, bar/statusbar.html.
  You can access to these files in the File Manager by double clicking on them and edit if needed. Please not that any manual change applied to these files would be overridden by saving the Application detail window if you confirm to save also the theme customization.

Data Model and Business Components  
Once defined the look and feel of the new application, it is time to define the  **data model** , in terms of  **objects**  and  **relations**  among them. Objects are usually defined through a few mouse clicks, starting from the list of the already existing database tables, for whom the object will be automatically created, through a reverse engineering task.

Windows and Panels  
Next, views can be created, again through a few clicks. Windows can be created starting from the list of objects previously defined: it is possible to create any number of  **windows**  and  **panels** , for each object and its outgoing relations. A wizard leads the user through the definition task, by choosing the right panel \(grid, detail form, filter panel, tree, image panel, map or their combination\), which is defined using the metadata extracted from the selected object.  
Ad hoc business components can be created, based on objects and their relations, by adding additional filter conditions, by adding or removing inner/outer join relations. Furthermore, business components to fillgrids or forms or trees can be defined starting from  **web services**  or lists of  **documents**  coming from a  **CMS** .  
Panels can be refined in terms of grid columns, input controls, filters, events. Users can in any time change the default settings for these components and customize in many ways their behavior.

Application menu  
Finally, the a **pplication menu**  can be organized in folders and menu items. Reports \(based on Jasper Report templates\), shell commands and web services can be started as menu items, too.

Check out the result!  
Once completedall of these steps, your new configured application is ready to be used through the Web Interpreter: go to the Home page, refresh it if needed, and you will see the new application link; when clicking on it, the application login page will appear and you can start using it!

Design tips  
Creating an application requires a few skills. Skills can be quite limited as long as the application to configure fits the way Platform works and uses the features provided by Platform as they are. The more complex the application to realize is, the more effort and skills are required.  
The easiest case is when you simply set a  **menu type, an application logo**  and optionally change the  **colors/fonts**  included in the “Theme customization” area. In such a scenario, the required skills are minimal.  
In case you want to ** highly customize the theme**  of your application, you have always the chance to work on the CSS files provided by Platform, that you can access through the File Manager functionality. In this case, you need to know also skills about the use of Cascading Style Sheets and work with them.  
The choice of  **which menu type to set**  in your application, could be driven by these tips:

* if your application is composed of very few menu items, the best choice is the Topbar menu, since it reports all of them on the top area and let you work on the main area to open your windows. Icons to use for such menu type should typically have a size of 16×16 up to 32×32 pixels.
* if your application is composed of many more menu items and could require a hierarchical organization in folders and subfolders, the best choice is the Popup + buttonsmenu, because it organizes the menu items in folders and let you navigate through those folders up and down and access to the menu items. This menu also includes a Buttons menu showed when opening the application. The advantage here is that you can use these buttons as shortcuts to menu items, without the need for clicking many times to reach a menu item to open a window. Icons to use for both themenus should typically have a larger size of 40×40 pixels or more. The same icons would be auto-scaled when used withinthe popup menu.
* if your application is composed of many menu items and could require a hierarchical organization in folders and want to see a larger area for the menu items, the best choice is the Left menu, sinceit organizes the menu items in folders, which are already expanded.Icons to use for such menu type should typically have a larger size of 16×16 up to 32×32 pixels.

---



