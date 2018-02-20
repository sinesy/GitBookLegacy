# How to create a wizard to navigate through a series of panels with Previous-Next buttons

Suppose you need to create a window containing a large amount of controls and you need to force the user to fill the content gradually, from a set of data to another.  
A common solution for this scenario is using an Alternative panel, containing panels to show alternatively and driving from a panel to the other through Previous/Next buttons.  
The steps to follow are:

* add a panel in the window, containing two buttons: Previous and Next, used to decide which panel to show at a time. This panel could be arranged on the bottom of the window \(South region\).
* add an Alternative panel in the window, occupying the rest of the available space
* add a set of panels as children of the Alternative panel

The Previous button should be configured as disabled at the beginning and it should have a javascript action linked to it, in order to switch which panel to show, through an instruction like:

```js
var currentPanel = getPanelParameter("CURRENT_PANEL");
if (currentPanel=="1") {
  setPanelParameter("CURRENT_PANEL","0")
  setEnabledPanelButton("prevButton", false);
  showCardPanel(cardPanelID, panel0);
}
else if (currentPanel=="2") {
  setPanelParameter("CURRENT_PANEL","1")
  showCardPanel(cardPanelID, panel1);
}
else
...
```

A panel parameter named CURRENT\_PANEL is used to store the current panel to show.  
cardPanelID represents the id for the Alternative panel.  
prevButton represents the attribute name for the Previous button.  
Similarly, the Next button needs to manage the switching of panels from left to right, which a scriptlet like the following:

```js
var currentPanel = getPanelParameter("CURRENT_PANEL");
if (currentPanel=="0" ||currentPanel==null) {
  setPanelParameter("CURRENT_PANEL","1")
  setEnabledPanelButton("prevButton", true);
  showCardPanel(cardPanelID, panel1);
}
else if (currentPanel=="1") {
  setPanelParameter("CURRENT_PANEL","2")
  showCardPanel(cardPanelID, panel2);
}
else
...
```

---



