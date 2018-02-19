# Column events

It is possible to add actions to perform when an event is fired in a cell editor. Three events are supported:

* **cell value changed**  – after losing focus on the cell, if the value has changed, this event is fired; the user can link an action to execute when the event happened
* **before validation**  – in case of a code selector column, the user can digit a value within the cell editor and when the focus is lost, the validation would start; through this event it is possible to intercept the validation task and perform an action just before the validation process: in this way it is possible for instance to apply filtering conditions to the validation request
* **before grid opening**  – in case of a code selector column, the user can select the code from the lookup grid; through this is event it is possible to intercept the grid opening and perform an action just before this event: in this way it is possible for instance to apply filtering conditions to the grid’s data loading request.

---



