# GMail

The GMail integration in 4WS.Platform EE lets the application developer implement Javascript actions that send email with GMail APIs. The main difference between this approach and the usage of GMail as authenticated SMTP server is that the sent mail is stored in the sender’s mailbox, in the outgoing messages folder.  
 **NOTE** : to make this function work properly the e-mail field of the user \(see the 4ws.Platform user management UI\) MUST be filled with the correct address that corresponds to the Google Apps for Work account.  
In order to use this feature, you have also to define a few parameters in 4WS.Platform:

* GOOGLE\_SERVACC\_EMAIL
* GOOGLE\_SERVACC\_KEY

to enable the Google Apps integration and the sending address must correspond to a Google Apps user.

### Syntax

```js
utils.sendGmail(from, to, subject, body, isHtmlContent, zipFiles, deleteFilesAfterSending, filesToAttach)
```

### Details

**from**  – \(optional, can be null\) a string representing the email address to use as the “from address” to send the email. Can be one of the address from which te Google usare can send emails.  
 **to**  – a string composed of one or more email addresses, separated by a comma \(,\)  
 **cc**  – carbon copy addresses – a string composed of one or more email addresses, separated by a comma \(,\)  
 **bcc**  – hidden addresses – a string composed of one or more email addresses, separated by a comma \(,\)  
 **subject**  – a string representing the email title  
 **body**  – the email body content  
 **isHtmlContent**  – a boolean flag used to define if the body content is in HTML format or not  
 **returnReceipt**  – a boolean flag used to request a return receipt to the destinators  
 **zipFiles**  – a boolean flag used to compress all files to attach in a unique zip file and send it, in order to reduce the email size  
 **deleteFilesAfterSending**  – a boolean flag used to optionally delete files to attach, after sending the email  
 **filesToAttach**  – a list of files to attach, separated by a comma; use \[\] to notinclude files; each file must include the absolute path  
This method will fire an exception if the email has NOT been sent correctly \(e.g. attachment file not found\).

---



