# Alfresco Introduction

An organization often has to manage a large number of documents, such as bills, transport documents, technical documentation, production orders and so forth. This large amount of documents would require a lower storage space and would be more easily retrieved if they were digitalized. For instance, bills coming from vendors could be scanned and converted to an electronic format, other documents could be created directly in a digitalized version, through some office applications or other information systems.  
When such a scenario occurs, there is the need to store several gigabytes of documents in an efficient way, indexing them through ad hoc criterias, which can change according to the document type.  
Moreover, they must be searched quickly and efficiently, that is to say, through specific search policies, like the navigation of a documents hierarchy, composed of categories and sub categories or by looking up documents using custom fields, such as the document title, author, creation date, etc.  
Another very helpful feature is the ability to search for a document based on its content, starting from a group of words to find inside the document.  
Finally, since that gigantic quantity of data is strategic for a company, it is essential to create a backup of it, in order to ensure the restoring of the duplicated data in case of loss of data due to hardware failures or software malfunctions.  
What just described is normally part of a system called Content Management System \(CMS\).  
Every organization should have an information system including a CMS module or, as an alternative, it should add a stand alone CMS system if it is not supported by the main I.S., since its presence allows to take advantage of what described above.  
Nowadays, several CMS solutions are available in the market, some of these are open source products which provide a significant economic saving for a company, especially for the small to middle size ones.  
One of the most popular CMS today is Alfresco, which is available also with a free edition. This product provides all of the features reported in the previous paragraphs.  
Basically, it is a Java based web application, portable on many platforms, including Windows and Linux and its user web interface allows to administer, search and manage documents both inside the company and remotelly, by simply using a web browser.  
Alfresco is composed of these main components:

* a CMS engine, through which it can store and retrieve documents
* a web interface to use to administer and look up documents
* a web services layer that allows external applications to connect to the CMS engine, without the need to use the Alfresco web interface
* a second web application, named Share, used to create ad hoc user interfaces, according to specific organization requirements, by developing the GUI and the business logic behind it; skilled Alfresco web developers are needed to create and mantain this part of the system.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadialfrescousermanual/image03.png)

The main advantages of this solution are:

* no licence costs are required, in case a company decides to choose the free Community Edition of Alfresco
* a powerful CMS engine to manage and search for documents
* a web services layer, extendable by writing additional web scripts executed through the engine; in this way, the product is very flexible and customizable.
* a fine Access Control List management \(ACL\), used to set the visibility and access level of a single document or documents folder, with the ability to restrict the access at user level or at group of users level.

However, there are a few issues involved with Alfresco Share and it is time to draw attention to them:

* creating an ad hoc user interface starting from Share is costly, because it requires a deep knowledge of the product, as long as skilled web developers to realize what needed; in addition, each time a change is required to that part of the system, an external software vendor or a developer must be engaged in order to mantain the custom part
* documents often are stored along with their metadata, which is additional information that describe the document, in terms of author, title or further structured data such as the customer code, an item code, etc,

This kind of information should be stored together with the document and they are helpful particularly when the user is searching for documents starting from these data.  
In most of the cases, this type of data is managed through other applications and it is typically stored in databases; consequently, it can be cumbersome to access this data from Share, which is connected to the rest of the Alfresco suite and has not been designed to access other systems.

---



