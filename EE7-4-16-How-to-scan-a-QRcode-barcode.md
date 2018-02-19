Platform Mobile allows to use the camera embedded in the mobile device to scan:

* a  **QRcode** 
* a barcode having one of the following formats: **EAN-13, EAN-8, UPC-A, UPC-E, Code-39, Code-93, Code-128, ITF, Codabar, QR Code, Data Matrix, PDF-417, AZTEC** 

This process starts with the execution of a javascript action, containing a js built-in method you can use to scan either a QRcode or a barcode.
Once done that, a callback js function will be invoked, having as argument the text just scanned.
Two javascript methods are available and described below:

 **1. QRcode** 

```js
scanQRCode(callbackSuccess, callbackCancel, callbackError);

```


Open a QR code reader and execute the scan.
Required arguments:

* callbackSuccess – function name which will be invoked in case of successful scan; an argument is passed to the function: a json with data just read, expressed as a string

* QRCode with a VCARD:


{
&#8220;displayValue&#8221;: &#8220;Name Surname&#8221;,
&#8220;format&#8221;: &#8220;QR_CODE&#8221;,
&#8220;rawValue&#8221;: &#8220;BEGIN:VCARD\nVERSION:2.1\nFN:Name Surname\nN:Surname;Name\nTITLE:Mr\nTEL;CELL:+3912345678\nTEL;WORK;VOICE:+ 3912345678\nTEL;HOME;VOICE:+ 3912345678\nEND:VCARD\n&#8221;,
&#8220;valueFormat&#8221;: &#8220;CONTACT_INFO&#8221;
}


---


