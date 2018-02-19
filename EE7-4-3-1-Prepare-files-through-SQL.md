A typical scenario involving the sending of a set of files (e.g. images) from a central server to all the devices is when there is a backend application on the central site, used to define the content to send.
In this case, it is possible to use Platform to create a second (not mobile but web) application, whose front-end will be used to prepare the images/files to send to the devices linked to the first (mobile) app.
Consequently, files to send must be first upload through a grid or a detail form, where a column/control will be defined as a "File path".
This is not enough: tables CON54/55 must be filled one accordingly too. In order to do so, an action linked to the "after saving data in insert/update" event is created. The goal of that action is to fill in the two tables each time a file is uploaded. The action can have type SQL, i.e. it contains a couple of SQL instructions which will fill in CON54 (one record) and then CON55 (many records).

As an example, let’s say that there is a table named TABELLA_IMMAGINI containing the files to upload; it would have a field mapped to a column/control having type "file path". Let’s say that the field isIMAGE_PATH. In thsat case, the two SQL instructions to put into the SQL action would be:

|  INSERT into CON54_FILES_TO_SEND (APPLICATION_ID, FILE_ID, SOURCE_ID, FILE_TYPE, SHARED_FILE, FILE_NAME, ROW_VERSION, USER_ID_CREATE, CREATE_DATE, STATUS) VALUES (‘ **XXX’** ,&#8217;/ **pathToFiles** /&#8217;|| **:TABELLA_IMMAGINI.IMAGE_PATH** ,&#8217;FILE_SYSTEM&#8217;, ‘&#8230;’, &#8216;Y&#8217;,  **:TABELLA_IMMAGINI.IMAGE_PATH** , 1, &#8216;ADMIN&#8217;,  **NOW()** , &#8216;E&#8217;); INSERT into CON55_USER_FILES (APPLICATION_ID, DEVICE_ID, FILE_ID,  ROW_VERSION, USER_ID_CREATE, CREATE_DATE, STATUS)  SELECT ‘ **XXX’** , DEVICE_ID, &#8216;/ **pathToFiles** /&#8217;|| **:TABELLA_IMMAGINI.IMAGE_PATH** , 1, &#8216;E&#8217;,&#8217;ADMIN&#8217;,  **NOW()**  from CON45_SYNC_DEVICES where APPLICATION_ID=’ **XXX’**   |
| :--- |

Note that these instructions will NOT allow to upload the same file name more than once; that means that either the file name is unique or a finer SQL instruction must be defined (INSERT INTO FROM SELECT NOT IN CON54…)

Note that in case of MySQL database, it is not allowed to concatenate two strings with the || symbol: the CONCAT(field1,field2) function must be used instead.
Moreover, the current date must be defined through the database predefined function, which changes according to the database: NOW() for MySQL, CURRENT_TIMESTAMP for PostgreSQL, SYSDATE for Oracle, GETDATE() for SQLServer.

Note that the variable   **:TABELLA_IMMAGINI.IMAGE_PATH **  will be replaced at runtime with a ? and its corresponding binding value. Unfortunately, some databases do not support the user of bind variables in concat instructions; in that case, the binding mechanism must be switched off in Platform to the business component linked to the grid/form (unselect the "Use binding variables" checkbox).


                

---


