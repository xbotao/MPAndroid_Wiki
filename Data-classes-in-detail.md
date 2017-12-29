This wiki entry focuses on the subclasses of the `ChartData` class. 
All other subclasses of `ChartData` not mentioned here do not provide any specific enhancements.

**BarData** (class `BarData`)
 - <code>setGroupSpace(float percent)</code>: Sets the space between groups of bars of different datasets in percent of the total width of one bar. 100 = space is exactly one bar width, default: 80
 - <code>isGrouped()</code>: Returns true if this data object is grouped (consists of more than 1 `DataSet`), false if it is not.

**ScatterData** (class `ScatterData`)
 - <code>getGreatestShapeSize()</code>: Returns the largest shape-size across all `ScatterDataSets` this data object contains.

**PieData** (class `PieData`)
 - <code>getDataSet()</code>: Returns the `PieDataSet` object that is set for this data object. `PieData` objects cannot contain multiple `PieDataSets`.
 - <code>setDataSet(PieDataSet set)</code>: Sets the `PieDataSet` this data object should represent.

**BubbleData** (class `BubbleData`)
 - <code>setHighlightCircleWidth(float width)</code>: Sets the width of the circle that surrounds the bubble when in highlighted state for all `BubbleDataSet` objects this data  object contains, in dp.

**CombinedData** (class `CombinedData`)

This data object is designed to contain instances of all other data objects. Use the `setData(...)` methods to provide the data for this object. This is used for the `CombinedChart` only.

This is what it looks like internally:

```java
public class CombinedData extends ChartData {
    
    // ...

    public CombinedData(List<String> xVals) { ... }

    public CombinedData(String[] xVals) { ... }

    public void setData(LineData data) { ... }

    public void setData(BarData data) { ... }

    public void setData(ScatterData data) { ... }

    public void setData(CandleData data) { ... }

    // ...
}
```
