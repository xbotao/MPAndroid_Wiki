The `YAxis` is a subclass of [AxisBase](https://github.com/PhilJay/MPAndroidChart/wiki/The-Axis). This wiki entry only describes the `YAxis`, not it's superclass.

The `YAxis` class (in versions older than 2.0.0 `YLabels` called), is the data and **information container for everything related with the vertical-axis**. Each Line-, Bar-, Scatter or CandleStickChart has a left and a right `YAxis` object, responsible for either the left, or the right axis respectively. The RadarChart has only one `YAxis`. By default, both axes of the chart are enabled and will be drawn.

In order to **acquire an instance** of the `YAxis` class, call one of the following methods:
```java
YAxis leftAxis = chart.getAxisLeft();
YAxis rightAxis = chart.getAxisRight();

YAxis leftAxis = chart.getAxis(AxisDependency.LEFT);

YAxis yAxis = radarChart.getYAxis(); // this method radarchart only
```

At runtime, use ```public AxisDependency getAxisDependency()``` to determine the side of the chart this axis represents.

Customizations that affect the value range of the axis **need to be applied before setting data** for the chart.

### Axis Dependency

Per default, all data that is added to the chart plots against the left `YAxis` of the chart. If not further specified and enabled, the right `YAxis` is adjusted to represent the same scale as the left axis.

If your chart needs to support different axis scales, you can achieve that by setting the axis your data should plot against. This can be done by changing the `AxisDependency` of your `DataSet` object:

```java
LineDataSet dataSet = ...; // get a dataset
dataSet.setAxisDependency(AxisDependency.RIGHT);
```

Setting this will change the axis your data is plotted against.

### The zero line

Besides the grid-lines, that originate horizontally alongside each value on the `YAxis`, there is the so called zeroline, which is drawn at the zero (0) value on the axis, and is similar to the grid-lines but can be configured separately. 

 - <code>setDrawZeroLine(boolean enabled)</code>: Enables / disables drawing the zero-line.
 - <code>setZeroLineWidth(float width)</code>: Sets the line-width of the zero line.
 - <code>setZeroLineColor(int color)</code>: Sets the color the zero-line should have.

Zero-line example code:
````java
// data has AxisDependency.LEFT
YAxis left = mChart.getAxisLeft();
left.setDrawLabels(false); // no axis labels
left.setDrawAxisLine(false); // no axis line
left.setDrawGridLines(false); // no grid lines
left.setDrawZeroLine(true); // draw a zero line
mChart.getAxisRight().setEnabled(false); // no right axis
````

The above code will result in a zero-line like shown in the image below. No axis values are drawn, no grid lines or axis lines are drawn, just a zero line.

<img src="https://raw.github.com/PhilJay/MPChart/master/screenshots/zero_line_example_barchart.png" width="600">

### More example code
```java
YAxis yAxis = mChart.getAxisLeft();
yAxis.setTypeface(...); // set a different font
yAxis.setTextSize(12f); // set the text size
yAxis.setAxisMinimum(0f); // start at zero
yAxis.setAxisMaximum(100f); // the axis maximum is 100
yAxis.setTextColor(Color.BLACK);
yAxis.setValueFormatter(new MyValueFormatter());
yAxis.setGranularity(1f); // interval 1
yAxis.setLabelCount(6, true); // force 6 labels
//... and more

```