# Application Metadata Management

Everything that has been configured via the App Designer can be exported in a zip file.  
In order to do that, you have to use the Application -&gt; Import/Export application menu item.  
This window allows to import/export files \(web content\) and import/export metadata. In this section, the import/export of metadata is described in detail.

![](http://4wsplatform.org/wp-content/uploads/2018/01/importmeta-1.png)

**Exporting metadata**   
The export operation is very simple: you have just to press the  **Export**  button: everything will be exported, including environment-related settings, such as parameters \(LDAP settings, Email servers, etc.\), directory paths, additional datasources \(database connections\).  
When pressing the Export button, a .zip file will be generated and the user can save it locally.

**Importing metadata**   
Metadata import can be carried out by choosing in the “Application to upload” input field the .zip file to upload.  
There are a few settings that can be refined when importing metadata:

* **Delete old data**  – it is recommended to let it checked; in this way, the current metadata will replace the previous one and will logically delete any old content
* **Company id to use in import**  – in case of a multi-tenancy environment, composed of multiple company ids, you can decide which company id to use when importing metadata; in this way, you could import changes to users and roles for a specific company; note that this setting can be dangerous to use, since in a multi-tenancy installation, all company ids should behave in the same way, in terms of metadata, therefore it would make sense to check the next setting:
* **Copy for all companies** – copy the imported metadata for all the company ids defined in this installation; it is recommended to check it for a multi-tenancy environment
* **Progressives**  – usually, this checkbox can be unselected: if checked, all internal counters defined within the .zip file will be reported in the current environment. Normally this is not a good idea, since different environment should have different counters, so that there will be never overriding of values and conflicts due to them
* **Roles**  –usually, this checkbox can be unselected: if checked, the user roles \(i.e. authorizations\) defined in the environment where the .zip has been created will be reported in the current environment. Normally, this is not needed, since different environments could have different roles: a production environment could have a variety of roles not needed and not defined in the dev environment
* **Users**  –usually, this checkbox can be unselected: if checked, the users defined in the environment where the .zip has been created will be reported in the current environment. Normally, this is not needed, since different environments could have different users: a production environment could have a number of users not needed and not defined in the dev environment
* **Custom translations**  – when defining translations, these are defined at application level. Just in case of a product to deploy in different environments for different clients, it could be helpful to distinguish and maintain ad hoc translations at client level. These custom translations can be defined in a specific environment, so it should not be needed to import them from the dev environment and, consequently, this checkbox can remain unselected
* **Mobile theme**  – when defining a theme for a mobile app \(images, colors, fonts, etc.\) these are defined at application level. Just in case of an app to deploy in different environments for different clients, it could be helpful to distinguish and maintain ad hoc themes at client level. These themes can be defined in a specific environment, so it should not be needed to import them from the dev environment and, consequently, this checkbox can remain unselected.

Once pressed the  **Import Application**  button, a comparison is performed between the metadata to import and the metadata currently defined in the current environment and to replace.  
The comparison is only about a fewenvironment-related settings:

* ** application parameters**  \(e.g. LDAP settings, Email servers, etc.\)
* **global parameters ** 
* **directory paths** 
* ** additional datasources**  \(database connections\)
* **scheduled processes**  \(timing, suspension, etc\)
* **templates**  \(email templates\)

Differences can be managed automatically or require a manual decision:

* **new records are automatically imported**  \(e.g. new scheduled processes, new additional datasources, new parameters\); that means the user maybe has to change their values after the import activity, since their value could depend on the environment
* **changes to a datasource related to the only title are automatically imported** 
* **changes to a directory related to the only title are automatically imported** 
* **changes to a template related to the only title are automatically imported** 
* **all the other changes will be prompted**  and require a manual decision

All differences found which require a manual decision will be reported. For each difference, a table composed of two lines is shown:

* the first line is about the values contained in the current environment
* the second line is about the metadata di import, stored in the .zip file

Data changes are grouped per topic \(global parameters, scheduled processes, etc.\) and highlighted in yellow, so that the user can easily identify what the change is about.

![](http://4wsplatform.org/wp-content/uploads/2018/01/importchecking-1.png)

For each change, the user can decide if import it or skip it. That operation is defined through the checkbox on the left of each change. The default setting is to import it \(check selected\).  
When pressing the  **Import Application**  button, all metadata will be imported, except for the settings prompted above, which has not been selected.

**Datasources activation**   
Once completed the import task, Platform will prompt the user about the  **re-activation of the datasources** , in case of changes with them or in case of new datasources.

**Comparison between Objects and Tables**   
This feature can be started at the end of the import process or manually, when pressing the  **Verify objects**  button.  
This checking consists of **comparing the definition of the imported objects**  \(data models\) with the corresponding database tables defined in the databases \(defined through the additional datasources.\)  
This checking comes in handy when there could be a misalignment between the database in the previous environment \(e.g. dev env\) and the current environment, for example because some fields are missing in tables.  
Such a scenario would lead to a wrong operation of the application and it should never happen. Platform can help identifying this possibility, by executing a comparison between what defined and expected at objects level, with what actually defined in the database.  
The starting point is based on the list of all defined objects: the checking can be applied to all objects or part of them:

![](http://4wsplatform.org/wp-content/uploads/2018/01/checkfields-1024x598.png)

For each object, it is possible to narrow or wide the checking to all datasources or a subset of them.  
The result of this comparison is a list of tables+fields which are missing the current database, somewhere in any datasource. The comparison is only limited to missing fields in the destination database: neither check constraints nor field length/types are taken into account during the comparison.

![](http://4wsplatform.org/wp-content/uploads/2018/01/checkfields2-1024x599.png)

The user can limit the comparison of objects to a subset of all defined datasources, at object level.

Once identified the missing fields, the user can optionally force the creation of these fields in the specified datasources. This operation is not recommended: it would be better to upgrade the database through a set of SQL scripts created for that purpose and not let Platform fix a misalignment problem created in the past. This optional operation is intended as a way to by-pass a blocking condition where there is no time to apply a better upgrade through a standard shared mechanism.

---



