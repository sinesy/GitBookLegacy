# How to load a grid when clicking on a tree node

Suppose you have a window containing a tree and a grid depending on the node currently selected on the tree. What you want is to reload the grid when selecting a node in the tree.  
You can do that manually, by binding to the "node clicked" event of the tree a javascript action containing js code to reload the grid. You can use a wizard available in the tree panel definition to generate the same settings automatically.  
A few wizards are available in the settings panel for a tree in the Web Designer. One of these wizards is about "Grid loading when clicking a node". When selecting this item, a settings dialog is showed: once the user has selected the grid, a list of required parameters is proposed on the right: these are parameters required by the grid in order to read data correctly.  
For each of them, the user has to bind a value to that parameter, which can be a constant value, a variable \(such as username, current date, etc.\) or a value coming from the current selected node.  
In this way, the wizard has all information needed to create a javascript action and bind it to the "node clicked" event.

---



