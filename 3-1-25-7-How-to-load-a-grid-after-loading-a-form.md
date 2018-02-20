# How to load a grid after loading a form

Suppose you have a window containing a form and a grid depending on the form content and that the grid content can be loaded starting from some data available in the form. That means that the grid will be loaded after the form loading has been completed and data available.  
You can do that manually, by binding to the "form loaded" event of the form a javascript action containing js code to reload the grid. You can use a wizard available in the form panel definition to generate the same settings automatically.  
A few wizards are available in the settings panel for a form in the App Designer. One of these wizards is about "Grid loading after form loading". When selecting this item, a settings dialog is showed: once the user has selected the grid, a list of required parameters is proposed on the right: these are parameters required by the grid in order to read data correctly.  
For each of them, the user has to bind a value to that parameter, which can be a constant value, a variable \(such as username, current date, etc.\) or a value coming from the form content.  
In this way, the wizard has all information needed to create a javascript action and bind it to the "form loaded" event.

---



