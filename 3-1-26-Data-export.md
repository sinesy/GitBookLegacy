# Data export

4Ws.Platform allows to export data from a grid. In order to activate this feature, you have to select the check-box "Enable Export" on the grid pane settings inside the Web Designer.  
After doing that, an export button will appear in the grid toolbar. When pressing on it, an export dialog will be shown: throught it the user can choose which columns to export. The default setting would export all visibile columns.  
The export task is then started: exported data inherits the filtering and ordering conditions currently applied to the grid, but data pagination is ignored.  
Please not that there is a limit in the amount of exported data: no more than 100.000 records can be exported, since the export task consumes a significan amount of resources on the serfver side.  
This limit can be changed in the Platform Enterprise Edition through a global parameter.

An export process in CSV format can also be started as a web service and therefore automated, for instance a a web service scheduled using the embedded scheduler available in the in the Platform Enterprise Edition.  
This is an example of such an URL, used to export data:

```js
http://host:port/contextpath/getlist?applicationId=...&amp;functionId=...&amp;compId=...&amp;panelId=...&amp;quickFilterNames=...,&amp;quickFilterValues=...,&amp;quickFilterOps=....,&amp;quickFilterCaseSensitives=...,&amp;sort=&amp;dir=&amp;exportColumns=...&amp;exportAttributes=...&amp;exportColWidths=...&amp;exportFormat=CSV&amp;title=...&amp;directExport=true
```

This URL can be invoked only when a web client has been previously authenticated, or then an auth token has been provided too.  
For each filtering condition to apply, 4 parameters must be filled in:

* quickFilterNames – attribute names, separated by a comma \(,\)
* quickFilterValues – attribute values, separated by a comma \(,\)
* quickFilterOps – list of operators to use when filtering data \(e.g. = or like or &lt;, …\), separated by a comma \(,\)
* quickFilterCaseSensitives – list of conditions to use when evaluating a text value: used to specify whether the attribute must be put in uppercase or not \(allowed values: true or false\).

For each sorting condition to apply, 2 parameters must be filled in:

* sort – attribute names, separated by a comma \(,\)
* dir – list of sorting versus \(ASC or DESC\), separated by a comma \(,\)

Meaning of the other parameters:

* exportColumns – list of column headers to report as the first row of the generated document, , separated by a comma \(,\)
* exportAttributes – list of attributes to export, separated by a comma \(,\); they must be a subset of the attributes supported by the grid
* exportColWidths – list of column widths, expressed in pixels, separated by a comma \(,\)
* exportFormat – format to use when exporting data: CSV

---



