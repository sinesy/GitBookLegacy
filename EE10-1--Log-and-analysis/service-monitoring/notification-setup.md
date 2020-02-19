# **Notifications setup**

In order to automate email notifications, a few global parameters must be set:

**MAIL group**

* * SMTP host

  * SMTP port

  * SMTP username

  * SMTP password

  * Administrator email - used to send email messages: this represents the sender address

**MONITOR group**

* * Email used to send a message - one or more email addresses \(separated by comma\) used to send notification emails

  * Email subject to notify - this is helpful to distinguish among different server installations \(e.g. development, test, production\)

  


In order to avoid multiple email notifications in a limited amount of time, which could be interpreted as spam, there is a smart mechanism that reduces the amount of messages to send: messages are grouped and sent together; no more than one message per minute can be sent; in case of messages after a minute from the last sending, the wait time is doubled: 2 minutes, 4 minutes, … up to 64 minutes; only in case there are fewer messages to send, wait time is automatically reduced up to 1 minute again.

  


An example of email message sent caused by a SQL error is

```
Application: ABC
Service code: CLIENTE
Service elaboration id: 1296aca6-212c-4402-b0d6-b3c027b705ff
Transaction id: 737fd14d-f2d1-4f3c-bd7b-5d016b2fa424
Service elaboration state: S
Date: 2020-02-18 10:07:02.071
Message Type: ERROR
Tags:cab: I000form: CLI10

Message:
Wrapped javax.script.ScriptException: Data truncation: Data too long for column 'CAB' at row 1 Failed instruction: INSERT INTO CLIENTE(LOCALITA….) VALUES(....?)(ActionID_179#155)
```



Thanks to that content, it is possible to search for this error by:

* application - the application which fired the error

* date interval - it allows to filter elaborations

* service code - it identifies the data flow \(e.g. customers, sellings, stock, etc.\)

* transaction id - it identifies a specific execution flow

* tags - they allow to filter elaborations which specific data



