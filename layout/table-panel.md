**Table panel \(responsive layout\)**  
This container allows to include any number of sub-panels, organized with different  **widths** ,  **heights**  and  **row/column spans** .  
This is the most flexible layout and also the most complex to configure.  
It allows to organize sub-panels in a way that they can use all the available space. Moreover, with different display sizes or when resizing the browser window, the organization of the panels can change. At panel container level, it is possible to set the maximum number of columns allowed: the content of the container will be then calculated at run-time, according to the available space.

For example, suppose you set the table panel container with a max nr of column = 2 and that you have 3 panels to add: the first is a filter panel having a fixed width and height of 400 pixels, the second panel is a grid \(a component having a dynamic width\), the third panel a detail form, again with afixed width and height of 400 pixels.  
With these settings, if your browser has a length of 1000 pixels could easily show the filter and grid in the first row and the detail form in the second. But when reducing the browser window to less than 400 pixels, the grid would automatically moved to the second row, along with the detail form.  
That behavior is what usually is called a responsive layout: a container whose content can be re-organized automatically, according to the current available space.

![](http://4wsplatform.org/wp-content/uploads/2018/01/table.png)

It is essential to understand how to definecorrectly a table panel. At panel level there is a  **Nr of columns**  property to set.  
For every sub-panel, you have to define an  **Height** .  
For every sub-panel which does not have a dynamic width \(panels having a dynamic width are grids and charts\), you have to define a  **Width**  as well, otherwise it will not be possible to render it correctly.  
Optionally, for every sub-panel you can define also the  **Column span** , i.e. the number of cells that the panel has to occupy horizontally.  
Optionally, for every sub-panel you can define also the  **Rows span** , i.e. the number of cells that the panel has to occupy vertically.  
Thanks to all these settings, you can arrange the window content in a very flexible way.  
Please pay attention to the mandatory properties reported above: if you have not set them, the window content will not be rendered correctly, when executing the web application.



