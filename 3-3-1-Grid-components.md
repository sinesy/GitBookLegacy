# Grid components

Grid components are based on Sencha ExtJS and provides advanced features like multiple sorting, filters, data export in Excel or CSV formats, data import, editable cells with ad hoc editors according to data type, toolbar linked to grid to manage CRUD operations \(create, retrieve, update,delete\), user profiles related to these settings stored permanently per user. A grid can have a filter panel binded to it.  
There is also a quick filter that can be showed by simply right clicking on a cell of a filterable column.Through this popup filter it is possible to apply multiple filters on different columns even without a filter panel binded with the grid.

![](http://4wsplatform.org/wp-content/uploads/2015/12/filter.jpg)

Data can be loaded with two different policies:

* all data
* a block of data, whose size can be defined using the App Designer

Data content can be read or changed. Additonal rows can be created from scratch as well, optionally having default values for specific cells. Default values can be defined also when editing already existing rows.  
More in general, a grid has a mode, a sort of state that determines the supported operations. Grid mode can be changed using the toolbar on the top of the grid:

* when pressing the insert button \(if enabled\), the grid mode changes from read only to insert mode: a new empty row is added to the grid; if the maximum number of rows set through the Designer is more than one, additional rows can be added, simply by pressing the down key
* when pressing the edit button \(if enabled\), the grid mode switches from read only to edit mode: all rows in the grid can be changed by the user
* when pressing the save button the grid mode changes to readonly again, if the saving operation succedes
* when pressing the cancel button the grid mode changes to readonly and all the changes applied to the grid in insert/edit mode are lost

---



