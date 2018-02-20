# How to format data in grid

You can change the default way data is shown in a grid, in terms of data format \(e.g. for numbers or date\) and colors.  
How to set colors for a cell is described in “4.22 How to change colors in a grid”.  
In order to customize the dataformat, you have to open the definition window for a grid, move to the “Column” sub-folder andswitch to “Advanced” mode.  
At this point, for each column you can see the “Renderer” property, where you can type javascript instructions to set both the background and/or foreground color for that column.

### Example

```js
var myDate = vo['TABLE.COLUNMNAME'];

var format = "yyyy-MM-dd HH:mm:ss";

var textToShow = addDate(myDate.getTime(),format,0);
var obj = { value: textToShow };

var val = convertToObjectJson(obj);

return val;
```

In this example you can see how it works:

* you have always to return a JSON string, representing a js object having the attribute value
* you can include js instructions to set the right format \(e.g. addDate, which converts milliseconds in a String type date\)
* you can access to the content of the current row, through the build-in “vo” js object, containing all the values for the row, each expressed as TABLENAME.COLUMNAME

---



