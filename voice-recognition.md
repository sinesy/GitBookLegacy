# Voice recognition

This functionality allows to execute some commands within the web application, starting from the voice of the end user.

Supported languages are Italian and English, according to the language linked to the user.

In order to activate this feature, go to the Application Parameters in  the App Designer, expand the VOICE group and enable the property "Enable voice". You have also the define the command to use to start the voice recognition session, through the property "Voice activation command". 

Once done that, you can start executing commands. The voice recognition session will automatically stops after 30 seconds without any sound.

Current supported commands are:

| Command in English | Command in Italian | Meaning |
| :--- | :--- | :--- |
| hello | ciao | Say hi to the web app and listen to the response |
| open window &lt;windowtitle&gt; | apri finestra &lt;titolofinestra&gt; | Open the window from the menu, having the specified title |
| close window | chiudi finestra | Close current window |
| insert | inserisci | Switch the grid/form to insert mode |
| edit | modifica | Switch the grid/form to edit mode |
| cancel | annulla | Undo the current operation and switch the grid/form  to read-only mode |
| save | salva | Save data |
| delete | cancella | Delete current selected row in grid |
| open row &lt;rownumber&gt; | apri riga &lt;numeroriga&gt; | Open the detail window related to the row having the specified row number \(starting from 0\) |
| select row &lt;rownumber&gt; | seleziona riga &lt;numeroriga&gt; | Select the specified row number \(starting from 0\) in the current grid |
| select window &lt;windowtitle&gt; | seleziona finestra &lt;titolofinestra&gt; | Among the already opened windows, select the specified one and make it in front of all the others |
| yes | si | Press the Yes button |
| no | no | Press the No button |
| ok | ok | Press the Ok button |
| clear up | pulisci | clear up the current content |
| button &lt;buttontitle&gt; | bottone &lt;titolobottone&gt; | Click the specified button |
| close all | chiudi tutto | Close all opened windows |
| quit | esci | Quit the web application |







