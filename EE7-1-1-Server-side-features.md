# Server-side features

The server-side installation of Platform includes several sub-systems:  
 **App Designer**  – the same front-end used to create web applications is used to create mobile applications, with the same paradigma: graphically design the data model, the user interface, manage the events fired by the application.   
Of course, ot all features provided by the web version can be used in tghe mobile version, since they are specific of a server-side installation, such as a scheduler able to run heavy batches or the access to files to stored in volumes accessible from the server.  
Moreover, there are some functionalities designed to work on mobile apps only, since they are specific for a mobile device, such as the GPS function, integration with the camera, etc.  
 **Mobile Web Module ** – this sub-system manages the communication between the mobile apps and the rest of Platform: it prepares the data strcutures to send to the mobile app, data, files and receives data and files coming from the app.  
Some additional features for mobile apps are provided at the GUI level within the App Designer: the list of registered devices, synchronization recordings.  
 **Mobile-like data structures ** – in case of mobile apps which needs to work offline, a set of database tables are required to store local data; Platform automatically manages this set of tables by synchronizing structures and data from the central site to each mobile device; in order to do that, the same data structures to create on the mobilevdevices are available in the central site, so data can be prepared for each devices and data coming from these devices can be received and stored centrally.  
Platform is able to automatically manage the extraction of data coming from a central Information System, such as a database, convert/transform and store it in the mobile-like central tables and send it to each mobile app.  
This task is an essential and critical part of the solution: a mobile app is different form a web application running in a server, because the hardware mounted in a mobile device is lightweight and consequently the apps running on it must be carefully designed, in order to limit the amount of resources consumed by the app, in terms of CPU, memory and space used to store data and files. That means that the database designed for a mobile app must be limited in the number of fields per table, tables and amount of records. As a consequence, it is never a good idea to simply use-as-is the same data structures designed for a web application running in a central site: on the opposite, they should be re-designed by taking case of what just mentioned. That is the reason why a conversion/transformation task is needed to extract data from a central information system to move it to a mobile device.  
Data coming from the devices is automatically stored in the mobile-like central tables. If this data is requisupposed to be sent to a central Information System, this task must be manually managed, since there cannot be an automatic feature able to convert from a simple reduced data structure to a more complex and large structure, as the one typically designed in a central I.S.

---



