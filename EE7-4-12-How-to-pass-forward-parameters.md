# How to pass forward parameters

Suppose you have a window, containing one or more panels and you need to open a second window, whose content depends on some selection of the first one.  
A common example is: the first window contains grid, the selection of a row should open a second window containing a detail form, used to show the record related to the selected row in grid.  
This very simple scenario is automatically managed by platform, when creating the second window from the App Designer’s windows Wizard.  
More in general, the need for passing forward parameters can be managed through a javascript action linked to some event on the first panel and write something like:

```js
setUserSessionVariable(varName,varValue);
```

Basically, the solution is storing temporary data at app level and refer it everywhere.  
In this way, any panel in any window can access to it, including panels added to other windows.  
This is the easiest way to pass forward parameters.

**Important note: ** pay attention to the the name assigned to the session variable! Bear in mind that this variable is defined at app level, so you must be sure to assign distinct names. A good practise is to define variable names like “PANELXXX\_VARNAME”, in this way you’ll never take the risk to erroneously reuse the same variable name in different panels.

---



