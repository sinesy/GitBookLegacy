# Tech specs and requirements

The App Designer and Web Interpreter are a unique web application based on the following technologies:

* **JPA \(Java Persistence API\) ** – a part of the standard JEE 5 and 6 specifications, used to map a relational database to an object model \(ORM\); the App Designer has been developed using this technology for the data access layer
* **JDBC**  – a part of the Java specifications, used to access a relational database through a JDBC driver, using the SQL language to enquiry data
* **EJB or Java Beans ** – 4WS.Platform has been designed to work with an EJB container included with any JEE A.S. as well as with a simple web container such as Apache Tomcat; the business components have been written as EJB Session Bean stateless, so that they can be run inside the EJB container; 4WS.Platform provides also a special "container", a sort of basic EJB container that allows to run the same components without an EJB container: in this way it can be run within a light web container, like Tomcat; this represents the default configuration of 4WS.Platform
* **JAX-RS \(Java Restful API\) – ** a standard layer provided with JEE 6, used to create Restful web services using JSON format to communicate with the GUI; these web services are a sort of "bridge" between the business components and the GUI; an additional perk is that they can be accessed by other applications too, so they are a sort of SOA based solution
* **ExtJS – ** this is probably the best GUI web solution available nowadays: it provides a rich set of Ajax components, including grids, forms, trees and a plethora of many other advanced components; both the App Designer and the Web Interpreter use this software layer along with Warp.ExtJS, to create the GUI.

![](http://4wsplatform.org/wp-content/uploads/2018/02/arch.png)

This product is available in two editions:

* **Community Edition**  – you have to download it, install it manually as well as a database; this edition represents a limited edition when compared with the Enterprise Edition
* **Enterprise Edition**  – including all the functionalities need for the enterprise.

Platform can be executed in two alternative ways:

* **as a Software as a Service \(SaaS\)** , thanks to the Google Cloud Platform \(onlyEnterprise Edition\)
* **in-house**  \(Enterprise Edition and Community Edition\) all you need is the Tomcat 9 web container, Java release 11 and a database.

Certified databases for the in-house solution are: Oracle, MS SqlServer, MySQL, PostgreSQL.  
A last generation browser is required: Google Chrome or Mozilla Firefox are recommended. Anyway, Internet Explorer releases 9 or 10 are supported too \(Microsoft Edge is not supported and is going to be desupported by Microsoft soon\).

---



