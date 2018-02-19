# Form properties

For  **user tasks**  and  **start events** , it is possible to define a 4WS.Platform form containing a series of variables \(properties\). Starting from the attributes on the right of the Web Modeler editor, these variable can be defined through the "form properties" item: a popup dialog will be opened in order to set ID, NAME and TYPE for each variable; additional settings can be added as well: editability, read-only value, mandatory.  
Any of these variables can then be accessed and referred in any part of the process, using the Activiti syntax:

${PROPERTY\_NAME}

For instance, a variable containing and email address could be referred in a Mail Task, to fill in the destination address, in order to send an email.

---



