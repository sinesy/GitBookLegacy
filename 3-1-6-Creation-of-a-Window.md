# Creation of a window

Once a data model has been defined and one or more business components related to that model have been created, all ingredients needed to fill in a panel are available.  
Basically, a window is composed of panels, at least one. There are several types of panels: grid, detail form, grid+detail form in the same window, image panel, map panel, tree, filter panel linked to a grid.  
In order to simplify and speed up the process of window creation, a wizard is available starting from the menu bar: UI -&gt; Windows -&gt; New window  
Alternatively, you can choose Application -&gt; New functionality and follow the wizard until the last step: Window creation.  
The result is the same: a form where defining the window settings:

![](http://4wsplatform.org/wp-content/uploads/2015/12/newWindow-1024x445.jpg)

When the user selects this item, a wizard is prompted to the user to specify the window settings, which are:

* window title
* dynamic part of the title – this final part of the title includes variables expressed as :VARIABLENAME that will be replaced at run-time with their values; in this way, for instance, it is possible to pass forward from one window to the next one some information, such as the customer name or the document number, etc. coming from the previous window
* window width and height
* window maximized – flag used to maximize the window size, in case the menu layout is compatible with this setting, that is to say, no tabs layout
* create menu item too – in addition to the window creation, a menu item is also added to "Other" menu subfolder and link to the window
* window icon
* one instance only – flag used to define if there can be one only instance of the window opened
* note – optional information about the window, not showed at run-time.

The Next step is the selection of the panel type to embed inside the window.  
After the window creation, it is always possible to manage the window and add/remove or arrange other panels.  
Therefore, the wizard always creates one only panel inside the window, except for two cases: grid + detail form and filter pane + grid.  
The next wizard panes to show depend on the panel type chosen by the user.  
In the following sections, a specific panel type is described, with its own properties and behavior.

**Window content**  
Once you have created a window and at least one panel, you can access to its content through the “Panels” folder:

![](http://4wsplatform.org/wp-content/uploads/2018/01/winpanels.png)

This folder is split up in 3 main areas:

* on the left there is a  **hierarchical representation of the window content** , in terms of panels composing the window; each panel is represented by a node of the tree, where the icon represents the panel type \(grid, form, folder container, etc.\) and the name reports the panel id
* on the top right part there is the  **property inspector of the selected node**  in the tree: when clicking on a node in the tree, you can see the main properties for the panel, related to its position in the window; you can quickly change these properties by pressing the Edit button on the “Properties panel for Window”. As an alternative, you can always access to the panel detail by double clicking the node in the tree or by right clicking on the node and choose “Show panel details” \(only when the tree is in readonly mode\).
* on the bottom right part of the window, there is a  **Preview**  of the whole window. Every time you click on a node of the tree the corresponding panel is highlighted in the Preview panel; every time a panel in the Preview is clicked, the corresponding node in the tree is selected. This is very helpful to speed up the search for a specific panel, starting from its visual position in the window. Note that there is a preview also for Form and Filter panel, which allows you to edit graphically the content for these panels: you can access to it, starting from the detail of the panel.

It is possible to change the content of this window by switching to edit mode the tree on the left: when pressing the Edit button on top of the tree, a popup menu is available at node level. The content of such a popup menu changes according to the selected node.  
When clicking on a panel you can always:

* **remove it**  from the window \(Remove panel from window\)
* **change its position**  with respect to its panel container \(Set panel location\)

In case of a panel which is a panel container, that is, a panel which can contain additional content, there is also an Add command through which you can add any other kind of panel.

**Panel containers and layouts**  
Platform supports a variety of different  **panel containers** , each managing the layout of its children panels in a different way:

* tab panel
* alternative panes
* accordion panel
* vertical orientation panel
* horizontal orientation panel
* table panel
* generic panel

Each of them is described as follow.  
Note: you can easily change the current panel container with another one, without having to remove its content and then remove it: the commands “Replace this panel with…” allow you to replace the current panel container with any other.

**Tab panel**

![](http://4wsplatform.org/wp-content/uploads/2018/01/folders.png)

This container allows to include any number of sub-panels, as folders. Each panel title will be used to set the corresponding panel title. You can change the position of a specific folder \(panel\), through the drag ‘n drop the corresponding node and move it to another position in the tree.

**Alternative panels**  
This container allows to include any number of sub-panels, but only one at a time is shown. All the others can be shown alternatively. The only way to select which sub-panel to show is by using javascript. Consequently, you have to set a GUI event \(e.g. a button click\) and link to it a client-side javascript action, through which selecting the sub-panel to make visible.  
The javascript method you can use to set the sub-panel to show is:  
setActiveItem\(yourPanelContainerId,subPanelIndex\);

**Accordion panel**  
This container allows to include any number of sub-panels, organized vertically like an accordion, where all panels are collapsed but one, which is the one expanded. All sub-panels are identified by their panel title. When clicking on a panel title in the accordion panel container, it is possible to expanded the corresponding sub-panel and make all the others collapsed.

**Vertical orientation panel**

![](http://4wsplatform.org/wp-content/uploads/2018/01/vert.png)

This container allows to include any number of sub-panels, organized vertically. Each sub-panel will occupy exactly the same height, which is distributed equally among all the sub-panels.

**Horizontal orientation panel**

![](http://4wsplatform.org/wp-content/uploads/2018/01/hor.png)

This container allows to include any number of sub-panels, organized horizontally. Each sub-panel will occupy exactly the same width, which is distributed equally among all the sub-panels.

**Table panel \(responsive layout\)**  
This container allows to include any number of sub-panels, organized with different  **widths** ,  **heights**  and  **row/column spans** .  
This is the most flexible layout and also the most complex to configure.  
It allows to organize sub-panels in a way that they can use all the available space. Moreover, with different display sizes or when resizing the browser window, the organization of the panels can change. At panel container level, it is possible to set the maximum number of columns allowed: the content of the container will be then calculated at run-time, according to the available space.

For example, suppose you set the table panel container with a max nr of column = 2 and that you have 3 panels to add: the first is a filter panel having a fixed width and height of 400 pixels, the second panel is a grid \(a component having a dynamic width\), the third panel a detail form, again with afixed width and height of 400 pixels.  
With these settings, if your browser has a length of 1000 pixels could easily show the filter and grid in the first row and the detail form in the second. But when reducing the browser window to less than 400 pixels, the grid would automatically moved to the second row, along with the detail form.  
That behavior is what usually is called a responsive layout: a container whose content can be re-organized automatically, according to the current available space.

![](http://4wsplatform.org/wp-content/uploads/2018/01/table.png)

It is essential to understand how to definecorrectly a table panel. At panel level there is a  **Nr of columns**  property to set.  
For every sub-panel, you have to define an  **Height** .  
For every sub-panel which does not have a dynamic width \(panels having a dynamic width are grids and charts\), you have to define a  **Width**  as well, otherwise it will not be possible to render it correctly.  
Optionally, for every sub-panel you can define also the  **Column span** , i.e. the number of cells that the panel has to occupy horizontally.  
Optionally, for every sub-panel you can define also the  **Rows span** , i.e. the number of cells that the panel has to occupy vertically.  
Thanks to all these settings, you can arrange the window content in a very flexible way.  
Please pay attention to the mandatory properties reported above: if you have not set them, the window content will not be rendered correctly, when executing the web application.

**Generic panel**  
This container allows to include up to 5 sub-panels, each in a specific region.  
Five regions are supported:

* **top**  – a sub-panel is shown on the top of the container, having a fixed height \( **Height**  is a mandatory property for that sub-panel\); it will expand itself horizontally
* **center**  – a sub-panel is shown in the central part of the container and it will use all the available space
* **bottom**  – a sub-panel is shown on the bottom of the container, having a fixed height \( **Height**  is a mandatory property for that sub-panel\); it will expand itself horizontally
* **left**  – a sub-panel is shown on the left of the container, having a fixed width \( **Width**  is a mandatory property for that sub-panel\); it will expand itself vertically
* **right**  – a sub-panel is shown on the right of the container, having a fixed width \( **Width** is a mandatory property for that sub-panel\); it will expand itself vertically

![](http://4wsplatform.org/wp-content/uploads/2018/01/border.png)

There must be at least one sub-panel, arranged automatically in the center region.  
This is also the default layout for the window \(the root node in the tree\) and it cannot be changed.

---



