# Introduction

Archiflow is a document management software, which allows you to manage documents and automate business processes. Archiflow is available on cloud or in house. Through the integration with office automation tools, traditional and certified email, portals, ERP systems, IT protocol management solutions and digital preservation products, allows you to create Document and Process Management innovative solutions and projects.

Platform provides an integration module which allows you to connect to Archiflow, through its Rest API. 

This chapter does not cover the installation, configuration, administration of Archiflow, which is supposed to be already available.

---

# Setup

in order to communicate with Archiflow, the following data must be available:

* **Archiflow base URL**

* **Archiflow username**, used to access its repository; it is assumed that one only user is used by Platform to read/write data and documents in Archiflow; as a consequence, filters on the documents will be defined at Platform level, through business components

* **Archiflow password**, related to the specified user

* **Language**

* **Date format**

* **Domain**

Once available these settings, they can be defined in the Application Parameters, within the Platform App Designer.

After setting them, a logout and login are required, in order to make the parameters ready to use.

