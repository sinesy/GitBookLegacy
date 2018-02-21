# Custom code and translations

Optionally, it is possible to develop custom panels, using ExtJS and Warp.ExtJS.  
This custom part of the GUI has to support the same languages of the rest of the interpreted application. This can be accomplished using .properties files to include with the product.  
The programmer has to create a XXX\_YY.properties file for each language, where YY is the language identifier and XXX is the application identifier.  
Consequently, if the application identified by "TEST" has two languages "EN" and "IT" declared, two files should be created as well, for the two languages: TEST\_EN.properties and TEST\_IT.properties.  
Each of them will contain the translations for a specific language, related to the custom part developed using javascript.  
More information about how to include custom artifacts with 4WS.Platform are provided in the section named "Customizations and import .zip file".

---



