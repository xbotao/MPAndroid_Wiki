The `XAxis` is a subclass of [AxisBase](https://github.com/PhilJay/MPAndroidChart/wiki/The-Axis) from which it inherits a number of styling and convenience methods.

The `XAxis` class (in versions prior to 2.0.0 `XLabels` called), is the **data and information container for everything related to the the horizontal axis**. Each Line-, Bar-, Scatter-, CandleStick- and RadarChart has an `XAxis` object.

The `XAxis` class allows specific styling and consists (can consist) of the following components/parts:
 - A so called "axis-line" that is drawn directly next to and parallel to the labels
 - The "grid-lines", each originating from an axis-label in vertical direction

In order to **acquire an instance** of the `XAxis` class, do the following:
```java
XAxis xAxis = chart.getXAxis();
```

### Customizing the axis values
 - <code>setLabelRotationAngle(float angle)</code>: Sets the angle for drawing the x-axis labels (in degrees).
 - <code>setPosition(XAxisPosition pos)</code>: Sets the position where the `XAxis` should appear. Choose between TOP, BOTTOM, BOTH_SIDED, TOP_INSIDE or BOTTOM_INSIDE.

### Example Code
```java
XAxis xAxis = chart.getXAxis();
xAxis.setPosition(XAxisPosition.BOTTOM);
xAxis.setTextSize(10f);
xAxis.setTextColor(Color.RED);
xAxis.setDrawAxisLine(true);
xAxis.setDrawGridLines(false);
// set a custom value formatter
xAxis.setValueFormatter(new MyCustomFormatter()); 
// and more...

```