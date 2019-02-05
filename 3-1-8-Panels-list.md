# Panel definition

A user can manage already existing panels through the "**Panels list**" menu items, where there are all panels defined behind the scenes by the wizard "Add Window" or through the popup menu accessible in the window detail.  
The information available through a panel detail is split up in several folders:

* **detail panel**  – data showed here is the same defined when creating the panel. Therefore, it is always possible to change the settings for a panel
* **panel parameters**  – this folder contains two subfolders:
* **input parameters**  – a readonly list filled automatically by the Web Designer when creating the panel; the list contains all parameters required by the business component binded to the panel \(:VARIABLE…\)
* **output parameters**  – an editable list of parameters to pass to child windows; the user can define these parameters starting from variables, such as fields coming from the linked business component or other system variables \(username that identifies the logged user, current language, current date/time, etc\)
* **events**  – list of events defined by the user to link to the panel \(e.g. click on a row of the grid, a button pressed, etc.\)
* **buttons panel ** – list of buttons to add to the default toolbar; the button definition includes the following properties:

  * button text

  * icon

  * action to link to the button \(see "Events and Actions" section\)

  * position of the button within the toolbar
  * synchronous or asynchronous event, i.e. if the button is blocked or not until the events has been completed
  * flags used to define the abilitation policy for the button: enabled only when the panel is in readonly/insert/edit modes

* **other subfolders** , depending on the panel type:

  * columns list and column events for grid panels

  * controls list and control events for detail form panels

  * controls list and control events for filter panels

* **menu popup** , available for grid panels: adds a field with a linked action to the filter window opened with a right click on the same grid’s field defined for the menu popup item

---



