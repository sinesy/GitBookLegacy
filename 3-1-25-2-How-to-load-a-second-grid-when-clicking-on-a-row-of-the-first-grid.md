# How to load a second grid when clicking on a row from the first grid

Suppose you have a window containing two grids and you want to reload the content of the second grid when clicking on a row of the first grid.  
You can do that manually, by binding to the "row click" event of the grid a javascript action containing js code to reload the second grid. You can use a wizard available in the first grid panel definition to generate the same settings automatically.  
A few wizards are available in the settings panel for a grid in the App Designer. One of these wizards is about "Grid loading from a row click". When selecting this item, a settings dialog is showed: once the user has selected a second grid, a list of required parameters is proposed on the right: these are parameters required by the second grid in order to read data correctly.  
For each of them, the user has to bind a value to that parameter, which can be a constant value, a variable \(such as username, current date, etc.\) or a value coming from the selected row in the current grid \(first grid\).  
In this way, the wizard has all information needed to create a javascript action and bind it to the "row click" event.

---



