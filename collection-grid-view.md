# Collection grid view

For displaying list of forms in grid like a photo gallery we can use the collection grid view.

Each cell of the grid contains the same form panel fill with the record returned by the business component.

Below are some advantages:

* You can have a fixed number of column \(the grid scroll vertically\) or a fixed number of row \(the grid scroll horizontally\)
* If the number of column is fixed you have to specify the row height, otherwise if is the number of row fixed you have to specify the column width.
* You may have a list draw in more than 1 column but each item of the list have same height and width
* Using GridLayoutManager we can split row more than one times

**Example 1**![](/assets/vertical_scroll.png)In this example the number of column is set to 4, the row height is fixed and the grid scroll vertically.

**Example 2**![](/assets/horizontal_scroll.png)In this example the number of row is set to 2, the row width is fixed and the grid scroll horizontally.

---

