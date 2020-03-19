# Detail scrollable form

The main features of a detail form are:

* input fields are always layout vertically from top to bottom, from left to right; the number of columns to use in the layout is configurable, but should be 1 for smartphone devices, in order to make it easy to read the form content
* **scrollable** 
* controls within the form are stretched automatically horizontally, starting from a standard with of 320 pixels, so that if a specific device has a different width, controls are relocated and strecthed according to the original with of 320. Consequently, you should define a layout based on a theoretic width of 320 pixels.
* supported input fields are:

* text field

* text area

* check box

* calendar, including a button to open a calendar
* numeric field, including an ad hoc numeric keypad; decimal numbers are supported too and they are configurable in the App Designer form panel
* code selector, composed of an input field and a selector button:

* when clicking on the selector button a popup window is showed, in order to choose a code from the list of proposed codes

* when typing a code directly on the input field, this code will be validated when loosing focus and will be emptied if the code validation fails

* image preview, with buttons to select an image \(from the camera/image gallery\) and remove it

* file selector – e.g. a PDF file, with buttons to show the file preview and delete it.



A for can be fill with a business component \(Form Panel\) or can exists without a business component \(Editable panel\).

Form Panel, Editable panel and Filter Panel support the [constraints layout](/constraint-layout.md).

---



