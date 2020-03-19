# Filtering a grid column without a filter panel

The easiest way to filter a grid is through a filter panel. The filter panel must be included in the same window containing the grid and it can have an height set to 0 pixel or more: in case of 0 pixel height, the filter is hidden and cab ne shown by clicking on the Filter symbol on the top-right part of the window. Otherwise the filter is shown in a specific region of the window.  
An alternative approach, not requiring a filter panel, is using a popup window showing a list of values used to filter the grid. This popup window can be shown starting from a javascript action execute on the mobile device.  
The action must be invoked in some way, for example by linking it to a custom button on the topbar or listening to a row event.  
The content of that action could be something like:

```js
var descriptions = [
  { description: "M", code: "Male" },
  { description: "F", code: "Female" }
];

var fun = function(ris) {
  // ris contains the INDEX of the selected item
  var selectedCode = descriptions[ris].code;
  addFilter("gender","=",selectedCode); // add a filter condition
  reloadGridPanelXXX({}); // reload grid
};
var opts = {};
opts.title = "Filter by gender";
opts.list = descriptions;
opts.attrName = "description";
opts.cancelAllowed = "Y";
showListDialog(opts,"fun");
```

where XXX is the panel id for the grid.  
In this example, the grid should contain a column named “gender” and the “addFilter” built-in function would apply a filtering condition for such a column. Finally, the grid is reloaded.

---



