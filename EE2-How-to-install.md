# How to Install

In this page you can find instructions about **how to install 4WS.Platform – Community Edition**.  
The Enterprise Edition is available as a SaaS on the Google Cloud, so you do not need to configure anything: the service is available instantly, once purchased the service.

There are two alternative versions of 4WS.Platform:

* **Java 1.7 based version** - Platform started with this version and it spreads up to the **5.2.3 version**
* **Java 11 new version** - this is the most recent version of **Platform: 6.0**, which is functionally equivalent to 5.2.3 version

In the next sections, you can find detailed descriptions about how to install both of them.

---

#### INSTALLING 4WS.PLATFORM COMMUNITY EDITION - JAVA 11

* **Install OpenJDK 11.0.2**  in your machine, if not already available; please, **do NOT use other versions**, such as Oracle JDK 11, otherwise some parts of the product would not work correctly and it would represent a license violation of Oracle JVM. You can find OpenJSK distribution at these links, for each  operating system:

| [Windows 64bit](https://download.java.net/openjdk/jdk11/ri/openjdk-11+28_windows-x64_bin.zip) |
| :--- |
| [Linux 64bit](https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz) |
| [MacOS](https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_osx-x64_bin.tar.gz) |

* 4WS.Platform requires the availability of an empty database schema: install a database server \(if not already installed\) and then **create an empty database** in one of the supported databases and  **be sure to provide grants to create objects**  to the database user that 4WS.Platform will use to connect to that schema. Alternatively, **you can reuse an already existing database schema where a previous version of Platform is used:** in such a scenario, you have still to install Platform for Java 11 and during the installation process specify the already existing schema.
  Supported databases are:

| **Oracle Database ** - release 11.2.0.4 e 12.2 e 12.1 |
| :--- |
| **Microsoft SQL Server** - release 2008R2 or above |
| **MySQL / Google CloudSQL** - release 5.5 or 5.6 |
| **PostgreSQL** |

* Once installed the database, you have to create a schema, a user and link this user to the schema and set the right privileges to the user, in order to allow the user to create objects such as tables, foreign keys, etc.
  You can use MySQL Workbench to carry out these operations.
  We don’t provide support for these activities: we give for granted that you are able to perform them on your own.
* 4WS.Platform requires a Java web container compatible with Java 11: Platform installer already includes Tomcat 9.0.2. If you have already installed it for other purposes, you can reuse it; if you do not have installed it yet, the 4WS.Platform installer will install it along with the product, since it is included in the distribution. You can  **download 4WS.Platform from the Sourceforge repository: ** [http://sourceforge.net/projects/xwsplatform/files](http://sourceforge.net/projects/xwsplatform/files)
* **Decompress**  the .zip file downloaded from the repository and **execute the installer** .  
  **If you are using recent versions of Windows \(e.g. Vista o next versions\), you have to use a superuser and open a DOSprompt by right clicking on it and choose “Run as Administrator”: that is the right way to install the program** .  **DO NOT simply execute the installer using a superuser \(e.g. administrator\), since this has not the same effect** .  
  There are two types of installer: an installer having a graphical user interface and the other without it. The first can be used with Windows or other graphical operating systems; in that case you have simply to follow the wizard and fill out all information required, including database type, host, port and the schema account. With the second one, you have to provide the same information, by executing the installer from the shell.

* In order to run theinstaller having a graphicaluser interface, type the following  **shell**  **command** :  **installgui.sh**  or  **installgui.bat** .

* The installer without a graphical user interface can be invoked fromthe shell: this comes in handy where you are using a remote access to a server \(such as ssh or telnet\) or when a GUI environment is not available; this installer requires to specify a series of data, the same provided using the GUI version.In order to run the installer without the GUI, type the command  **install.sh**  or  **install.bat** , according to the operating system in use.Independently of the execution mode, you have to provide some a few data required to correctly install and configure the product:

* first of all, you have to choose which kind of installation to execute:

  * **New Installation/Change Configuration** - used for the first installation or, very rarely, when you want to change the default installation settings \(like from portal mode to no portal mode\)

  * **Update Installation** - used after the first installation, when executing an upgrade of the already existing installation

* **database settings**, required to connect to the database schema, where the installer will create automatically all the required tables and initial data

* **company id;** it represents a 5 characters code to use to partition all data for a specific “tentant”: 4WS.Platform supports multi-tenancy, that is to say, you can run the same application for distinct organizations, each identified by a specific company id, which is used to partition data per organization

* **default language code**; 4WS.Platform supports any number of languages

* **installation path**, where Tomcat will be installed; if you want to reuse an already existing Tomcat 7 installation, you can simply specify that path and the installer will skip the Tomcat installation task and will install and configure the 4WS.Platform web application only

* **JDK path**: pay attention to this path! it is NOT the JRE path, but  **the JDK path:** if you erroneously set the JRE instead of the JDK, Tomcat will not work correctly and you will not be able to access 4WS.Platform web application; in that case, you have to delete the installation and run the installer again

* **4WS.Platform web context**; the web context is the folder name within webapps Tomcat’s subfolder where the web application will be installed; the same name will be used to connect from a browser; for instance, if you set that web context to “platform”, then the URL to specify in your browser would be: [http://host:port/platform](http://host:port/platform)

* **Run Tomcat**  A.S. and use a browser to connect to the web application; typical URL is: [http://localhost:8080/platform](http://localhost:8080/platform)

The default account to use is:  
company id: 00000  
site id: 100  
username: ADMIN  
password: admin

**It is recommended to use Chrome or Mozilla Firefox browsers** ; Internet Explorer 8 or above are also supported, but they are not optimized for javascript usage as for the other two browsers.

#### PORTING FROM JAVA 1.7 TO JAVA 11

In case you already have a Platform installation previous to Platform 6 \(previous to Java 11\) and need to migrate it to the last version, you have to follow the steps reported above: installing the new version of Plaftorm, specify the same settings for the database connection.

After doing it, bear in mind that you have also to copy a few other files:

* copy the application static content from one installation to the other
* copy the WEb-INF/classes/reports subfolder from the previous installation to the new one

#### 4WS.PLATFORM INSTALLER STEPS

* **START**

  Type the following command from the shell: installgui.sh or installgui.bat.

  ![](http://4wsplatform.org/wp-content/uploads/2013/10/Install0-300x206.png)

* **SETTING DATABASE**

  Insert data of database connection.

  [![](http://4wsplatform.org/wp-content/uploads/2013/10/Install1-300x206.png)](http://4wsplatform.org/wp-content/uploads/2013/10/Install1.png)

* **SETTING CONFIG**

  Complete configuration fields for installation.

  [![](http://4wsplatform.org/wp-content/uploads/2013/10/Install2-300x206.png)](http://4wsplatform.org/wp-content/uploads/2013/10/Install2.png)

* **END**

  Enjoy 4WS.Platform.

  [![](http://4wsplatform.org/wp-content/uploads/2013/10/Install3-300x206.png)](http://4wsplatform.org/wp-content/uploads/2013/10/Install3.png)

---

#### INSTALLING 4WS.PLATFORM COMMUNITY EDITION - JAVA 1.7 \(OLDER VERSION\)

* **Install JDK 1.7**  in your machine, if not already available; please, **do NOT use other versions**, such as OpenJDK, otherwise some parts of the product would not work correctly.

* 4WS.Platform requires the availability of an empty database schema: install a database server \(if not already installed\) and then **create an empty database** in one of the supported databases \(Oracle, MySQL 5.x or above, SQLServer 2008 or above, PostgreSQL 9 or above\) and  **be sure to provide grants to create objects**  to the database user that 4WS.Platform will use to connect to that schema.

* Once installed the database, you have to create a schema, a user and link this user to the schema and set the right privileges to the user, in order to allow the user to create objects such as tables, foreign keys, etc.  
  You can use MySQL Workbench to carry out these operations.  
  We don’t provide support for these activities: we give for granted that you are able to perform them on your own.

* 4WS.Platform requires a Java web container compatible with Java 1.7: Platform installer already includes Tomcat 7. If you have already installed it for other purposes, you can reuse it; if you do not have installed it yet, the 4WS.Platform installer will install it along with the product, since it is included in the distribution. You can  **download 4WS.Platform from the Sourceforge repository: ** [http://sourceforge.net/projects/xwsplatform/files](http://sourceforge.net/projects/xwsplatform/files)

* **Decompress**  the .zip file downloaded from the repository and **execute the installer** .  
  **If you are using recent versions of Windows \(e.g. Vista o next versions\), you have to use a superuser and open a DOSprompt by right clicking on it and choose “Run as Administrator”: that is the right way to install the program** .  **DO NOT simply execute the installer using a superuser \(e.g. administrator\), since this has not the same effect** .  
  There are two types of installer: an installer having a graphical user interface and the other without it. The first can be used with Windows or other graphical operating systems; in that case you have simply to follow the wizard and fill out all information required, including database type, host, port and the schema account. With the second one, you have to provide the same information, by executing the installer from the shell.

* In order to run theinstaller having a graphicaluser interface, type the following  **shell**  **command** :  **installgui.sh**  or  **installgui.bat** .

* The installer without a graphical user interface can be invoked fromthe shell: this comes in handy where you are using a remote access to a server \(such as ssh or telnet\) or when a GUI environment is not available; this installer requires to specify a series of data, the same provided using the GUI version.In order to run the installer without the GUI, type the command  **install.sh**  or  **install.bat** , according to the operating system in use.Independently of the execution mode, you have to provide some a few data required to correctly install and configure the product:

* first of all, you have to choose which kind of installation to execute:

  * **New Installation/Change Configuration** - used for the first installation or, very rarely, when you want to change the default installation settings \(like from portal mode to no portal mode\)

  * **Update Installation** - used after the first installation, when executing an upgrade of the already existing installation

* **database settings**, required to connect to the database schema, where the installer will create automatically all the required tables and initial data

* **company id;** it represents a 5 characters code to use to partition all data for a specific “tentant”: 4WS.Platform supports multi-tenancy, that is to say, you can run the same application for distinct organizations, each identified by a specific company id, which is used to partition data per organization

* **default language code**; 4WS.Platform supports any number of languages

* **installation path**, where Tomcat will be installed; if you want to reuse an already existing Tomcat 7 installation, you can simply specify that path and the installer will skip the Tomcat installation task and will install and configure the 4WS.Platform web application only

* **JDK path**: pay attention to this path! it is NOT the JRE path, but  **the JDK path:** if you erroneously set the JRE instead of the JDK, Tomcat will not work correctly and you will not be able to access 4WS.Platform web application; in that case, you have to delete the installation and run the installer again

* **4WS.Platform web context**; the web context is the folder name within webapps Tomcat’s subfolder where the web application will be installed; the same name will be used to connect from a browser; for instance, if you set that web context to “platform”, then the URL to specify in your browser would be: [http://host:port/platform](http://host:port/platform)

* **Run Tomcat**  A.S. and use a browser to connect to the web application; typical URL is: [http://localhost:8080/platform](http://localhost:8080/platform)

The default account to use is:  
company id: 00000  
site id: 100  
username: ADMIN  
password: admin

**It is recommended to use Chrome or Mozilla Firefox browsers** ; Internet Explorer 8 or above are also supported, but they are not optimized for javascript usage as for the other two browsers.

#### 4WS.PLATFORM INSTALLER STEPS

* **START**

  Type the following command from the shell: installgui.sh or installgui.bat.

  ![](http://4wsplatform.org/wp-content/uploads/2013/10/Install0-300x206.png)

* **SETTING DATABASE**

  Insert data of database connection.

  [![](http://4wsplatform.org/wp-content/uploads/2013/10/Install1-300x206.png)](http://4wsplatform.org/wp-content/uploads/2013/10/Install1.png)

* **SETTING CONFIG**

  Complete configuration fields for installation.

  [![](http://4wsplatform.org/wp-content/uploads/2013/10/Install2-300x206.png)](http://4wsplatform.org/wp-content/uploads/2013/10/Install2.png)

* **END**

  Enjoy 4WS.Platform.

  [![](http://4wsplatform.org/wp-content/uploads/2013/10/Install3-300x206.png)](http://4wsplatform.org/wp-content/uploads/2013/10/Install3.png)

---

#### TROUBLESHOOTING

Be careful : **avoid the installation of Tomcat in paths having a space in folders**, such as C:\Program Files

Windows operating system could have problems in recognizing the correct path.

If you are using recent versions of Windows \(Vista or next versions\), you have to use a superuser and open the prompt by right clicking on it and choose “Run as Administrator”: that is the right way to install the program. DO NOT simply execute the installer using a superuser \(e.g. administrator\), since this has not the same effect.

Moreover, pay attention to the port configured in Tomcat: in Linux/Unix O.S. you could have to change OS settings in order to allow the use of that port by Tomcat.

If the installation process was successfully completed but when you start Tomcat it terminates immediately or 4WS.Platform is not accessible, it is likely that you have specified the wrong JDK path during the installation process: it is NOT the JRE path, but**the JDK path: **in that case, you have to delete the installation and run the installer again.

**If you have changed the HTTP port in tomcat/conf/server.xml file, the URL to use in the browser to connect to 4WS.Platform changes as well.**

**If** **you are using MySQL database and it seems that every SQL command is autocommitted**, probably there is an erroneous configuration in the database schema: pay attention to the “table type” defined at table level in MySQL: MyISAM does not support transactions; if this is the table type defined for yuor tables, you have to change it to InnoDB.

#### UPGRADES

The same installing procedure can be used to apply upgrades to the product. In such a case, you have to select the second option, when executing the installer: Update Installation. Next, the already existing web context is requested. Starting from this information, the installer will apply the update to Platform web application, without changing any setting \(no changes are applied to web.xml or persistence.xml files\).

**Important note**: there could be the need for including in Platform some custom jar file, in order to invoke custom java classes.

That means that one or more jar files must be stored into **WEB-INF/lib** folder related to the Platform web context.

Since each time the installer is executed the whole content of **WEB-INF/lib **is deleted, the additional custom files will be lost. In order to avoid it, you can optionally include into your already existing web.xml file the following tag:

```html
<init-param>
  <description>Comma separated list of additional jar files added to WEB-INF/lib to not delete when updating Platform. Can be empty</description>
  <param-name>additionalResourcesJarsNotToDelete</param-name>
  <param-value>myCustomFile1.jar,myCustomFile2.jar</param-value>
</init-param>
```

Otherwise you can specify the files you want to be deleted after the update. You can optionally include into your already existing web.xml file the following tag:

```html
<init-param>
  <description>Comma separated list of additional jar files added to WEB-INF/lib to delete when updating Platform. Can be empty</description>
  <param-name>additionalResourcesJarsToDelete</param-name>
  <param-value>myCustomFile1.jar,myCustomFile2.jar</param-value>
</init-param>
```

---



