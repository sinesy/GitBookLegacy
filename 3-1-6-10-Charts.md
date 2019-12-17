# Charts

A chart panel is a panel containing a Google Chart. These charts have been designed to address the need for showing aggregate data in a variety of different ways.

![](http://4wsplatform.org/wp-content/uploads/2015/12/2016-07-05_bn-1024x522.jpg)

When the user chooses this kind of panel in the "Add window" wizard, a few settings must be provided.

![](http://4wsplatform.org/wp-content/uploads/2015/12/chartDetail-1024x522.jpg)

* **Width**  and H **eight**  are mandatory fields.
* Check  **Auto load data**  if you want to load data after the chart panel has been rendered.
* **Title HV Axis is** property that specifies the title of the horizontal or vertical axis.
* **MinMax Value H Axis** : Moves the min or max value of the horizontal axis to the specified value; this will be leftward in most charts.
* **Increment H Axis** : Replaces the automatically generated X-axis ticks with the specified array. The array values start from Min Value and create tick with +Increment formula.
* **MinMax Value V Axis** : Moves the min or max value of the vertical axis to the specified value; this will be leftward in most charts.
* **Increment V Axis** : Replaces the automatically generated Y-axis ticks with the specified array. The array values start from Min Value and create tick with +Increment formula.
* **Legend Field** : field of the legend.
* **Unique query for all series** , ** Series List** : check it if you want to define a query common to all the series and another query to control how many times to execute the first query, that is to say, one for each record read by the latter query.
* **Options** : this field allows to add optional settings , usually to customize the default behavior of a chart, according to the Google Chart options. Example:

```js
legend: {position: 'none'}, colors:['#ff6600', '#779aab']
```

In the next form the user can define any number of series.

![](http://4wsplatform.org/wp-content/uploads/2015/12/chartFields-1024x489.jpg)

* **Legend Field, Series Field:**  if the user has checked "Unique query" for all the series and has specified the Series List in the previous panel, then these fields are enabled.
* **Color** : set the color of a series.
* **Business Component, V Axis Field, H Axis Field** : a query of series and relative fields of V and H axis.

  **Note** : if the user has selected a gauge or geo chart, then it is allowed to set other options.  
  After the window creation, the user can optionally create a filter panel connected to the chart panel just created.  
  Please bear in mind that when a filter panel is created, all filter contrals defined within it are disabled. Consequently, you have to select which filter fields will be visible.  
  Finally, if you want to apply a \(hidden\) filter without a filter panel, i.e. without prompting the user to specify the filter value, you have to create an action containing:

```js
baseParamsChartPanelXXX.filterNames = ‘field’;
baseParamsChartPanelXXX.filterValues = ‘value’;
baseParamsChartPanelXXX.filterOps = ‘=’;
baseParamsChartPanelXXX.filterCaseSensitives = ‘false’;
drawChartXXX();
```

This javascript action should be linked to the "Before loading data" event of the chart panel.

---

### **Example to colorize columns with a single series:** 

**NOTE:**  **This shouldn’t be done with lots of columns/data since it involves overwriting a function by specifying all the chart columns again. Do it only if you have few columns.**  


As can be seen on the relative Google Docs page \(this example considers column charts\) you might want to colorize different columns with different colors even if you have a single serie, check example below.

![](http://4wsplatform.org/wp-content/uploads/2015/12/singleSerieColor.jpg)

![](http://4wsplatform.org/wp-content/uploads/2015/12/singleSerieMultipleColors.jpg)

As explained in the Google documentation, there’s a column type called **role**  that helps us on achieving this:

```js
var data = google.visualization.arrayToDataTable([
         ['Element', 'Density', { role: 'style' }],
         ['Copper', 8.94, '#b87333'],
         ['Silver', 10.49, 'silver'],
         ['Gold', 19.30, 'gold'],
         ['Platinum', 21.45, 'color: #e5e4e2' ],
]);
```

In Platform we can do it by overwriting the chart column declaration inside an action, such as the “After Data Load” on the related grid.  
In this example we only had 4 columns so we declared an array with colors codes and with a cycle we assigned the color code to the related column

```js
function getChart292DataStoreWithStyles(list) {
  var data = new google.visualization.DataTable();
  data.addColumn('string', Ext.translate.Cache.getTranslation('CHART_TITLE.292.DESCRIPTION_IT'));
  data.addColumn('number', Ext.translate.Cache.getTranslation('CHART_TITLE.292.CHART_VALUE'));
  data.addColumn({type:'string', role:'style'});
  var colors = ['#5c403c', '#ff6600', '#779aab', '#A79069']
  for(var i=0; i&lt;list.length; i++) {
    data.addRow([
      list[i].descriptionIt,
      list[i].chartValue,
            colors[i]
    ]);
  };
  return data;
};
```

---

### Special charts

Some charts requires a specific number of mandatory fields to correctly work. In the following sections it is reported how to correctly set up a chart.



**Timelane**

This chart requires always 4 mandatory fields. Common misconfiguration errors are reported in the section below.

For additional settings, see: [https://developers.google.com/chart/interactive/docs/gallery/timeline](https://developers.google.com/chart/interactive/docs/gallery/timeline)

Common cases:

1 - hide the first cell \(lane name\)

In order to do it, you can use Options multitext field in the Chart definition panel and set the following setting:

```js
timeline: { colorByRowLabel: true }
```

2 - make the chart horizontally scrollable

The default behavior of charts is to autofit themselves to the available space provided by their container.

In case you want to distinguish between the available container space \(defined at runtime, since it depends on the browser page size\) and the chart width \(which can be larger\), you have to include in the xtheme.css a CSS scriptlet as follows:

```css
.x-chart-panel-39 {
  overflow-x: scroll;
  overflow-y: hidden;
  width: 400px;
}
```

where the CSS name must always defined as x-chart-panel + the panel id

the width should be relatively lower than the real chart length, which is consequently auto enlarged, according to the provided timing for activities.



---

### Common mistakes

Not all charts works in the same way and require the same configuration. When configuring charts, you have to pay attention to the settings you define, according to the chart type.  
These are the most common mistakes made when configuring charts:

* **Any chart –** the SQL select linked to the chart should always have \(at least\) two fields: one used by the horizontal axis, the other for the vertical axis. While the second must be a number value, the first could be a numeric or text value. Of course this point of view\(vertical/horizontal axis\) cannot be applied for charts where there is not a cartesian diagram, as for pies or donuts. Anyway, the concept is the same: a couple of values is required for each data to show: a value and a corresponding “label”
* **Donut/Pie**  – the legend must be a text type value; a common error is to pass a numeric value, like when you are showing the distribution per year and the sections of the pie represent different years: in such case, you have to convert the numeric year in a text value, when defining the SQL query in the business component: this is the right place when you have define precisely the data type for each field in the select clause
* **Gauge**  – a list of gauges are shown for each record read by the defined SQL query. A single column in the SQL selectis required: if you define more than one field in the SQL select, then the number of gauges will be the sum of the records for each field in the select. A common mistake is thinking that a field in the select is required for the legend and a second field for the corresponding values, as for other charts: a gauge does not work in that way. A single field in the select is needed: the field name will be used as the gauge legend, the values for each record as the value of the gauge.
* **Geolocation**  – this chart is based on the use of Google Maps: in order to use it, you have to purchase a Google account and activate a key for the Google Maps Javascript API. In case the didn’t to that, you will not be able to show the right content in the chart: it will not due to Platform, but on a wrong configuration on your Google account/APIs and that is beyond the support that the Platform team can provide. Additional information about Google configuration can be found here.
* **Timelane** - this chart requires 4 mandatory columns: 
  * a lane name, which can include multiple activities along the time, each having the same lane name; a common error is not to define it as a text type
  * a description, related to the activity to draw into a lane
  * start time, related to the initial time of the activity to draw; a common mistake is to pass forward a null value or provide a not date value
  * end time, related to the final time of the activity to draw; a common mistake is to pass forward a null value or provide a not date value

---



