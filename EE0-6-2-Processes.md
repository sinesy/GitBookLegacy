# Processes

Starting from this menu item, it is possible to create new processes and show the list of already designed processes. Through this menu processes can also be started manually, along with input data required when starting the process.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiactivitiusermanual/image08.png)

A new process can be created in two alternative ways:  


* by importing a file in ‘.bpmn’ format, which defines a business process; this file can be created externaly, for instance through a stand alone designer available as an Eclipse plugin;
* by using the Activiti Modeler, included in 4WS.Platform; this modeler has a web front-end embedded in 4WS.Platform that can be used to graphically design a process and create a model; models can then be converted to active processes; all these operations can be managed internally to 4WS.Platform. 

The web modeler can be accessed starting from the list of models when choosing a model, or by pressing the new model button.  
A more detailed description of how to use the Activiti web modeler can be found in its project documentation \([http://www.activiti.org/](http://www.activiti.org/)\).

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiactivitiusermanual/image04.png)

Another way to create a new model is through the duplication of an already existing process and then use the web modeler to change the copy.  
Finally, it is always possible to create a ‘.bpmn’ file by exporting a model, for instance with the goal of creating a backup copy of the process.  
Once completed the process definition and converted the model to an active process, the process selection will show its detail, composed of the process name, version and the picture representing the process definition.  
The process detail includes also a button to start the process and optionally fill in the variables involved with the starting task.  
This variables pane is configurable through the 4WS.Platform’s App Designer, since it is managed like any other configurable panel defined within Platform.

---



