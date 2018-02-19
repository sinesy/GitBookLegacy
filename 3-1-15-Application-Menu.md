The application menu window contains:

* a tree containing all the menu folders, organized hierarchically
* a list of menu items, filtered per folder: when the user clicks on a folder, the menu items related to that folder are showed in that list.
* Menu items can be related to:
* a window to open
* a shell command to execute on the server side
* a report to show (developed using JasperReport templates)
* a URI to open on a web page
* a business component to call on the server side


![](http://4wsplatform.org/wp-content/uploads/2015/12/appMen-1024x491.jpg)

When a new window is created through the "Add window" wizard, a menu item can be created and automatically added to a special menu folder named "Others".
All the other menu item types can be created through the menu item "Application Menu".
The tree showed in this functionality reports all the already defined menu items, organized in folders.
When the user right clicks on a folder, it is possible to:

* create a new subfolder, in terms of text and folder icon
* change the text and icon of the selected folder
* remove the selected folder (children of that folder are not automatically removed, they are simply not showed)
* add a report (variables can be included for report parameters)
* create a link to an already existing custom window (a javascript file included with the distribution, created manually by a developer)
* create a link to an already existing window (created through the App Designer)
* create a link to a web page, in order to show it in a separate window
* create a command to execute on a shell on the server side.

When the user selects a node (a folder) from the tree, the menu items contained in that folder are showed in the list below the tree.
Using the drag and drop feature it is possible to move a menu item from the current folder to another one; once selecting the destination folder, a popup menu is showed to prompt the user how to manage the source menu item: copy it or move it.
The menu window contains also a combo-box to select a language from the list of defined languages: any change applied to a text for folders or menu items will be stored for the selected language only.

                

---


