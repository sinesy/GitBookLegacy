# Windows list

Once a window has been created, it can be arranged in terms of content.  
You can see all the created windows from the menu entry

![](http://4wsplatform.org/wp-content/uploads/2015/12/windowList-1024x490.jpg)

And a new feature allows you to see how windows are related to each other by clicking on  **Windows Schema**

![](http://4wsplatform.org/wp-content/uploads/2015/12/windowSchema-1024x515.jpg)

The window content includes a set of panels, which can be: grids, detail forms, trees, image panels, map panels, custom panel.  
A user can manage these panels through the "Panels list" menu items, where there are all panels defined behind the scenes by the wizard "Add Window".  
Moreover, the user can create additional panels from the detail of an already existing window.  
The window detail contains several folders:

* **window settings**  – these settings are the same the user had defined when creating the window through the window wizard
* **input parameters ** – optional parameters list, required by business components or other parts of the window \(panels, window title, panels title, etc.\) and passed by the parent window
* **panels**  – a hierarchical representation of the window, in terms of panels and subpanels.

![](http://4wsplatform.org/wp-content/uploads/2015/12/windowDetail-1024x486.jpg)

The window container has always a layout that requires at least one panel at center \(which will be streched in all direction, by occupying the whole window container\).  
Up to 5 panels can be added to that container, using these regions: left, right, top, bottom, center. For panels added to left or right the panel width is required. For panels added to top or bottom the panel height is required.  
A pane can be a container or a data panel.

Supported containers are:

* a  **subpanel \(generic panel\)**  – having the same layout of the window container \(up to 5 panels\), so you can arrange any number of panels in the end, through nested panels
* a  **folder container**  – it contains a set of folders, where a folder can be any kind of panel. The user can show any of these folders by clicking on the folder title. Additional javascript methods are available in order to programmatically show any folder, through the following method:

  **setActiveTab\(‘folderContainerIdentifier’,panelIndex\);**  
  Moreover, a specific folder can be showed/hidden through the following method:  
  **setVisibleTab\(‘folderContainerIdentifier’,panelIndex,true\|false\);**  
  Finally, a specific folder can be enabled/disabled through the following method:  
  **setEnableTab\(‘folderContainerIdentifier’,panelIndex,true\|false\);**

* a **vertical folder container**, working like the previous one, but tabs are arranged vertically

* an ** accordion panel**  – which is a special kind of panel where any number of panels can be added to it, but only one of them can be showed at a time; the first added subpanel is the one showed at the beginning; any other subpanel can be showed by simply clicking on its title: all other subpanes are minimized and the one just clicked will be maximized. Any other subpanel can be showed and replace the previous one, also by executing a special javascript method which can be invoked from a js action; the method is accessible from within the window and has the following signature: **setActiveItem\(“accordionPanelIdentifier”,panelIndex\);**

* a  **card panel** – which is a special kind of panel where any number of panels can be added to it, but only one of them can be showed at a time; the first added subpanel is the one showed at the beginning. Any other subpanel can be showed and replace the previous one, only by executing a special javascript method which can be invoked from a js action; the method is accessible from within the window and has the following signature:

```js
setActiveItem("cardPanelIdentifier",panelIndex);
```

* a **vertical/horizontal panel**, where the content is arranged either vertically \(1 only scrollable column\) or horizontally \(1 only scrollable row\)
* a** responsive container \(table layout\)**, where the content is arranged from left to right, top to bottom and each element can have a weight potentially different from the others and can have a prefixed height or width. According to the avilable space in  the web page \(browser size\), elements are then arranged and moved in order to occupy the available space without the need for an horizontal bar.

Data panels can be included in any container. Supported data panels are:

* a  **grid, **supporting both read and write operations \(CRUD operations\)
* a  **pivot grid, **a special type of grid, where 2 kinds of fields are managed in a special way: \(i\) a numeric field \(grouping field\) is spread along multiple columns, where each column represents a value for a second field \(identifying field\)
* a ** filter panel**  linked to a grid
* a ** detail form, **supporting both read and write operations \(CRUD operations\)
* an **editable panel**, which is not connected to any data source \(as for a detail form\), used to manage volatile data
* a **tree** 
* a **preview panel, **which can be used to show an image, a document like a PDF, etc.
* an **image gallery**, containing a set of images, spread horizontally \(up to N predefined columns\) and along the vertical axis
* a ** map panel** 
* a **tree+grid panel**, working as a tree, where all data but the first field is arranged in a grid: expanding the value for the first field in the tree, leads to show all other data in the grid row \(helpful for instance when showing a BOM\)
* a ** custom panel** , based on a javascript file, created by a programmer and uploaded together with 4WS.Platform, that will be automatically included within the window.

When the user presses the edit button in the "Panels" folder of the window detail, it is possible to access to a popup menu through right click of the mouse on a tree node. The popup menu content is dynamic and depends on the clicked node: it allows to add subpanes or any other panel types, with these exceptions:

* you cannot add a filter panel if there is not a grid
* you cannot add a subpanel or a folder container to a grid/filter/form/tree/map/image panel

Furthermore, The user can remove panels, rearrange them, change the position \(region\) of the panel, change width/height of a panel.

---



