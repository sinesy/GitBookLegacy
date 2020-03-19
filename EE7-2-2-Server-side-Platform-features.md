# Server-side Platform features

The App Designer is used to define those apps in a similar way to the interpreted web applications. The main features enabled in the App Designer when creating mobile apps are:

* creation of any number of mobile apps per single installation of the server-side version of Platform
* definition of any number of objects and relationships
* definition of any number of business components; this component can work online \(as web services available on the server-side and invoked remotelly by the the mobile app\) or can work offline, by accessing the local database \(SqlLite\)
* definition of windows containing:

  * a filter
  * a read only grid, with scrolling support of both sides, pagination, multiple sorting of columns
  * a filter + read only grid
  * a detail form
  * a combination of these panes

  A window can then be linked to a specific device: a smartphone or a tablet or used by both of them

* support for a toolbar in grids and forms to execute CRUD operations \(insert, update, delete\)
* support for custom buttons to add to toolbars
* support for UI events: before/after insert/update/delete, row click, button touch, before/after loading data



