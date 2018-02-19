**Creating an editable grid**
A window composed of a single grid can be created through the following steps:

* select &#8220; **Data Model** &#8221; -&gt;  **Add Objects to Database** &#8220;
*  **select the table**  related to the content to show on grid; if multiple tables are needed to show the right content on the grid, select all of them; some of the tables could have been already selected in the past, so here you can only select tables which have not been chosen yet
* press the &#8220; **Generate** &#8221; button on the right bottom area
* once created the object, two additional business components have also been created; one of them can be used to feed a grid: select &#8220; **Objects and relations** &#8221; and select the object just created; in case data to show on grid requires the access to multiple tables, press the &#8220; **New** &#8221; button on the &#8220; **Relations** &#8221; section and  **add any relationship needed, ** then press ** &#8220;Save&#8221;** 
* choose the &#8220; **Business Components** &#8221; tab in the object detail window and select the business component related to a list of data and

* press the &#8220; **Edit** &#8221; button to change setttings
* click on the &#8220; **Relations** &#8221; subfolder and check the relationships required for that business component
* in the main subfolder, set the  **WHERE**  condition as needed, then press &#8220; **Save** &#8220;


* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Add Window** &#8221; to access to the window creation wizard, set the  **window title** , an  **icon**  and press &#8220; **Next** &#8221; button on the right bottom area
* select the &#8220; **Grid** &#8221; widget andpress &#8220; **Next** &#8221; button on the right bottom area
* set the  **business component ** to feed the grid, i.e. the one just configured
* press the &#8220; **Generate** &#8221; button on the right bottom area

At this point, the window containing the grid has been created and it is ready to be used.
You can access at any time the grid settings and change them, through the&#8220;Application Management&#8221; -&gt; &#8220;Windows&#8221; menu item: once opened the window settings, choose the &#8220;Panels&#8221; subfolder and double click on the grid component showed in the hierarchical representation of the window content.
Note that you are not allowed to change the business component previously binded to the grid: you can still change the current business component content anyway.

 **Creating a readonly grid + detail form in the same window** 
A window composed of a read onlygrid + detail form can be created through the following steps:

* select &#8220; **Data Model** &#8221; -&gt;  **Add Objects to Database** &#8220;
*  **select the table**  related to the content to show on grid/detail; if multiple tables are needed to show the right content on the grid/form, select all of them; some of the tables could have been already selected in the past, so here you can only select tables which have not been chosen yet
* press the &#8220; **Generate** &#8221; button on the right bottom area
* once created the object, two additional business components have also been created; one of them can be used to feed a grid, the other to fill in the detail form: select &#8220; **Objects and relations** &#8221; and select the object just created; in case data to show on grid/form requires the access to multiple tables, press the &#8220; **New** &#8221; button on the &#8220; **Relations** &#8221; section and  **add any relationship needed, ** then press ** &#8220;Save&#8221;** 
* choose the &#8220; **Business Components** &#8221; tab in the object detail window and select the business component related to a list of data and

* press the &#8220; **Edit** &#8221; button to change setttings
* click on the &#8220; **Relations** &#8221; subfolder and check the relationships required for that business component
* in the main subfolder, set the  **WHERE**  condition as needed, then press &#8220; **Save** &#8220;


* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Add Window** &#8221; to access to the window creation wizard, set the  **window title** , an  **icon**  and press &#8220; **Next** &#8221; button on the right bottom area
* select the &#8220; **Grid and detail** &#8221; widget andpress &#8220; **Next** &#8221; button on the right bottom area
* set the  **business component ** to feed the grid, i.e. the one just configured; here you have to ** unselect the checkboxesrelated to &#8220;can insert&#8221;, &#8220;can update&#8221;, &#8220;multiple update&#8221; and &#8220;can delete&#8221;** ; the latter could be let selected, in case you want to allow the deleting operation from the grid
* press &#8220; **Next** &#8221; button on the right bottom area
* set the  **business component ** to feed the detail form
* press the &#8220; **Generate** &#8221; button on the right bottom area

At this point, the window containing the grid and form has been created and it is ready to be used.
You can access at any time the grid or form settings and change them, through the&#8220;Application Management&#8221; -&gt; &#8220;Windows&#8221; menu item: once opened the window settings, choose the &#8220;Panels&#8221; subfolder and double click on the grid or form component showed in the hierarchical representation of the window content.
Note that you are not allowed to change the business component previously binded to the grid or form: you can still change the binded business components content anyway.

 **Adding a detail form to an already existing window containing a grid** 
If you have already created a window containing a grid, you can still add to the same window a detail form binded to the grid, through the following steps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the already existing window containing the grid, choose the &#8220;Panels&#8221; subfolder and double click on the grid
* here you can change the grid settings, in order to make it a readonly grid, since now the editing will be moved to the detail form to create, so there is not any more need for editing data in grid. If the grid is already a readonly grid, skip this step; to make a grid a readonly grid,  **unselectthe checkboxesrelated to &#8220;can insert&#8221;, &#8220;can update&#8221;, &#8220;multiple update&#8221; and &#8220;can delete&#8221;** ; the latter could be let selected, in case you want to allow the deleting operation from the grid
* in the &#8220; **Panels** &#8221; subfolder of the window settings, press the &#8220; **Edit** &#8221; button and right click on the root node
* in the popup menu showed, choose the &#8220; **Add detail form** &#8221; menu item
* within the small dialog opened,  **press the + button** to create a new detail form
* set the  **business component ** to feed the form and be sure to  **select the &#8220;binded grid&#8221;** , i.e. the one already included in the same window
* press &#8220; **Save** &#8221; button on the right bottom area to close the detail form window creation
* select the &#8220; **position** &#8221; of the detail form and its  **height**  (e.g. 200 pixels)
* press the &#8220; **Save button** &#8221; to complete the detail form creation and add it to the window
* press the &#8220; **Save** &#8221; buttonabove the tree and store these settings permanently

At this point, the window contains boththe grid and formandit is ready to be used.
You can access at any time the grid or form settings and change them, through the&#8220;Application Management&#8221; -&gt; &#8220;Windows&#8221; menu item: once opened the window settings, choose the &#8220;Panels&#8221; subfolder and double click on the grid or form component showed in the hierarchical representation of the window content.
Note that you are not allowed to change the business component previously binded to the grid or form: you can still change the binded business components content anyway.

 **Creating a window containinga detail form and attach it to analready existing window containing a grid** 
If you have already created a window containing a grid, you can create a secondwindow with a detail form binded to the grid, through the following steps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Add Window** &#8221; to access to the window creation wizard, set the  **window title** , an  **icon**  and press &#8220; **Next** &#8221; button on the right bottom area
* select the &#8220; **Detail** &#8221; widget andpress &#8220; **Next** &#8221; button on the right bottom area
* set the  **business component ** to feed the form and **select the &#8220;binded grid&#8221;** ,i.e. the one included in the firstwindow
* press &#8220; **Save** &#8221; button on the right bottom area to close the detail form window creation

At this point, the window contains boththe grid and formandit is ready to be used.
You can access at any time the grid or form settings and change them, through the&#8220;Application Management&#8221; -&gt; &#8220;Windows&#8221; menu item: once opened the window settings, choose the &#8220;Panels&#8221; subfolder and double click on the grid or form component showed in the hierarchical representation of the window content.
Note that you are not allowed to change the business component previously binded to the grid or form: you can still change the binded business components content anyway.

 **Adding a gridto an already existing window containing a grid** 
If you have already created a window containing a grid, you can still add to the same window a second gridbinded to the first one, through the following steps:

* be sure you have already an object and  **business component to bind to the second grid** ; that business component should contain a filtering condition in the WHERE clause having a bind variable (e.g. FIELD = :VARIABLE)
* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the already existing window containing the grid, choose the &#8220;Panels&#8221; subfolder and double click on the grid
* in the &#8220; **Panels** &#8221; subfolder of the window settings, press the &#8220; **Edit** &#8221; button and right click on the root node
* in the popup menu showed, choose the &#8220; **Add grid** &#8221; menu item
* within the small dialog opened,  **press the + button** to create a newgrid
* set the  **business component ** to feed the second grid and unselect the &#8220;autoload data&#8221; checkbox, since the second grid would be loaded when selecting a row in the first grid
* press &#8220; **Save** &#8221; button on the right bottom area to close the detail form window creation
* select the &#8220; **position** &#8221; of the gridand its  **height**  (e.g. 200 pixels)
* press the &#8220; **Save button** &#8221; to complete the gridcreation and add it to the window
* press the &#8220; **Save** &#8221; buttonabove the tree and store these settings permanently
* the last step is to force the second grid reloading when selecting a row in the first grid: open the settings related to the first grid and select the &#8220; **Wizards** &#8221; combobox in that pane; choose &#8220; **Load grid when selecting a row&#8221;** , then select the second grid a bind the right fields needed to correctly load the second grid:  **select in the combobox the table related to the first grid**  and choose the field/fields to bind to the variables declared in the business component of the second grid.

At this point, the window contains the two gridsandit is ready to be used.
You can access at any time the two gridsand change them, through the&#8220;Application Management&#8221; -&gt; &#8220;Windows&#8221; menu item: once opened the window settings, choose the &#8220;Panels&#8221; subfolder and double click on one of the grids showed in the hierarchical representation of the window content.
Note that you are not allowed to change the business component previously binded to a grid: you can still change the binded business components content anyway.

 **Creating a window containinga gridand attach it to analready existing window containing a grid** 
If you have already created a window containing a grid, you can create a secondwindow with a gridbinded to the first grid, through the following steps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Add Window** &#8221; to access to the window creation wizard, set the  **window title** , an  **icon**  and press &#8220; **Next** &#8221; button on the right bottom area
* select the &#8220; **Grid** &#8221; widget andpress &#8220; **Next** &#8221; button on the right bottom area
* set the  **business component ** to feed the grid
* press &#8220; **Save** &#8221; button on the right bottom area to close the detail form window creation

At this point, the two windows areready to be used and connected to each other.
You can access at any time the two grid settings and change them, through the&#8220;Application Management&#8221; -&gt; &#8220;Windows&#8221; menu item: once opened the window settings, choose the &#8220;Panels&#8221; subfolder and double click on the grid showed in the hierarchical representation of the window content.
Note that you are not allowed to change the business component previously binded to agrid: you can still change the binded business components content anyway.


 **Setup an enumeration of values (static combobox) for a grid column** 
If you have already created a grid and need to define a column having a fixed enumeration of values, you have to use a static combobox. In order to do that, you have to followthesesteps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Code Selectors** &#8221; and press the &#8220; **New** &#8221; button, in order to define a new code selector for the static combobox
* choose &#8220; **Static combo box** &#8220;, set a descriptionfor it and press the &#8220; **Next** &#8221; button at the right bottom area
* in the table showed, ** definethe enumeration,**  in terms of a list of couples: the first is the code (not showed) the second is the description to show in the combobox
* once completed this task, press the &#8220; **Save** &#8221; button to confirm the operation
* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the already existing window containing the grid, choose the &#8220; **Panels** &#8221; subfolder and  **double click on the grid** 
* in the second folder &#8220; **Grid columns** &#8220;, press the &#8220; **Edit** &#8221; button and select the row related to the column where you want to set the combobox
*  **change the column type to &#8220;static combo box&#8221;** 
*  **set the code selector**  just defined in the column at the right of the column type
* press the &#8220; **Save** &#8221; button to confirm the settings.

At this point, the grid will use the combobox to decode the codes and show the code description instead.
You can change at any time the codes or descriptions for the code selector by selecting it on &#8220;Code Selectors&#8221; menu item.

 **Setup a dynamic enumeration of values (remotecombobox) for a grid column** 
If you have already created a grid and need to define a column having a dynamicenumeration of values, coming from database tables, you have to use a static combobox. In order to do that, you have to followthesesteps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Code Selectors** &#8221; and press the &#8220; **New** &#8221; button, in order to define a new code selector for the remotecombobox
* choose &#8220; **Remotecombo box** &#8221; and set a descriptionfor it
* select the business component to bind to that combobox
* select the field to use for the code; the proposed fields come from the SELECT clause defined in the business component
* press the &#8220; **Next** &#8221; button at the right bottom area
* select the field to use for the description to show in the items list of the combobox
* once completed this task, press the &#8220; **Save** &#8221; button to confirm the operation
* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the already existing window containing the grid, choose the &#8220; **Panels** &#8221; subfolder and  **double click on the grid** 
* in the second folder &#8220; **Grid columns** &#8220;, press the &#8220; **Edit** &#8221; button and select the row related to the column where you want to set the combobox
*  **change the column type to &#8220;remote combo box&#8221;** 
*  **set the code selector**  just defined in the column at the right of the column type
* press the &#8220; **Save** &#8221; button to confirm the settings.

At this point, the grid will use the combobox to decode the codes and show the code description instead.
Important note: do not use a remote combobox to show a large amount of data, since the combobox is not a suitablecomponent to use with thousand of data; with high volume of data to show, use a lookup component instead.

 **Setup a lookup cod+buttonfor a grid column** 
If you have already created a grid and need to define a column having a lookup component,followthesesteps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Code Selectors** &#8221; and press the &#8220; **New** &#8221; button, in order to define a new code selector for the lookup component
* choose &#8220; **Code+button lookup** &#8221; and set a descriptionfor it
* select the business component to bind to thatcomponent
* select the field to use for the code; the proposed fields come from the SELECT clause defined in the business component
* press the &#8220; **Next** &#8221; button at the right bottom area
* once completed this task, press the &#8220; **Save** &#8221; button to confirm the operation
* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the already existing window containing the grid, choose the &#8220; **Panels** &#8221; subfolder and  **double click on the grid** 
* in the second folder &#8220; **Grid columns** &#8220;, press the &#8220; **Edit** &#8221; button and select the row related to the column where you want to set thelookup
*  **change the column type to &#8220;code+button lookup&#8221;** 
*  **set the code selector**  just defined in the column at the right of the column type
* press the &#8220; **Save** &#8221; button to confirm the settings.


Optionally, you can also set a series of additional columns to automatically fill in, when choosing a code from the lookup component: the values for these columns would come from the SELECT clause of the business component linked to the lookup. In order to preset the column values, press the &#8220;Edit&#8221; button in the &#8220;Grid Columns&#8221; subfolder, choose the row related to the lookup and press the lens button to the right of the code selector column.
In the opened window, there are two lists: in the list to the left the fields coming from the lookup are showed, whereas in the list on the right, the list of columns to fill in is showed. You have to combine fields coming from the lookup with the ones coming from the grid. Pay attention to double click a field from lookup with a column: do it one row at a time and do not double click all the fields in the lookup first and then the columns from grid!

 **Set grid cell content** 
If you have already created a grid and need toset thecontent a column according to a specific logic, you have to add one or more column events to specific columns.
Suppose you have a grid where there are three columns linked to the following table fields: QUANTITY, UNIT_PRICE, ROW_TOTAL. That means that each of these columns can be identified by the corresponding attribute names: quantity, unitPrice, rowTotal. If you need to set the totalRow with the result ofquantity x unitPrice, what you need is to add a column event to the quantity column, so that a javascript action can be invoked when losing focus on that column and execute the calculus.
Note that probably additional column events are needed for other columns to cover all the cases involved with the reckoning of the row total.
In order toadd that column event,followthesesteps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the already existing window containing the grid, choose the &#8220; **Panels** &#8221; subfolder and  **double click on the grid** 
* in the folder named &#8220; **Column events** &#8220;, press the &#8220; **New** &#8221; buttonto create a new column event
*  **select the column you want to listen to the change value event**  (related to the quantity)
*  **select the event related to the &#8220;focus lost&#8221; or &#8220;value changed&#8221;** 
* create a new action by  **double clicking on the action cell;**  this will open a window where you can define that action
* select &#8220; **javascript** &#8221; as the language format
* fill in the action content with something like that:

var quantity = gridXXX.getSelectionModel().getSelected(). **get** (&#8220;quantity&#8221;);
var unitPrice= gridXXX.getSelectionModel().getSelected(). **get** (&#8220;unitPrice&#8221;);
gridXXX.getSelectionModel().getSelected(). **set** (&#8220;rowTotal&#8221;,quantity*unitPrice);

* press the &#8220; **Save** &#8221; button to confirm the action and close that window
* press the &#8220; **Save** &#8221; button to confirm thecreation of that event linked to the action just created


 **Set server sidecontent** 
Suppose you have a couple of tables having a relationship 1:N (as for an order header and order rows tables).Moreover,you have a grid showing data from the first tableand a second grid showing data about the second table.
If you need to reload the content of the first grid when saving data on the second grid, what you have to do is to create a SQL action linked to the &#8220;after saving&#8221; event of the second grid, so that this SQL can be used to update the content of the first grid.
Finally, the first grid has to be reloaded, to refresh its content.

You can perform these operations throughthesesteps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the window containing the  **second**  grid, choose the &#8220; **Panels** &#8221; subfolder and  **double click on the grid** 
* in the folder named &#8220; **Events** &#8220;, press the &#8220; **New** &#8221; buttonto create a new event after saving
* choose the event related to &#8220; **after saving data on insert** &#8221; (you should probably also create events for after saving data on update and after deleting data and link the same action)
* create a new action by  **double clicking on the action cell;**  this will open a window where you can define that action
* select &#8220; **SQL** &#8221; as the language format
* fill in the action content with something like that:

UPDATE FIRST_TABLE SET &#8230; WHERE FIELD = :FIELD_FROM_SECOND_TABLE

* press the &#8220; **Save** &#8221; button to confirm the action and close that window
* press the &#8220; **Save** &#8221; button to confirm thecreation of that event linked to the action just created


 **Reload a grid from another window** 
If you have two windows and you need to reload a grid included in the first window, starting from a second window opened from the first one, what you need is to pass a reference to the first window grid to the second window and then use it to force the grid reloading when needed.
These are the steps to follow:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the firstwindow containing the grid, choose the &#8220; **Panels** &#8221; subfolder and  **double click on the grid** 
* in the folder named &#8220; **Events** &#8220;,select the action related to the opening of the second window, probably when double clicking a row or when pressing a toolbar button (see &#8220;Buttons&#8221; subfolder too)
* once identified and opened the right action, having the openWindowXXX(args) instruction, you have to add an additional instruction before it, in order to pass forward the reference to the first grid

args. **parentGridId**  = gridZZZ. **id** ;

* at this point, you can reference it from another action included with the second grid; in that action you can reload the first grid through a line like this one:

var gridPanelId = args. **parentGridId** ;
var parentGrid = Ext.ComponentMgr.get(gridPanelId);
parentGrid.store.reload();

 **Creating a window with a tree + grid** 
A window composed of a tree and a gridcan be created through the following steps:

* select &#8220; **Data Model** &#8221; -&gt;  **Add Objects to Database** &#8220;
*  **select the tables**  related to the content to show on the grid and for each tree level; if multiple tables are needed to show the right content on the grid/tree, select all of them; some of the tables could have been already selected in the past, so here you can only select tables which have not been chosen yet
* press the &#8220; **Generate** &#8221; button on the right bottom area
* once created the objects, two additional business components have also been created for each object; you have to set the right filtering conditions for each tree level and for the grid: select &#8220; **Objects and relations** &#8221; and open everyobject created, for each of it,choose the &#8220; **Business Components** &#8221; tab in the object detail window and select the business component related to a list of data and

* press the &#8220; **Edit** &#8221; button to change settings
* in the main subfolder, set the  **WHERE**  condition as needed, then press &#8220; **Save** &#8220;


* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Add Window** &#8221; to access to the window creation wizard, set the  **window title** , an  **icon**  and press &#8220; **Next** &#8221; button on the right bottom area
* select the &#8220; **Tree** &#8221; widget andpress &#8220; **Next** &#8221; button on the right bottom area
* set the  **business component ** to feed  **the first level**  of thetree; once saved that panel, you can access to the configuration of all the other levels by pressing the &#8220; **Further levels** &#8221; button on the right bottom area
* press &#8220; **New** &#8221; buttonto  **selectthe business component**  to use for each level; you have to repeat this step for each remaining tree level; choose the right component,  **select the field to use as node description**  and select again the row to have access to the fields list in the second grid
* in the second grid,  **choose the field to map**  with the filtering conditions defined for the current business component; press &#8220; **Save** &#8221; button when completing that task


 **Use a grid to upload/download files** 
First you have to create a window containing and editable grid.
Once create that grid, be sure there is a column that can be used to store the file name and then follow these steps:

* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Directories** to define a new path in the server file system where all files will be stored for that grid
* press the &#8220; **New** &#8221; button to create a new path
* set a  **description**  and a feasible  **path** ; be sure that path can be accessed both to read and write files by the o.s. user defined to start 4WS.Platform web application
* press the &#8220; **Save** &#8221; button to confirm the setting
* select &#8220; **Application Management** &#8221; -&gt; &#8220; **Windows** &#8221; and select the window containing the  **second**  grid, choose the &#8220; **Panels** &#8221; subfolder and  **double click on the grid** 
* in the folder named &#8220;Grid columns&#8220;, press the &#8220; **Edit** &#8221; buttonand select the row related to the column which will host the file name
* change its t **ype to &#8220;File Upload&#8221;** 
* select also thepath where saving files:  **choose the directory previously defined**  in the &#8220;Directory&#8221; column
* press the &#8220; **Save** &#8221; button to confirm the setting


At this point, the file name column will show a button used to show a small dialog through which upload/download/preview files.

 **Embedding google calendar, drive or other content in Platform** 
Goole Apps suite includes several content: Google Spreadsheets, Calendar, Hangout, etc.
This content is HTML based, consequently, it can be easily embedded into a 4WS.Platform application, as HTML fragments.
In order to do it, you have first to configure your application with the Google SSO. This operation is described in the Google sections.
Once completed the Google SSO setting, you can start embedding Google panels into Platform.
You can do it in two alternative ways:

*  **as a menu item** : when the user clicks on that menu item, a window is opened; that window only contains the Google feature to show (a Google Calendar page, a Spreadsheet, etc.)
*  **as a panel inside a window** , which can contain more than the Google feature


In the first case, you are defining application menu items, so you have to use the App Designer and go to  **Application Management**  -&gt;  **Menu** 
Here you have to select the folder when you want to add a new menu item,  **right click**  on it and choose **Create link to a web page** .
At this stage, you can also specify whether the web resource must be showed as a window inside Platform application or outside, as an independent web page, through the &#8220;Open on another page&#8221; check-box
In the URL input field, you have to specify the URL to the Google resource you want to refer. Platform will use it to create a window containing an &lt;iframe&gt; tag.
Consequently, you have to include in the URL also the required parameter to make it possible to open a Google web resource withinan &lt;iframe&gt;.
These are a few examples of URLs to specify in order to add Google web resources:

| Calendar | A specific calendar, identified by its src property:  **https://www.google.com/calendar/embed?src=&#8230;**  You can retrieve your own complete URL from the URI in your web browser, when opening directly on your own the Calendar page A specific calendar, identified by the email address:  **http://www.google.com/calendar/embed?src=:USERNAME**  Here the username is specified dynamically using :USERNAME Since you have already logged on using your Google email address, it will be inherited here and passed forward. Note the &#8220;embed&#8221; directive: it is used to inform Google that the web resource will be showed inside an &lt;iframe&gt; |
| :--- | :--- |
| Spreadsheet | A specific spreadsheet, identified by its id property:  **https://drive.google.com/open?id=**  **&lt;idproperty&gt;**   A specific spreadsheet, identified by its id property  **https://docs.google.com/a/sinesy.it/spreadsheets/d/&lt;idproperty&gt;/edit**  |
| Hangout on a Form Panel | You can add a Google Hangout button to the form panel, in order to open an independent web page where hosting the Hangout. An email address can also be added to it, to invite another person to thee Hangout. A prerequisite is to configure the Google Domain and SSO before that. After creating the form panel, you have to add a panel event: &#8220;after rendeer&#8221; and link to it a javascript action: if (formPanelXXX.hangout==null) { formPanelXXX.hangout = true; // this is to avoid that multiple hangout button will be added to the toolbar // important note: the hangout js lib must be loaded when the app is loaded&#8230; // see https://developers.google.com/+/hangouts/button for more details about how to customize an Hangout button&#8230; // initialize google hangout button as an HTML element&#8230; var hangoutButtonId = &#8220;HANGOUT&#8221;+new Date().getTime(); var html = &#8216;&lt;div class=&#8221;g-hangout&#8221; data-render=&#8221;createhangout&#8221; id=&#8221;&#8216;+hangoutButtonId+&#8217; &#8216;+ &#8216;data-initial_apps=&#8221;[{ }]&#8221; &gt;&#8217;+ &#8216;&lt;/div&gt;&#8217;; var settings = { render: &#8216;createhangout&#8217;, widget_size: 30, invites: [{ id : formPanelXXX.getForm().record. **attributeRelatedToTheEmailAddress** , invite_type : &#8216;EMAIL&#8217; }] }; var b = new Ext.Button({ xtype: &#8216;button&#8217;, text: html, id: hangoutButtonId, tooltip: &#8216;Hangout&#8217;, listeners: { afterrender: function(c) { gapi.hangout.render(hangoutButtonId, settings); } } }); formToolbarXXX.addButton(b); formToolbarXXX.doLayout(); }  Note: before using this feature, be sure to load the Google js library for Hangout. You can load it by creating a js action linked to the application event &#8220;After loading application&#8221;, available in the Application Detail. That action should include this instruction: // load google lib x hangout&#8230; reloadScript(&#8220;https://apis.google.com/js/platform.js&#8221;); |






                

---


