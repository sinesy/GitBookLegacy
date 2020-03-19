# How to pass back parameters

Suppose you have a window W2, previously opened starting from another window W1 and you need to pass back to W1 values set in W2.  
An example is a first window containing a form panel in EDIT mode and the pressing of a custom button would show a second window used to fill a few input controls. When pressing a button on the second window, the values set on these input controls should be passed back to controls on the first form control.

There are two alternative approaches for that:

* using session variables, as for “Passing forward parameters”
* directly set the content of a detail form

**1. Passing back parameters**  can be managed through a javascript action linked to some event on the second window \(e.g. the button click\) and write something like:

```js
setUserSessionVariable(varName,varValue);
```

Basically, the solution is storing temporary data at app level and refer it everywhere.  
In this way, any panel in any window can access to it, including panels added to other windows.  
This is the easiest way to pass back parameters.

**Important note: ** pay attention to the the name assigned to the session variable! Bear in mind that this variable is defined at app level, so you must be sure to assign distinct names. A good practise is to define variable names like “PANELXXX\_VARNAME”, in this way you’ll never take the risk to erroneously reuse the same variable name in different panels.

**2. Directly set the content of a detail form**   
In this scenario, you can use the build-in javascript method:

```js
setFormPanelValueXXX(attr,value);
```

within a javascript action invoked for example when closing the second window.  
XXX represents the panel id form the detail form.  
In this way, you can set the value for each graphics control defined in the detail form.

---



