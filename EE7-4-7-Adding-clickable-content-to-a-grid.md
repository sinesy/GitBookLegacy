# Adding a clickable content to a grid

A grid panel in a mobile app is never editable: it means that you cannot switch the grid in INSERT or EDIT mode, since there is not content in the grid which can be edited.  
However, it is still possible to add readonly content which can be clickable, like buttons: aspecial column type for a grid is the “ **Detail** ” column type.  
Suppose you want to set the content of a cell in the grid with these controls:

* a button to decrement a numeric value \(with text “-“\)
* a readonly numeric control including the current value for the cell
* a button to increment a numeric value \(with text “+”\)
* a button to save the changes somewhere

First, you have to define a  **form panel,**  having the same data model \(indirectly\) linked to the grid. In this way, the form can be loaded automatically starting from the values contained current row in grid. The form panel should contain the controls described above, for example by defining virtual fields for the buttons.  
Second, you can open the definition for the grid, select the corresponding column and change its type to “ **Detail** “.  
Next, change the property named “ **Form** ” and select the form panel just defined.  
The next time you open that grid in the mobile app, the cell will be rendered with the form panel, loaded automatically and the user will be able to press the buttons in it.  
Finally, you have to add events on the +/- buttons, in order to listen to the click event and execute a javascript action, used to increment/decrement the content of the numeric field AND of the current cell.  
The code in such an action could be something like:

```js
var qty = parseInt(getFormPanelValueXXX('quantity'));
qty = qty + 1;
setFormPanelValueXXX('quantity', qty);
```

where XXX is the panel id for the form panel and “quantity” is the name of an attribute defined in the form panel \(and in the row for the grid\).  
The last control, the Save button, can be used to save the changes somewhere, by retrieving the current value in the numeric field and save it in a table.  
Note that you don’t have necessarely to pass through a Save button: you could use the events for the +/- buttons and save the change directly in that action.

---



