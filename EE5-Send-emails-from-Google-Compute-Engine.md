# Send emails from Google Compute Engine

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



