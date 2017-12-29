The `DataSet` class is the baseclass of all data-set classes (subclasses), like `LineDataSet`, `BarDataSet`, ... and so on. 

```java
public class LineDataSet extends DataSet { ...
```

The DataSet class represents one group or type of entries (Entry) in the `Chart` that belong together. It is designed to logically separate different groups of values inside the `Chart` (e.g. the values for a specific line in the `LineChart`, or the values of a specific group of bars in the `BarChart`).

The following mentioned methods are implemented in the `DataSet` class and can therefore be used for all subclasses.

**Styling data**
 - <code>setValueTextColor(int color)</code>: Sets the color of the value-text (color in which the value-labels are drawn) for this `DataSet` object.
 - <code>setValueTextColors(List<Integer> colors)</code>: Sets a list of colors to be used as value colors.
 - <code>setValueTextSize(float size)</code>: Sets the size (in dp) of the value-text for this `DataSet` object.
 - <code>setValueTypeface(Typeface tf)</code>: Sets the `Typeface` for all value-labels for this `DataSet` object.
 - <code>setValueFormatter(ValueFormatter f)</code>: Sets a custom `ValueFormatter` for this `DataSet` object, more on the `ValueFormatter` [here](https://github.com/PhilJay/MPAndroidChart/wiki/The-ValueFormatter-interface).
 - <code>setDrawValues(boolean enabled)</code>: Enables / disables drawing values (value-text) for this `DataSet` object.

If all values in your whole data object (not data-set) should e.g. have the same color, you can simply call one of the above mentioned on the `ChartData` object.

**Highlighting**
 - <code>setHighlightEnabled(boolean enabled)</code>: Set this to true to allow highlighting via touch for this specific `DataSet`.
 - <code>setDrawVerticalHighlightIndicator(boolean enabled)</code>: Enables / disables the vertical highlight-indicator-line. If disabled, the indicator is not drawn.
 - <code>setDrawHorizontalHighlightIndicator(boolean enabled)</code>: Enables / disables the horizontal highlight-indicator-line. If disabled, the indicator is not drawn.

**Getters / Convenience**
 - <code>contains(Entry entry)</code>: Checks if this `DataSet` object contains the specified `Entry`. Returns true if so, false if not. NOTE: Performance is pretty bad on this one, do not over-use in performance critical situations.