# **Searching for logged data**

Through the menu-bar **Monitoring -&gt; Logs elaborations** it is possible to search for logged data, gathered from the services under control, both on the local installation and on remote installations.

This feature provides a filter panel on the UI through which searching for a variety of different data, coming from elaborations or specific messages.

Available filters include:

* **application** - if not specified, elaborations are not only the ones gathered locally, but also the ones coming from remote Platform installations, where there can be other applications defined and running; in any case, elaborations are filtered by the company id of the logged user \(site id is also filtered according to the site ids bounded to the current logged user\)

* **start date / end date **- elaborations can be filtered by interval or starting from the start datetime or until the specified end datetime

* **service** - the combo-box includes all services defined locally and remote services \(fetched through the “Synchronize and search” button\)

* **code** - this is the service code, which can be specified instead of the service \(description\)

* **elaboration state** - elaborations are filtered according to the state specified here; i this way it is possible to search for errors only or elaborations not finished yet

* **transaction id **- a value representing a cross-server transaction; another way to look for all elaborations having the same transaction is simply filtering the transaction directly in the corresponding column \(right click with the mouse, to activate the quick filter\)

* **message code** - this is related to errors; Platform supports a set of pre-defined message codes \(e.g. out of memory, database lock, etc.\); moreover, a Platform developer can define additional errors \(message codes\), which can be filtered here; if specified, only elaborations having logged messages with this code will be shown

* **file name** - in case of elaborations involving files to read/write and logged as messages, it is possible to filter elaborations referring such a files as logged messages

In case the “service” combo-box has been specified, additional input fields are prompted: for each tag defined for the selected service, a filter control is shown here.

For example, if a “selling” service has been defined with a “barcode” tag, when selecting this service in the filter panel, a “barcode” filter control will be added as well.

![](/assets/Schermata 2020-02-24 alle 11.56.13.png)

The result list reports the following columns:

* **application** - the application id, needed in case of elaborations coming not only from the local server but also from remote servers

* **code** - service code, related to the elaboration

* **start/end date** - datetime when the elaboration started and finished; end date is filled only for elaborations terminated without or with errors

* **duration** - the elaboration duration, expressed in seconds

* **transaction id **- helpful to aggregate elaborations which share the same transaction

* **elaboration state** - an elaboration can be started, ended correctly, ended/interrupted with errors

When double clicking on a row in the result list, the corresponding detail window is prompted.

![](https://lh3.googleusercontent.com/0t4gQ2oIyu5RiPtqa-rpy7r0K56kQkLiIAr_3dLKc26pHuP563QM5CetxX_6mQtOp3T0Qy0qPL-g7MoxfF-6qebIfB0cw7ZrLdK-qFIxOJpabzFts878GIbrWJ2mJE4_lk2S9l4T)

The elaboration detail window contains 3 subfolders:

* **Elaboration** - it reports the elaboration details, such as the application, service code, elaboration state and its transaction id; apart from that, there is also a sub panel containing the input and output for the elaboration, better described below

* **logged messages** - every message can be related to errors or other informative messages; each message include: message type \(fatal error, error, informative message, detailed message, finest message\), message date code, message text, optional file name

* **files** - list of files managed by this elaboration; for each file it is reported the elaboration outcome: still in progress or completed

Note: in the Log sub-folder, when moving the mouse cursor over the “message code”, a tooltip is shown to show:

* the **problem** description for that message code

* the **solution** suggested by Platform to solve the problem

![](https://lh3.googleusercontent.com/92GrmgR1XZTU8mVEHMoruzPSpcTmPp5Hz9eMeLesifFvc_Vw-D3H57dVOfbKblnKeHHUVuotf1eedG678wjVURbmPbKVJI7pX_kaT-Fs3ln5cGp_8dTmg8cpRrnGHK1N73BsXamE)

Note: the **input and output** for the elaboration sub panel contains different content, spread along 4 sub-folders and expressed using JSON format.

The content changes according to the service under monitoring:

* in case of a web service: request headers, request parameters, body request, response

* in case of a data export from table, the result sub-folder contains the number of extracted rows



