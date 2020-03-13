**Responsive panel**

This kind of layout makes a form/filter panel content dynamically rendered on a variety of devices and windows having different screen sizes.

A form/filter panel having this layout adapts the content to the viewing environment, so that when there is not enough horizontal space to host all controls designed to be in the same row, these are re-arranged on the next lines. It means that a vertical scrolling can be needed, when there is not enough horizontal space and controls are arranged on multiple lines.      


This layout is based on the definition of

* a predefined **number of columns **\(field “Columns number”\), defined at panel level

* for each control to show, a few mandatory properties must be defined:

* * an **Height**

  * the minimum width is equals **Width**

  * a maximun Width \(field named “Max Width”\)

  * the **percentage occupied by the control **\(field named “% Occuped”\) with respect to the number of columns; in the example below, the first line contains 3 controls having the same length: 1/3 \(to be more precise: 33%+33%+33%\), whereas the second line contains only 2 control, where the first is 33% and the second 66%
* **Controls under label **\(above the control, on the left of it\)

Example with 3 pre-defined columns and no maxWidth set, except for “Sex”:

![](https://lh5.googleusercontent.com/C9_r7HXp8mVVu2fcsfCTG2H-qrtgIWfyLZlkZSOZj8EpyobLOqiq8RZXlVcO18U-h4lOi7WdTBTOyVCopDdPn8tzgHgGVns9sgYJBtRptK4RxqQpFLlN1PYLPtkzgS49eCVAB4Gw)  


Starting from these settings \(where N is the default number of columns per row\), the content of the panel is arranged: when there is not enough space \(in horizontal\) to maintain N controls in the same row, the last ones are moved to the next line and so on.

Arrangement is carried out by evaluating the min/max width for each control and comparing them with the current available space \(current panel width\) and according to it, they are moved to the next lines if there is not enough space of N controls for each row.

Example with 3 default columns for row, but available space only for 2 columns:

![](https://lh5.googleusercontent.com/5JcwzzoQscbs4vtu-qGp-ArcS-3_AQ41qaIiRR3dcr5gikjfS6I-muJ3ZDtLUfM_G_PD8SdQJCsFjW0xZmDz6SDR49dUti1oiqfzaFKnMS1JplhOciLTkbwbBphcOjTp_Y1V8Kb_)

As soon as the available horizontal space is reduced, controls are arranged until they reach the minimum number of columns: 1

Example:

![](https://lh6.googleusercontent.com/QAvRM1jM8WL4KI2FYsGfSi8DXuQr_V2BjOKUzk3YCZlGRbB5Ktm_-Cg3Ap-lMq7l8xo4yLEAZZ4JGZ9K0zXRPIs6HLAKBbWtBxM23ciccCd5PszIl2i58ax3jJdNpUMlAFF9AOh9)

Optional settings for each control are:

* **Max Width**; if not set, a control will be stretched to all the available space, so that no empty space is left on the panel \(on the right\); if set, this value represents the max width for the control: helpful especially for input controls which should be rendered with a small width, like age, sex, etc.

An alternative approach involves the definition of an optional setting at panel level:

* **Max Width** of a panel; if set, the specified columns \(N\) will occupy no more than the specified width: this solution is good for windows designed for a specific resolution \(e.g. 1024x… pixels\), but has the drawback of let an empty space on the right \(not good for displays having a larger resolution\)

When the max width for the panel is set, a “larger than needed” panel would be rendered as follows:

![](https://lh5.googleusercontent.com/wh7qi78MDB4ab07B6s6ofx8dJ6EtimzY4WDK-CoXDxV2EzgwsVlyf0BjypG632u39y_Is4NXbETRvqLkhwhYVFUo9RusydNHA4jQsOiTRx_DT-0417D_jR5LBOQjtTV6-_Vo1vP8)

As long as the available space is reduced, a smaller number of columns will be used and consequently controls will be re-arranged:

![](https://lh5.googleusercontent.com/2hMF_5IAJmBtdXjDAhZohMi8dZrRFXRDSzoTFdY83Z7bt2Qtc16_BmS64PDz4O1hmGQU5bO4OB-oBv1hYkAF6k2W6OCb-pRLbfz5UPOTuZZxWVW4re-VuIs9cTaGJ_E9mH_IYj-7)

Finally, as for the first scenario, 1 only column will be used:

![](https://lh6.googleusercontent.com/ZZzBnCGTXX7ZYxV-3wrWqjWJbJwpZiRxrMpTA9ESPx1ixyy_XhJDtY-cb8y7CefuFzNVdhYovK-j4L0YTwcSO8wVNDolnvFX8xoHQGpn0q0tkQAJ6Ts8GHuCwLY6h78Qx-0Zeawt)

    

## Bad & Good practises

Here it is a list of things no to do when configuring a form/filter panel



**Do not set invalid percentages for controls**

Bear in mind that the total percentage of control widths for a line must never be more than 100%.

When you have a row having 3 controls with same width, you have to set the percentage with a value like: 33% + 33% + 33%

A wrong configuration would be: 33% + 33% + 34%

Theoricaly, the latter choice would be better, since the total percentage is exactly 100%, but this can lead to an unaesthetic rendering of the controls when there is not enough space for all of them: in such a case, there would be a control a bit larger than the others \(34%\) rendered on the next column; consequently, it would be better to maintain always the same percentage, rather than rounding one of them to fit a 100%.

Another common mistake is setting percentages of 33+33+33 for a row and 100% for another row \(when a control should occupy all available space\). The right percentage for the latter is 99%



**Do not arrange controls with a large number of columns**

Pay attention to the number of columns you set for a panel: 1,2,3,4 seem to be good numbers, not only because they arrange a small number of controls over a line, but also because they allow to define percentages for controls easy to define:

1 column: 100%

2 columns: 50% + 50%

3 columns: 33% + 33% + 33%

4 columns: 25% + 25% + 25% + 25%

This is not true for larger number of columns, so avoid to use a large number of columns or a number of columns not easy to divide by.



**Do not set max width for every control**

If you set a min=max width for each control, controls are bounded to an exact width and this can lead to empty spaces among them, especially in case of a form/filter panel where a max width has not been set.

A better choice would be to classify controls in two groups:

* controls which should have a fixed width, as for controls representing gender, ag \(i.e. width a small number of digits to type in\); these controls can have a fixed width, so they are aesthetically good to see

* controls containing large descriptions, as for corporate name, address, etc., where it would be better to let them stretch to all available space



**Do not arrange controls randomly**

Pay attention to the position when you arrange controls, especially for the ones having a different percentage with respect to the others.

Let’s take this example, where there are 3 columns and controls have 33% width each, except for the address, which contains a large description and hence is set with a 66% width. The position for the last control can make the difference. Look at this \(wrong\) arrangement:

| name | surname | city |
| :--- | :--- | :--- |
|  | address | zip code |

If this panel were resized to a smaller width so that only 2 columns can be showed, the responsive layout would re-arrange it in this way:

| name | surname |
| :--- | :--- |
| city | SPACE NOT USED |
|  | address |
| zip code | SPACE NOT USED |

which is aesthetically not good, because there are empty spaces and it occupies 4 lines, instead of 3, which could lead to vertically scroll the screen to show part of it.

A better choice would have been:

| name | surname | city |
| :--- | :--- | :--- |
|  | zip code | address |

When this panel is resized to a smaller width so that only 2 columns can be showed, the responsive layout would re-arrange it in this way:

| name | surname |
| :--- | :--- |
| city | zip code |
|  | address |

This is clearly a better choice, since it only requires 3 lines to render the whole content and there are not empty spaces among the controls.

