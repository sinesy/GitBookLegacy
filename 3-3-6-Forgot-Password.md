# Forgot Password

Within the login form there exists a "forgot password" link. After clicking on this link, the user has to insert the email address.  
After that, 4WS.Platform will send to that email address a link for changing the password.  
The “forgot password” link is visible only if the following parameters have been defined in the App Designer, through the Application Parameters or Global Parameters feature:

* SMTP host to use for sending emails
* Administrator e-mail, i.e. the email address used for the sender
* 4WS.Platform base URL – needed to create a dynamic link to include in the email message, used to point to the right Platform server.

---



