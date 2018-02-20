# How to add a checkbox grid to select one or more rows

When opening the detail window, it is possible to manage the window content in the "Panels" subfolder. One of the panes that can be added to a previously created window is a "checkbox grid". In order to add it to the window, you have to switch to edit mode the panels hierarchical representation and richg click on the root: in the popup menu that will be showed, you can chhose "Add checkbox grid". When selecting that item, a new window will be viewed: through it you have the chance to set all information required to create on the fly a checkbox grid.  
Such a grid will show two only columns: a checkbox editable column used to select rows and a description readonly column.  
Moreover, a toolbar with REFRESH/EDIT/SAVE/CANCEL buttons is set on top of that grid. No insert or delete are allowed. No permissions settings are allowed if the function is visible.

These are the settings to provide in that window:

* a business component to use to retrieve all rows \(e.g. roles\)
* a business component to use to retrieve only the selected rows \(e.g.selected roles
* a grid title
* a flag to define whether the title is visible or not
* the attribute name binded to the description column to show
* the corresponding column header
* a server-side JS action to invoke when saving data
* an optional filterBy parameter which could include an additional SQL like filter to add to the lists

**Note** : both business component must share the same fields structure.  
When saving data, two parameters are provided to the server side js action:

* list of rows just selected
* list of rows just deselected

The input provided to such an action class is a JSON object having this format:

```js
{
"selRows": [{ attr1:... attrN:... },{...},...],
"noSelRows": : [{ attr1:... attrN:... },{...},...]
}
```

The same action class must return a success flag to the client side:

```js
{ "success": true }
```

---



