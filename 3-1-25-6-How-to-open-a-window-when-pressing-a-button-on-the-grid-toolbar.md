# How to open a window when pressing a button on the grid toolbar

Suppose you have a window containing a grid and you want to open another window when clicking on a button available in the toolbar on the top of the grid. You can do that manually, by adding a javascript action to a popup menu item and create that javascript action containing js code to open the second window. You can use a wizard available in the grid panel definition to generate the same settings automatically.  
A few wizards are available in the settings panel for a grid in the App Designer. One of these wizards is about "Window opening from a button". When selecting this item, a settings dialog is showed: once the user has selected a window, a list of required parameters is proposed on the right: these are parameters required by the selected window in order to read data correctly.  
For each of them, the user has to bind a value to that parameter, which can be a constant value, a variable \(such as username, current date, etc.\) or a value coming from the selected row in the current grid.  
In this way, the wizard has all information needed to create a javascript action and bind it to the button.

---



