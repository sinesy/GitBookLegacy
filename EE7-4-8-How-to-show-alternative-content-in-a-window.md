# How to show alternative content in a window

Suppose you have a window containing a large amount of data and you don’t have enough space to show all of it at the same time.  
In a larger display, a possible solution could be to group the content in a set of folders, where one folder at a time is shown and the user can click on the folder title to pass from one sub-content to the other.  
Folders are not directly supported in Platform Mobile, but you can create something very similar, using an Alternative Panel, whose content can be shown alternatively and you can drive which content to show at a time programmatically.  
This solution requires to:

* define in the window a panel to manage the switching among the alternative content. This panel could contain a set of buttons, one for each alternative content: when pressing a button, the corresponding alternative content would be shown. This buttons panels could be arranged on the top of the window or for instance at its left margin \(West region\)
* define in the window an Alternative panel
* create a series of panels to add as children to the Alternative panel, such as grids, detail form or other panels
* attach to each button an javascript action used to programmatically switch from an alternative content to the other.

For example, if your Alternative panel has id XXX and contains alternative contents such as panels identified by X1, …  
An example of such an action is:

```js
showCardPanel(XXX, X1);
```

In this way, you can decide which content to show.

---



