# How to change color for input controls

It is possible to dynamically set the background color for an input control in a form panel or in a filter panel.  
You have to create a javascript action, link it to some event and use the following method:

```js
setBackgroundColorComponent(attributeName, hexBackgroundColor);
```

This method works on the current opened form. The input control is identified by its attribute name and the second argument represents the background color to set, expressed as an hexadecimal string \(e.g. FFFFFF\).

---



