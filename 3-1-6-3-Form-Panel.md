# Form Panel

**In case of detail form or grid+detail form** , the form definition panel is showed; through it the user has to define settings related to the form component:

* form title \(optional, can be hidden\)
* business component \(for a single record loading\) to link to the form; the fields specified in the select clause are used to automatically create the form controls; user can then show/hide each of them, as well as define many other control settings
* form width and height
* flags to show/hide border and to set panel opacity
* flags to allow the CRUD operations, i.e. insert, update and delete \(only if the data model linked to the selected business component is writable\);
* flags to define if the window embedding the detail form must be closed after the operations of insert/update/delete
* flag to define if data loading is automatically performed when the form is showed
* initial form mode, when the form is showed; grids and forms have 3 alternative modes: readonly, insert, edit; in insert mode all controls are cleared up
* flag "copy enabled", used to show a "copy" button in the form toolbar, used to switch to insert mode the form, clear up all controls and then copy the values from the previous record to the new one
* boolean javascript expression "disable when", to disable everything when the boolean condition is true
* linked grid, used to manage some default operations, such as the grid reloading after inserting/updating the form content
* number of columns and label length, used to define the labels+controls layout; it is also possible to arrange labels and controls by specifying the x and y coordinates for each of them.
* flags "enable tag" and "enable rating" used only for detail form based on a business component that uses Alfresco service.

  **Important note:**  when defining a form panel, a linked grid should be selected; in this way, Platform can automate many operations involved with the interaction between grid and form: automatic form opening when double clicking on a grid, form loading when selecting a row in grid, grid content automatic update when saving/deleting data in the form.  
  However,  **it is also allowed not to set any linked grid when defining the form** : in that case, the form is disconnected from any other panel and the previous automatisms are not available; that means that the required input parameters for the form must be explicitelly provided by the programmer, for example when opening a window containing that form. This is relatively easy to do, by passing to the openWindowXXX\(args\) instruction the required input parameters through the args obiect.  
  If case the form \(not linked to any grid\) is  **directly opened starting from a menu item** , there aren’t any input values passed to the window containg the form; it that case, the required input parameters must be defined within the window and before the creation of the form. That means that t **he required input parameters must be defined through a javascript action linked to the "before render" event of the window** , which can be defined in the window detail form.

When creating the form, a form toolbar is automatically showed on top of it; this toolbar always includes the reload button; the other buttons \(insert, edit, delete and save/cancel\) are showed/hidden according to the flags described above.  
These buttons change the current form mode, according to the following policy:

* insert button, from readonly mode -&gt; insert mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* edit button, from readonly mode -&gt; edit mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* delete button, from readonly mode -&gt; after confirming the operation, the selected records are deleted
* cancel button, from insert/edit mode -&gt; after confirming the operation, the form is switched to readonly mode and the content reloaded
* save button, from insert/edit mode -&gt; the form is switched to readonly mode if the saving operation has been performed successfully.

---



