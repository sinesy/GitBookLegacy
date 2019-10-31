# Mail task

This task allows to send an email message during the execution of a process.  
Before sending email, the mail subsystem must be configured correctly: the activty-context.xml file must contain the settings related the SMTP server to communicate with.  
Once completed the initial configuration of the SMTP server, a mail task can be included in a process and the following task properties must be defined:

* Id and Name: they identity the task and they are mandatory; be sure NOT to include accents in these fields \(only alphanumeric characters are allowed\).
* Documentation: an optional description of this task
* To/From/Subject/Cc/Bcc: to and from address and subject are required; the other properties are optional
* Text/HTML: either the text or the HTML body must be provided.

---



