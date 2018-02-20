# GMail

The GMail integration in 4WS.Platform EE lets the application developer implement Javascript actions that send email with GMail APIs. The main difference between this approach and the usage of GMail as authenticated SMTP server is that the sent mail is stored in the sender’s mailbox, in the outgoing messages folder.  
 **NOTE** : to make this function work properly the e-mail field of the user \(see the 4ws.Platform user management UI\) MUST be filled with the correct address that corresponds to the Google Apps for Work account.  
In order to use this feature, you have also to define a few parameters in 4WS.Platform:

* GOOGLE\_SERVACC\_EMAIL
* GOOGLE\_SERVACC\_KEY

to enable the Google Apps integration and the sending address must correspond to a Google Apps user.

#### Syntax

```js
utils.sendGmail(from, to, subject, body, isHtmlContent, zipFiles, deleteFilesAfterSending, filesToAttach)
```

#### Details

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



## Send emails from Google Compute Engine

When 4ws.Platform is installed on Google Cloud Platform, the Compute Engine component is used. From the official documentation you can read how to send emails from virtual machines. In particular outbound traffic towards standard SMTP ports \(25, 465, 587\) is blocked.  
Three options are available:

* use a third party SMTP delivery service, like Sendgrid, Mandrill/Mailchimp, Mailgun, Sparkpost, Mailjet. These services allow to use non standard ports \(in general 2525\) and put in place domain whitelisting to guarantee the reputation of the domain and the sending IPs.
* Google Apps for Work. If your company has a Google Apps domain, you can send email through the SMTP relay service. In this case beware the sending limits: the service is not meant to be a replacement for an high traffic transactional/marketing email system.
* Use a corporate email server, configuring non standard ports for the SMTP listener, or bypassing the block connecting Google Cloud and the corporate network with a VPN. This requires to set up the P2P IPSec VPN on both sides, Google Cloud Platform project and corporate firewall.

Our advice is to use the first option: free plans are available in almost every listed provider pricing plans.  
Set up 4WS.Platform  
Once the SMTP service is configured, the following parameters can be specified in 4ws.Platform, under the application parameters section:

* SMTP service IP or address
* SMTP port, different from standard ports
* SMTP protocol
* SMTP username
* SMTP password
* SMTP TLS \(E/F: enabled/forced\)

![](http://4wsplatform.org/wp-content/uploads/2016/05/param_mail_platform-300x165.png)

\(click on the image to enlarge\)

---



