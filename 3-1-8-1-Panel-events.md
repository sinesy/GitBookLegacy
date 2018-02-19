# Panel events

A panel can fire several events, according to the panel type.

![](http://4wsplatform.org/wp-content/uploads/2015/12/panelEvents-1024x519.jpg)

In case of a  **grid ** \(or ** pivot grid** \), these are the allowed events:

* row click
* row double click
* before the rendering of the grid
* before a cell editing
* before the deleting of a row
* before inserting data in grid/form
* before editing data in grid/form
* before data loading
* before data saving on copy mode
* before data saving on insert mode
* before data saving on edit mode
* after a cell editing
* after the deleting of a row
* after data loading
* after data saving in insert mode
* after data saving in edit mode
* click on Enter button
* column model creation
* multiselection in grid
* column headers
* before import row \(Javascript Server only\)
* after import row \(Javascript Server only\)

In case of a  **detail form** , these are the allowed events:

* before the rendering of the detail form
* before data loading
* before data saving in insert mode
* before data saving in edit mode
* before the deleting of the content
* after data loading
* after data saving in insert mode
* after data saving in edit mode
* after the deleting of the content
* on button click \(listen to any additional button added to the top toolbar\)

In case of a  **tree** , these are the allowed events:

* node click
* tree check selected
* tree expand node

In case of a  **filter** , these are the allowed events:

* after loading data
* before render
* when pressing search button
* when pressing undo button

In case of a  **detail form** , these are the allowed events:

* Before data load

For each event it is possible to link an action defined through the "Actions" menu item.

---



