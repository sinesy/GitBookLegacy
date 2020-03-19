# How to share a document text on social media

Social media like Facebook or Google+ or other sharing services like Whatsapp or Messanger allow to share content, which can be expressed as links, images, text.  
Platform Mobile supports two ways to share content:

* share a document, like an image
* share a text

In both cases, a popup window is prompted to the user, showing the available social media supported by the user mobile device.  
The user can then select on which media to share the content and the destination, if available \(e.g. phone number for Whatsapp\) and send it.  
The two alternatives can be managed through the following javascript methods, that you can include in a javascript action to link to some mobile event, like a button click:

**Sharing a document, like an image**

```js
shareDocument(path, filename);
```

Here you have first to save an image locally and you have to know where it is located \(absolute path + file name\).

**Sharing a text + an image**

```js
shareText(Text, imageUrl, appType);
```

Here you have to provide the text.  
ONLY FOR email messages to send through the mobile app, you can specify as well an image, expressed as a remote URL.  
That means that the image must be a public URL.  
appType can be one of the following:

* EMAIL
* FACEBOOK,
* WHATSAPP
* SMS
* ALL

That parameter is used to filter the list of media to prompt to the user.

---



