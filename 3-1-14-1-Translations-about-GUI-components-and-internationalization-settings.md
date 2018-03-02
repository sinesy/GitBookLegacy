# Translations about GUI components and internationalization settings

A functionality named "Translations" is available through the menu item: it allows the user to set every single translation related to the GUI defined through the App Designer, for each declared language.  
The feature is composed of an editable grid, reporting for each row, the component to translate and the description for each language. The grid content is filtered according to the selected node in the tree on the left.  
The tree organizes all the translations according to the type:

* **Windows**  – includes all defined windows and for each window, all the panels included in it
* **Static**  combobox values – here all static comboboxes defined in Selectors are reported: for each selector, the items for it are reported
* **Button text**  – includes all the buttons defined in any panel
* **Popup title**  – includes all the commands defined in popup menus
* **Custom**  – includes all custom translations, defined manually by the user \(through the Add button\)
* **Audit**  – includes all the translations involved with the Data Audit functionality
* **Menu items**  – includes all the translations for folders and items in the application menu

![](http://4wsplatform.org/wp-content/uploads/2018/01/translations.png)

**How the translations are generated**  
When creating a new component through the Designer, such as a label,  **the user**  has only  **provided one**   **description**  for the label, so  **this description is applied for all the languages** . Afterwards, the user can exploit the "Translations" feature to  **change the description for any language**  related to that label.

**How to work with translations**  
The best way to find a panel is to work with the filter on the left: just expand Windows node and then select the right window and select the panel you are interested in, to show its translation in the grid on the right.  
In order to make it easier the search for a specific component in this dictionary of translations, you can always use the  **quick filter panel**  by right clicking on a cell of that grid.  
Moreover, there is a ** filter panel**  above the editable grid: it is possible to show in the grid only a subset of the whole dictionary, by showing only the ones:

* to manage – control labels/column headers declared as “to manage”, i.e. visible or not, but in any case managed by the UI
* visible –control labels/column headers declared as “visible”, i.e. shown as default behavior
* hideable –control labels/column headers declared as “hideable”, i.e. they can be visible or not currently, but they could be shown at some time
* exportable – UI components which will be exported when exporting metadata

**Custom translations**  
In addition to the "Translations" functionality, there is also a " **Custom translations** " node in the tree: it can be used to show all ad hoc translations already defined and to add new ones.  
Moreover, you can customize the default translations provided through the first feature. If the same entry is defined as a custom translation, this one has priority over the default translation.  
In order to figure out when "Custom translations" comes in handy, it is important to focus on the deploy task, from the development environment to the next one, such as test or production.  
During the deploy activity, all metadata defined using the App Designer are exported and imported in the next environment, including the translations stored through the "Translations" functionality; however, "Custom translations" are not imported: that means that for each environment it is possible to define specific translations, if needed, that overwrite the default ones.  
Apart from translations, this feature also manages internationalization settings, that is to say, the way data should be formatted independently of the specific panel \(grid, form, etc\).  
A date value can be formatted with different separators among year, month, day, hours, minutes \(e.g.  **2015-01-01**  vs  **2015/01/01** \) and these parts can be set in different orders \(e.g.  **2015-31-12**  vs  **31-12-2015** \).  
Similarly, numbers can be formatted in different ways: decimal symbol, thousand symbol, grouping or not, numbers of digits before and after the decimal symbol and so forth.  
All these settings have already a default value, for each language used.  
In case these settings must be overridden, it is possible to reset them, by adding entries in the Translations window, according to the following list of entries:

| Entry | Example of value | Meaning |
| :--- | :--- | :--- |
| common.extdateformat | Y/m/d | define how year, month and day of month must be showed, for date \(only\) values |

  
\|  **Entry**  \|  **Example of value**  \|  **Meaning**  \|  
\| :--- \| :--- \| :--- \|  
\| common.extdateformat \| Y/m/d \| define how year, month and day of month must be showed, for date \(only\) values \|  
\| common.extdatetimeformat \| Y/m/d H:i \| define how year, month and day of month + hours and minutes must be showed for date+time values \|  
\| common.currencysymbol \| $ \| currency symbol to use when defining numeric columns/controls as currency type components \|  
\| common.decimalsymbol \| . \| decimal symbol to use with numeric columns/controls \|  
\| common.thousandsymbol \| , \| thousand symbol to use with numeric columns/controls \|  
\| common.groupingsymbol \| , \| grouping symbol to use with numeric columns/controls \|  
\| common.showcenturyindateformat \| true\|false \| define if the century must be showed in years \|  
\| common.timeformat \| HH:mm \| define how hours and minutes must be showed for time \(only\) values \|  
\| common.exttimeformat \| G:i \| define how hours and minutes must be showed for time \(only\) values \|

---



