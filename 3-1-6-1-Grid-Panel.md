# Grid Panel

**In case of grid or filter+grid or grid+detail form** , the grid definition panel is showed; through it the user has to define settings related to the grid component:

* grid title \(optional, can be hidden\)
* business component \(for list of data\) to link to the grid; the fields specified in the select clause are used to automatically 
* create the grid columns; user can then show/hide each of them, as well as define many other column settings
* grid width and height
* flags to show/hide border and to set panel opacity
* flags to allow the CRUD operations, i.e. insert, update and delete \(only if the data model linked to the selected business component is writable\); in case of insert enabled, it is possible to specify the maximum number of rows to insert before saving them
* data fetching policy: read all or a block of data and its size
* flag to define if data loading is automatically performed when the grid is showed
* initial grid mode, when the grid is showed; grids and forms have 3 alternative modes: readonly, insert, edit; in insert mode a new row is showed; through up/down arrows is possible to add/remove \(empty\) rows; in edit mode, all rows are editable or the one only \(selected row\), according to the flag "multiple changes"
* flag "copy enabled", used to show a "copy" button in the grid toolbar, used to switch to insert mode the grid, add a new row an copy the values from the selected row to the new one
* number of columns anchored to the left of the grid \(0 by default\)
* boolean javascript expression "disable when", to disable everything when the boolean condition is true flags "enable columns permission" and "enable columns profile", used to manage these special features, described in a separate section.

When creating the grid, a grid toolbar is automatically showed on top of it; this toolbar always includes the reload button; the other buttons \(insert, edit, delete and save/cancel\) are showed/hidden according to the flags described above.  
These buttons  change the current grid mode, according to the following policy:

* insert button, from readonly mode -&gt; insert mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* edit button, from readonly mode -&gt; edit mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* delete button, from readonly mode -&gt; after confirming the operation, the selected records are deleted
* cancel button, from insert/edit mode -&gt; after confirming the operation, the grid is switched to readonly mode and the content reloaded
* save button, from insert/edit mode -&gt; the grid is switched to readonly mode if the saving operation has been performed successfully.

---

## Summary row

Optionally, a **summary locked row**  can be showed on the bottom of the grid; this read only row is automatically showed only if there is an "update summary row" event linked to the grid: in that case it will be showed and the javascript action binded to the event is invoked for each column, every time a cell is changed.  
In order to avoid setting a total value for a specific cell, a ‘’ can be returned to that callback in the action. It is possible to set foreground and background colors for a cell through css class names \(see details specified below for the "update summary row" event\).

Example:

```js
if (colAttr!='attributenameofaspecificcolumn') return '';
return formattedValue;
```

or

```js
params.css = 'red';
return total;
```

---

## Grouped columns in multiple groups

Optionally , it is possible to **group columns in multiple groups**, so that there will be a hierarchy of headers, spread in multiple header rows.

In order to do it, add the "Column header" panel event to the grid and define a client-side javascript action containing the headers definition.

An example  of such a definition is the following:

```js
// example for 45  columns, grouped in 5 main headers
// colspan is used to define how many headers to include in each main header
return [[
{ // first main header
    header: ' ',
    colspan: 10
}, { // second main header 
    header: Ext.translate.Cache.getTranslation('SECOND_TITLE'),
    align: 'center',
    colspan: 3
}, {
    header: Ext.translate.Cache.getTranslation('THIRD_TITLE'),
    align: 'center',
    colspan: 3
}, {
    header: Ext.translate.Cache.getTranslation('FORTH_TITLE'),
    align: 'center',
    colspan: 4
}, {
    header: Ext.translate.Cache.getTranslation('FIFTH_TITLE'),
    align: 'center',
    colspan: 25
}
]];
```

---

## Locked columns

Optionally, a group of** locked columns** can be anchored to the left side of the grid. In order to do it, set the "**Locked columns nr**" in the grid definition window.

In case **locked columns are combined with grouping columns, a new grid is rendered, composed of a tree+grid,** where grouping columns become tree nodes, which are anchored on the left side of the grid. That means it is not supported a grid having grouped columns+locked columns.

