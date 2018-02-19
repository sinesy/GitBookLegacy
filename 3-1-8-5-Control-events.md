# Control events

It is possible to add actions to perform when an event is fired in a control.  
Many events are supported:

* **focus grab and lost** 
* **value changed**  – after losing focus on the control, if the value has changed, this event is fired; the user can link an action to execute when the event happened
* **enable/disable a control** 
* **before validation**  – in case of a code selector column, the user can digit a value within the cell editor and when the focus is lost, the validation would start; through this event it is possible to intercept the validation task and perform an action just before the validation process: in this way it is possible for instance to apply filtering conditions to the validation request
* **value correctly validated**  – in case of a code selector column, the user can digit a value within the cell editor and when the focus is lost, the validation would start; through this event it is possible to intercept the outcome of the validation task, in case of valid value
* **value not correctly validated**  – in case of a code selector column, the user can digit a value within the cell editor and when the focus is lost, the validation would start; through this event it is possible to intercept the outcome of the validation task, in case of invalid value
* **before grid opening**  – in case of a code selector column, the user can select the code from the lookup grid; through this is event it is possible to intercept the grid opening and perform an action just before this event: in this way it is possible for instance to apply filtering conditions to the grid’s data loading request
* **row selected**  – in case of a code selector column, the user can select the code from the lookup grid; through this is event it is possible to intercept the grid selection value.
* **button click**  – in case of a button controls, the user can select the action to execute on click.

---



