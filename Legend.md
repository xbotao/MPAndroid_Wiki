By default, all chart types support legends and will automatically generate and draw a legend after setting data for the chart. The `Legend` usually consists of multiple entries each represented by a label an a form/shape.

The number of entries the automatically generated legend contains depends on the number of different colors (across all `DataSet` objects) as well as on the `DataSet` labels. The labels of the `Legend` depend on the labels set for the used `DataSet` objects in the chart. If no labels for the `DataSet` objects have been specified, the chart will automatically generate them. If multiple colors are used for one `DataSet`, those colors are **grouped** and only described by (belong to) one label.

For customizing the `Legend`, use you can retreive the `Legend` object from the chart using the `getLegend()` method:

```java
Legend legend = chart.getLegend();
```

**Control if the legend should be drawn**
- <code>setEnabled(boolean enabled)</code>: Sets the `Legend` enabled or disabled. If disabled, the `Legend` will not be drawn.

**Styling / modifying the legend**
 - <code>setTextColor(int color)</code>: Sets the color of the legend labels.
 - <code>setTextSize(float size)</code>: Sets the text-size of the legend labels in dp.
 - <code>setTypeface(Typeface tf)</code>: Sets a custom `Typeface` for the legend labels.

**Wrapping / clipping avoidance**
 - <code>setWordWrapEnabled(boolean enabled)</code>: If enabled, the content of the legend will not clip outside the charts bounds, but instead create a new line. Please note that this reduces performance and is only available for legends below the chart.
 - <code>setMaxSizePercent(float maxSize)</code>: Sets the maximum relative size out of the whole chart view in percent. Default: 0.95f (95%)

**Customizing the legend**
 - <code>setPosition(LegendPosition pos)</code>: Sets the `LegendPosition` which defines where the `Legend` should appear. Choose between RIGHT_OF_CHART, RIGHT_OF_CHART_CENTER, RIGHT_OF_CHART_INSIDE, BELOW_CHART_LEFT, BELOW_CHART_RIGHT, BELOW_CHART_CENTER or PIECHART_CENTER (`PieChart` only), ... and more.
 - <code>setForm(LegendForm shape)</code>: Sets the `LegendForm` that should be used. This is the shape that is drawn next to the legend-labels with the color of the `DataSet` the legend-entry represents. Choose between SQUARE, CIRCLE or LINE.
 - <code>setFormSize(float size)</code>: Sets the size of the legend-forms in dp.
 - <code>setXEntrySpace(float space)</code>: Sets the space between the legend-entries on the horizontal axis.
 - <code>setYEntrySpace(float space)</code>: Sets the space between the legend-entries on the vertical axis.
 - <code>setFormToTextSpace(float space)</code>: Sets the space between the legend-label and the corresponding legend-form.
 - <code>setWordWrapEnabled(boolean enabled)</code>: Should the legend word wrap? / this is currently supported only for BelowChartLeft, BelowChartRight, BelowChartCenter. / you may want to set maxSizePercent when word wrapping, to set the point where the text wraps.

**Setting custom labels & colors**
 - <code>setCustom(int[] colors, String[] labels)</code>: Sets a custom legend's labels and colors arrays. The colors count should match the labels count. Each color is for the form drawn at the same index. A null label will start a group. A (-2) color will avoid drawing a form This will disable the feature that automatically calculates the legend labels and colors from the datasets. Call `resetCustom()` to re-enable automatic calculation (and then `notifyDataSetChanged()` is needed to auto-calculate the legend again)
 - <code>resetCustom()</code>: Calling this will disable the custom legend labels (set by `setCustom(...)`). Instead, the labels will again be calculated automatically (after `notifyDataSetChanged()` is called).
 - <code>setExtra(int[] colors, String[] labels)</code>: Sets colors and labels that will be appended to the end of the auto calculated colors and labels arrays after calculating the legend. (if the legend has already been calculated, you will need to call `notifyDataSetChanged()` to let the changes take effect)

**Example**
```java
    Legend l = chart.getLegend();
    l.setFormSize(10f); // set the size of the legend forms/shapes
    l.setForm(LegendForm.CIRCLE); // set what type of form/shape should be used
    l.setPosition(LegendPosition.BELOW_CHART_LEFT);
    l.setTypeface(...);
    l.setTextSize(12f);
    l.setTextColor(Color.BLACK);
    l.setXEntrySpace(5f); // set the space between the legend entries on the x-axis
    l.setYEntrySpace(5f); // set the space between the legend entries on the y-axis

    // set custom labels and colors
    l.setCustom(ColorTemplate.VORDIPLOM_COLORS, new String[] { "Set1", "Set2", "Set3", "Set4", "Set5" });

    // and many more...
```