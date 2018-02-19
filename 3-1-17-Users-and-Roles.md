# Working with users and roles

Both the App Designer and the Interpreter support users and roles.  
The default implementation for authentication and authorizations provided with 4WS.Platform includes the definition of users, roles, associations between user and roles.  
In alternative, an organization can create its own implementation covering these topics, by implementing a few interfaces that decouple the product from this pluggable implementation.  
Through the " **Roles** " menu item, it is possible to define a role, meant as a set of functionalities with related authorizations.  
When double clicking on one of this functionality, a detail window appears: it can be used to define authorizations for the panels contained within the window represented by that functionality.  
Authorizations can be defined at grid or from level, if needed.

![](http://4wsplatform.org/wp-content/uploads/2015/12/roles-1024x520.jpg)

More in general, authorizations cover several topics:

* enabled  **menu items** , i.e. the ones showed in the application menu
* for each  **grid**  included in a window opened starting from a menu item, the grid toolbar can be defined in terms of habilitations for the insert, edit, delete buttons; in this way it is possible to disable these operations through roles
* for each  **detail form**  included in a window opened starting from a menu item, the form toolbar can be defined in terms of habilitations for the insert, edit, delete buttons; in this way it is possible to disable these operations through roles
* starting from an enabled grid, it is possible to set the habilitations for its  **columns**  \(only if the "enable profile and permissions" flag in column grid has been enabled\), in terms of:

* columnvisibility

* habilitation in insert
* habilitation in edit
* mandatory

Through the " **Users** " menu item, it is possible to define a user, in terms of:

* username
* password
* optional expiration date
* language identifier associated to the user
* user description
* flag to lock the account

![](http://4wsplatform.org/wp-content/uploads/2015/12/users-1024x519.jpg)

Once defined one or more roles and users, it is possible to associate one or more roles to the user, through the user roles grid.  
Since a user can have more than one role, these roles can have conflicts: one role could disable a function and the other could enable the same functionality; in that case the conflict resolution policy makes enabled such a function.  
By means of "Users" and "Roles" it is possible to define authentication and authorizations data.  
The first set of data is used when authenticating users; authentication will be successfully completed if:

* the provided credentials are correct \(username and password\)
* the user has not an expiration date set or the account is not yet expired
* the user has at least one role associated and that role has at least one function enabled

Once authenticated, the application menu will include only the menu items enabled according to the roles binded to the user.  
 **Note** : 4WS.Platform has a strong security policy which does not allow the invocation of Ajax requests to the server side without an authentication process. Moreover, only requests related to functionalities enabled for the user will be processed. For instance, if the user can access to a function but he is not granted for change data, any request involving a change to data will be rejected.

---



