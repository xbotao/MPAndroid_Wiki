This wiki entry is intended to provide better insight into the **data model** behind _MPAndroidChart_.

The `ChartData` class is the baseclass of all data classes (subclasses), like `LineData`, `BarData`, ... and so on. It is used to provide data for the `Chart` via the `setData(...)` method of the chart.

```java
public class LineData extends ChartData { ...
```

The following mentioned methods are implemented in the `ChartData` class and can therefore be used for all subclasses.

### Styling data
 - <code>setValueTextColor(int color)</code>: Sets the color of the value-text (color in which the value-labels are drawn) for all `DataSets` this data object contains.
 - <code>setValueTextColors(List<Integer> colors)</code>: Sets a list of colors to be used as value colors.
 - <code>setValueTextSize(float size)</code>: Sets the size (in dp) of the value-text for all `DataSets` this data object contains.
 - <code>setValueTypeface(Typeface tf)</code>: Sets the `Typeface` for all value-labels for all `DataSets` this data object contains. 
 - <code>setValueFormatter(ValueFormatter f)</code>: Sets a custom `ValueFormatter` for all `DataSets` this data object contains, more on the `ValueFormatter` [here](https://github.com/PhilJay/MPAndroidChart/wiki/The-ValueFormatter-interface).
 - <code>setDrawValues(boolean enabled)</code>: Enables / disables drawing values (value-text) for all `DataSets` this data object contains.

### Getters / Convenience
 - <code>getDataSetByIndex(int index)</code>: Returns the `DataSet` object at the given index in the data-objects `DataSet` list.
 - <code>contains(Entry entry)</code>: Checks if this data object contains the specified Entry. Returns true if so, false if not. NOTE: Performance is pretty bad on this one, do not over-use in performance critical situations.
 - <code>contains(T dataSet)</code>: Returns true if this data object contains the provided `DataSet`, false if not.

### Clearing
 - <code>clearValues()</code>: Clears the data object of all `DataSet` objects and thereby all `Entries`. Does not remove the provided x-values. 

### Highlighting
 - <code>setHighlightEnabled(boolean enabled)</code>: Set this to true to allow highlighting via touch for this `ChartData` object and all underlying `DataSets`.
 - <code>setDrawVerticalHighlightIndicator(boolean enabled)</code>: Enables / disables the vertical highlight-indicator-line. If disabled, the indicator is not drawn.
 - <code>setDrawHorizontalHighlightIndicator(boolean enabled)</code>: Enables / disables the horizontal highlight-indicator-line. If disabled, the indicator is not drawn.

### Dynamic Data
- <code>notifyDataChanged()</code>: Lets the data object know it's underlying data has changed and performs all necessary recalculations.

For ways of adding and removing data from an existing data object, please visit the [dynamic & realtime data](https://github.com/PhilJay/MPAndroidChart/wiki/Dynamic-&-Realtime-Data) section.