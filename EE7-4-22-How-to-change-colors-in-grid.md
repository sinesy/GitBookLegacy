You can change foreground and background colors for a specific cell of a grid.
You have to open the definition window for a grid, move to the &#8220;Column&#8221; sub-folder andswitch to &#8220;Advanced&#8221; mode.
At this point, for each column you can see the &#8220;Renderer&#8221; property, where you can type javascript instructions to set both the background and/or foreground color for that column.
## Example

```js
var textToShow = vo['TABLE.COLUNMNAME'];
var obj = {
  value: textToShow
};

var someCondition = ... // boolean value

if (someCondition) {
  obj.foregroundColor = '000000';
  obj.backgroundColor = 'FFAA00';
};
else {
  obj.foregroundColor = '000000';
  obj.backgroundColor = 'AAFF00';
};

var val = convertToObjectJson(obj);
return val;
```

In this example you can see how it works:

* you have always to return a JSON string, representing a js object having attributes: value, backgroundColor, foregroundColor
* you can include js instructions to figure out what color to set (e.g. if/else)
* you can access to the content of the current row, through the build-in &#8220;vo&#8221; js object, containing all the values for the row, each expressed as TABLENAME.COLUMNAME





                

---


