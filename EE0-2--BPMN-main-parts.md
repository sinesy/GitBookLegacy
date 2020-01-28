# BPMN main parts

A BPMN process is composed of a set of **activities** and **properties**.

![](/assets/Schermata 2020-01-28 alle 08.39.36.png)

**Properties** represent data that the process has to manage, composed of data passed to the process when starting it and data created or updated when moving from an activity to the other. Properties can be read only or updatable and can be linked to specific activities, in order to show or edit them.

An **activity** can be **manual** \(a user task\) or **automatic** \(a service\).  
In the first case, it must be started manually by a user, carried out and completed by the same user. A manual activity can be started by a group of people \(candidates\); any of them can start it but once started it, it can be completed only by that person. Optionally, a manual activity can be automatically assigned to a specific person.

An automatic activity can be of several types: **an email**, a **command to execute from the shell, a program, a web service to invoke, a SQL query** to fetch data to work with or a **SQL statement to write data** on a database.  
According to the activity type, different settings are required; for instance, in case of an email to send, the "from address", "destination addresses", "object" and "body" are required. A SQL task is totally different and requires different settings.

---



