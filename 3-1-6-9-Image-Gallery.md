# Image Gallery

An image gallery is a special panel containing a list of images \(and optionally a caption below it\) arranged horizontally and vertically; the number of images per row is automatically reckoned according to the current width of the window, i.e. of the web page opened in the browser.  
When the user chooses this kind of panel in the "Add window" wizard, a few settings must be provided:

* image title \(optional, can be hidden\)
* business component \(for  **list of data** \) containing the column whose content allows to show an images \(for instance, an "Image path" or "Image URL" column type\); for each record read through this business component, an image will be viewed within the image gallery panel, starting from left to right, top-down
* caption field \(optional\); if specified, it is a column provided by the business component whose content will be showed below each image; it should be a text type content

In order to correctly render the image gallery panel, the user has also to specify which column contains the data needed to show the image for each record; in order to specify that column, after creating the panel, the user has to open it, click on its columns definition and choose the column to set as the "image" column, by setting the column type to "Image path" or "Image URL".

---



