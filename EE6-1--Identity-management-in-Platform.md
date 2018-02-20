# Identity management in Platform

4WS.Platform can work on premise or installed in the cloud.  
In both cases, a Platform web application is based on a relational database to store metadata and data.  
Users are always stored in the Platform respository, since user  **authorizations**  are tightly coupled with a specific application and its functionalities. Consequently, users must be defined too in the same repository,  so that it is possible to link authorizations \(roles\) to users.  
The  **authentication**  process, which is different from the user authorizations, can be managed internally to Platform \(i.e.  **user credentials**  can be defined in the Platform repository\) or can be delegated to an external identity system, such as the  **Google Authentication**  or the authentication based on an  **LDAP**  server, like Microsft Active Directory.  
All these identity processes can cohexist together, by definying an ** authentication chain** , where the enabled authentication systems are defined in sequence: when logging on, the user credentials are checked out in the first authentication system, if not recognized, the credentials are checked out in the next authentication system, until the end of the authenticaion chain.  
In this way, it is possible for instance to check out credentials for users defined in the organization’s LDAP, for all the employees, and to check out all other users \(external users, such as clients, suppliers, etc.\)  in the Platform local repository.  
In case of an authentication forwarded externally, a synchronization process is needed to import on a regular basis all the users, so that these users can then be linked to authorizations.

In the next sections, a series of different scenarios are described, according to the external authentication system to connect; the configuration settings needed are reported as well.

---



