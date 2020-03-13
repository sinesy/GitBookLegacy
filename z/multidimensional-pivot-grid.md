# Multi-dimensional Pivot Grid

This kind of read-only grid allows to show numeric values grouped together, according to some other dimensions, reported on the horizontal and vertical axis.

![](/assets/pivot.png)

It is possible to group a numeric quantity using a variety of different grouping predefined functions:

* Count

* Count Unique Values

* List Unique Values

* Sum

* Integer Sum

* Average

* Median

* Sample Variance

* Sample Standard Deviation

* Minimum

* Maximum

* First

* Last

* Sum over Sum

* 80% Upper Bound

* 80% Lower Bound

* Sum as Fraction of Total

* Sum as Fraction of Rows

* Sum as Fraction of Columns

* Count as Fraction of Total

* Count as Fraction of Rows

* Count as Fraction of Columns

It is also possible to show the resulting aggregation of values in different type of charts:

* Table

* Table Barchart

* Heatmap

* Row Heatmap

* Col Heatmap

* Area Chart
* Bar Chart
* Horizontal Bar Chart
* Horizontal Stacked Bar Chart
* Line Chart
* Scatter Chart
* Stacked Bar Chart

* Treemap   

* TSV Export

* Table With Subtotal
* Table With Subtotal Bar Chart
* Table With Subtotal Col Heatmap
* Table With Subtotal Heatmap
* Table With Subtotal Row Heatmap



Moreover, a filter panel can be included in the same window, used to filter the raw data used as input to the pivot grid.



Main features supported by this multi-dimensional pivot table:

* subtotals per column and row
* aggregated data export in TSV format \(text format, based on copy and paste of available data - see that renderer\)
* 17 different types of charts 
* 22 different types of aggregators
* data sort support for dimensions chosen for horizontal/vertical axis
* customization of the UI through CSS
* customization of renderers/aggregators via Javascript



### Defining raw data

Input data for the pivot grid comes from a business component. Every field defined in the SELECT clause for this business component can be used to aggregate data or as a dimension on the horizontal/vertical axis.

Of course, only numeric fields can be used as the aggregated quantity, whereas there is no constraint on fields to use for the horizontal/vertical axis.

It is strongly recommended to **not overpass a limit of 10.000 records as result set for the query** defined for the business component, otherwise the pivot grid could not perform in a few seconds. 

In any case, the business component is limited on the server side to not more than 50.000 records, in order to ensure the correct work of the application server.



### Events

It is available the single cell click event, if needed, in order to execute some other operation. In order to listen to the cell click event, use the "Events" folder in the pivot grid definition window and choose a "Cell click" option.



### Customizing aggregators/renderers

It is possible to define the available aggregator functions and/or renderers by overriding the default setting, where all of them are available for the end user.

In order to fine grained define the aggregators/renderers, use the "Events" folder in the pivot grid definition window and choose the "Before render" option.

Here you can link a client-side javascript action you can use to invoke two available predefined functions: one used to define the aggregators \(deleteAggregator\), the other for renderers \(deleteRenderer\).

For example, in case you want to maintain one only aggregator, the sum, and one only renderer, the table, you have to include the action as many deletexxx invocations as the number of renderers/aggregators available but one:

```js
//deleteRenderer("Table");
deleteRenderer("Table Barchart");
deleteRenderer("Heatmap");
deleteRenderer("Row Heatmap");
deleteRenderer("Col Heatmap");
deleteRenderer("Area Chart");
deleteRenderer("Bar Chart");
deleteRenderer("Horizontal Bar Chart");
deleteRenderer("Horizontal Stacked Bar Chart");
deleteRenderer("Line Chart");
deleteRenderer("Scatter Chart");
deleteRenderer("Stacked Bar Chart");
deleteRenderer("Treemap      ");
deleteRenderer("TSV Export    ");
deleteRenderer("Table With Subtotal");
deleteRenderer("Table With Subtotal Bar Chart");
deleteRenderer("Table With Subtotal Col Heatmap");
deleteRenderer("Table With Subtotal Heatmap");
deleteRenderer("Table With Subtotal Row Heatmap");

deleteAggregator("Count");
deleteAggregator("Count Unique Values");
deleteAggregator("List Unique Values");
//deleteAggregator("Sum");
deleteAggregator("Integer Sum");
deleteAggregator("Average");
deleteAggregator("Median");
deleteAggregator("Sample Variance");
deleteAggregator("Sample Standard Deviation");
deleteAggregator("Minimum");
deleteAggregator("Maximum");
deleteAggregator("First");
deleteAggregator("Last");
deleteAggregator("Sum over Sum");
deleteAggregator("80% Upper Bound");
deleteAggregator("80% Lower Bound");
deleteAggregator("Sum as Fraction of Total");
deleteAggregator("Sum as Fraction of Rows");
deleteAggregator("Sum as Fraction of Columns");
deleteAggregator("Count as Fraction of Total");
deleteAggregator("Count as Fraction of Rows");
deleteAggregator("Count as Fraction of Columns");
```

### 

### Theme

The pivot grid content can be customized in terms of font and colors. 

The **css/xtheme.css** file defined at sub-context level \(for your application\) can be used to override the default CSS settings.

In this example, a few settings are changed: font for comboboxes and selector dialogs, background color for the result grid:

```css
.pvtAxisContainer li span.pvtAttr {
    font-size:11px;
}

.pvtFilterBox{
    font-size:11px;
}

.pvtCheckContainer{
    font-size:11px;
}

table.pvtTable thead tr th, table.pvtTable tbody tr th {
    background-color: #EEEEEE;
}
```



