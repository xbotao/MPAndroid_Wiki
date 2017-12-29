This wiki page focuses on the `AxisBase` class, the baseclass of both `XAxis` ([XAxis](https://github.com/PhilJay/MPAndroidChart/wiki/XAxis)) and `YAxis` ([YAxis](https://github.com/PhilJay/MPAndroidChart/wiki/YAxis)). Introduced in v2.0.0

The following methods mentioned below **can be applied to both axes**.

The axis classes allow specific styling and consist (can consist) of the following components/parts:
 - The labels (drawn in vertical (y-axis) or horizontal (x-axis) alignment), which contain the axis description values
 - A so called "axis-line" that is drawn directly next to and parallel to the labels
 - The "grid-lines", each originating from an axis-label in horizontal direction
 - `LimitLines`, that allow to present special infomation, like borders or constraints

### Control which parts (of the axis) should be drawn
 - <code>setEnabled(boolean enabled)</code>: Sets the axis enabled or disabled. If disabled, no part of the axis will be drawn regardless of any other settings.
 - <code>setDrawLabels(boolean enabled)</code>: Set this to true to enable drawing the labels of the axis.
 - <code>setDrawAxisLine(boolean enabled)</code>: Set this to true if the line alongside the axis (axis-line) should be drawn or not.
 - <code>setDrawGridLines(boolean enabled)</code>:  Set this to true to enable drawing the grid lines for the axis.

### Customizing the axis range (min / max)
 - <code>setAxisMaximum(float max)</code>: Set a custom maximum value for this axis. If set, this value will not be calculated automatically depending on the provided data. 
 - <code>resetAxisMaximum()</code>: Call this to undo a previously set maximum value. By doing this, you will again allow the axis to automatically calculate it's maximum.
 - <code>setAxisMinimum(float min)</code>: Set a custom minimum value for this axis. If set, this value will not be calculated automatically depending on the provided data. 
 - <code>resetAxisMinimum()</code>: Call this to undo a previously set minimum value. By doing this, you will again allow the axis to automatically calculate it's minimum.
 - <code>setStartAtZero(boolean enabled)</code>: _Deprecated_ - Use `setAxisMinValue(...)` or `setAxisMaxValue(...)` instead.
 - <code>setInverted(boolean enabled)</code>: If set to true, this axis will be inverted which means the highest value will be on the bottom, the lowest value on top.
 - <code>setSpaceTop(float percent)</code>: Sets the top spacing (in percent of the total axis-range) of the highest value in the chart in comparison to the highest value on the axis. 
 - <code>setSpaceBottom(float percent)</code>: Sets the bottom spacing (in percent of the total axis-range) of the lowest value in the chart in comparison to the lowest value on the axis. 
 - <code>setShowOnlyMinMax(boolean enabled)</code>: If enabled, this axis will only show it's minimum and maximum value. This will ignore/override the defined label-count (if not forced).
 - <code>setLabelCount(int count, boolean force)</code>: Sets the number of labels for the y-axis. Be aware that this number is not fixed (if force == false) and can only be approximated. If force is enabled (true), then the exact specified label-count is drawn - this can lead to uneven numbers on the axis.
 - <code>setPosition(YAxisLabelPosition pos)</code>: Sets the position where the axis-labels should be drawn. Either INSIDE_CHART or OUTSIDE_CHART.
 - <code>setGranularity(float gran)</code>: Sets the minimum interval between the y-axis values. This can be used to avoid value duplicating when zooming in to a point where the number of decimals set for the axis no longer allow to distinguish between two axis values. 
 - <code>setGranularityEnabled(boolean enabled)</code>: Enables the granularity feature that limits the interval of the y-axis when zooming in. Default: false

### Styling / modifying the axis
 - <code>setTextColor(int color)</code>: Sets the color of the axis labels.
 - <code>setTextSize(float size)</code>: Sets the text-size of the axis labels in dp.
 - <code>setTypeface(Typeface tf)</code>: Sets a custom `Typeface` for the axis labels.
 - <code>setGridColor(int color)</code>: Sets the color of the grid-lines of this axis.
 - <code>setGridLineWidth(float width)</code>: Sets the width of the grid-lines of this axis.
 - <code>setAxisLineColor(int color)</code>: Sets the color of the axis-line of this axis.
 - <code>setAxisLineWidth(float width)</code>: Sets the width of the axis-line of this axis.
 - <code>enableGridDashedLine(float lineLength, float spaceLength, float phase)</code>: Enables the grid line to be drawn in dashed mode, e.g. like this "- - - - - -". "lineLength" controls the length of the line pieces, "spaceLength" controls the space between the lines, "phase" controls the starting point.

### Formatting axis values

For formatting axis values, you can use the `IAxisValueFormatter` interface, which is explained [here](https://github.com/PhilJay/MPAndroidChart/wiki/The-AxisValueFormatter-interface). You can use the `axis.setValueFormatter(IAxisValueFormatter formatter)` method to set your custom formatter to the axis.

### Limit Lines

Both axes support so called `LimitLines` that allow to present special information, like borders or constraints. `LimitLines` added to the `YAxis` are drawn in horizontal direction, and in vertical direction when added to the `XAxis`. This is how you add and remove `LimitLines` from the axis:

- <code>addLimitLine(LimitLine l)</code>: Adds a new `LimitLine` to this axis.
- <code>removeLimitLine(LimitLine l)</code>: Removes the specified `LimitLine` from this axis.
- More methods for adding / removing available as well.
- <code>setDrawLimitLinesBehindData(boolean enabled)</code>: Allows to control the z-order between the `LimitLines` and the actual data. If this is set to true, the `LimitLines` are drawn behind the actual data, otherwise on top. Default: false

Limit lines (class `LimitLine`) are (as the name might indicate) plain and simple lines can be used to **provide additional information** for the user. 

As an example, your chart might display various blood pressure measurement results the user logged with an application. In order to inform the user that a systolic blood pressure of over 140 mmHg is considered to be a health risk, you could add a `LimitLine` at 140 to provide that information.

### Example Code
```java
YAxis leftAxis = chart.getAxisLeft();

LimitLine ll = new LimitLine(140f, "Critical Blood Pressure");
ll.setLineColor(Color.RED);
ll.setLineWidth(4f);
ll.setTextColor(Color.BLACK);
ll.setTextSize(12f);
// .. and more styling options

leftAxis.addLimitLine(ll);
```