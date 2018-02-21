# Code selectors

A code selector is a special input control or column cell editor that can be used to select a value from a list of possible values. A code selector can be defined through the "Code Selector" menu item, which provides a wizard that makes it possible to define a code selector.

![](http://4wsplatform.org/wp-content/uploads/2015/12/Selector-1024x464.jpg)

4WS.Platform provides these types of code selector:

* **static combo box ** – a combobox whose content is fixed and pre-defined by the user through the "Code Selector" wizard; for each item showed in the combo-box, two data must be provided: a code \(not showed in the combobox\) and a description \(which is the one viewed as combo item\); the description is translated according to the current language; this is the typical MVC paradigm where the model \(data\) is decoupled from the view \(what to show on the GUI\); for instance, it can be defined a code selector for the "gender", having two items: "M" with translation "male" and "F" with translation "female", where "male" and "female" are entries in the translations dictionary and will be translated in each of the supported language \(see "Translations" section for more details\)
* **dynamic combo box**  – a combobox whose content is retrieved at runtime; through the "Code Selector" wizard it is possible to define the business component which will provide the data at runtime; again, two data have to be provided for each item: code and description \(to translate\), so the business component must provide at least these two data
* **code + button lookup**  – this control is composed of an input field + a button; the user can validate the input control content when losing focus or can fill out it by selecting a code from the lookup grid opened when pressing the button; in both cases the input control will contain a valid code; the business component used to feed the grid is the same invoked when losing focus on the input control: in the latter case, the SQL query defined in the business component will have an additional filter condition related to the specified code to validate; this component is useful when the code is known to the user and have a real meaning
* **lookup button** – this control is similar to the previous one, with the difference that there is not the input control, so it is feasible when there is not a code to validate, for instance because there is not a real value known to the user \(e.g. an internal counter\).
* **images combo-box** – a combo-box whose entries are images chosen by user during the wizard procedure. For each item showed in the combo-box two data must be provided: a  **code**  \(not showed in the combo-box\) and an  **image**  \(showed in the combo-box\).
* **tree lookup –** this control is similar to the other lookups, with the difference that it is based on a tree panel \(not a business component\). Before using this code selector you need to create a tree panel to associate with it.

When creating a code selector of type lookup, the wizard will automatically create also a grid panel used to show the list of codes, when pressing the lookup button. The user can change the content of this grid, in terms of grid title, visible columns, column lengths and headers, etc, as for any other grid.

---



