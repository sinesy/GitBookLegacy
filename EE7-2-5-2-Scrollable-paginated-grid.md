# Scrollable paginated grid

The main features of a grid are:

* read only grid
* full read content or paginated reading
* vertical and horizontal scrolling \(useful in case of a large amount of columns exceeding the display width\)
* sortable columns, by tapping on the column headers
* supported columns:
  * text field
  * check box
  * date, date+time, time
  * numeric field; decimal numbers are supported too and they are configurable in the Web Designer form panel image preview, with buttons to select an image \(from the camera/image gallery\) and remove it
  * file selector – e.g. a PDF file, with buttons to show the file preview and delete it.testo \(per testo e numeri\) decoded value, starting from an enumeration of couples &lt;code, description to show&gt;
  * **form panel **
* support render for standard columns
* support render for field on form columns



## Render fields

With render you can change the field style or properties. Available properties are:

```js
var obj = {};
obj.value = vo["progId"];
obj.backgroundColor="#FFFF0000";
obj.foregroundColor="#FF000000";
obj.fontName="Arial"; //the font must be present in the application
obj.fontStyle="Bold";
obj.fontSize="15";
obj.label="My Label;
obj.textAlignment="right"; //right, center, left
obj.visible="Y"; // Y or N
obj.enabled="Y"; // Y or N
return convertToObjectJson(obj);
//NOTE fontName, fontStyle and fontSize must be filled in together
```



---



