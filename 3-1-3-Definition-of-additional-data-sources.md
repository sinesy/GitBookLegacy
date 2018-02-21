# Definition of additional data sources

This task is not mandatory: it is required if the metadata repository schema used by the Web Designer/Interpreter is different from the schema used by the interpreted application. For instance if the application has to connect to multiple database schemas, it is possible to define an additional data source for each of these schema.

![](http://4wsplatform.org/wp-content/uploads/2015/12/additionalDSs-1024x522.jpg)

Information provided when creating a new additional data source includes: database username and password, JDBC connection URL and driver.  
You have also to manually include the JDBC driver into the application classpath, that is to say, you have to include the .jar driver file in tomcat/webapps/platform/WEB-INF/lib or tomcat/lib folder.  
Finally, you have to restart the A.S. in order to read the .jar file and make 4WS.Platform to correctly apply the new data source.  
Typical URL to set as JDBC URL are:

* MS SQLServer database:  **jdbc:sqlserver://SQL2008:1170;databaseName=** 
* MySQL database:  **jdbc:mysql://:3306/?profileSQL=true** 
* Oracle database:  **jdbc:oracle:thin:@:1521:** 
* PostgreSQL database:  **jdbc:postgresql://:5432/** 

---



