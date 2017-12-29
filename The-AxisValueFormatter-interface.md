Introduced in release [v3.0.0](https://github.com/PhilJay/MPAndroidChart/releases), this interface allows the custom styling of both `XAxis` and `YAxis` values before drawing.

### Creating a Formatter

All that needs to be done to custom-format values on the axis is to create a class that implements the `IAxisValueFormatter` interface, as shown below. This formatter is used to format the values of an axis to 1 decimal digit always.

```java
public class MyYAxisValueFormatter implements IAxisValueFormatter {

    private DecimalFormat mFormat;

    public MyAxisValueFormatter() {

        // format values to 1 decimal digit
        mFormat = new DecimalFormat("###,###,##0.0");
    }

    @Override
    public String getFormattedValue(float value, AxisBase axis) {
        // "value" represents the position of the label on the axis (x or y)
        return mFormat.format(value) + " $";
    }
    
    /** this is only needed if numbers are returned, else return 0 */
    @Override
    public int getDecimalDigits() { return 1; }
}
```

The example below shows how to plot values from a `String[]` array to the axis:

```java
public class MyXAxisValueFormatter implements IAxisValueFormatter {

    private String[] mValues;

    public MyXAxisValueFormatter(String[] values) {
        this.mValues = values;
    }

    @Override
    public String getFormattedValue(float value, AxisBase axis) {
        // "value" represents the position of the label on the axis (x or y)
        return mValues[(int) value];
    }
    
    /** this is only needed if numbers are returned, else return 0 */
    @Override
    public int getDecimalDigits() { return 0; }
}
```

### Setting the Formatter

After the creation of the formatter, simply set it to your axis of choice:

```java

YAxis left = chart.getAxisLeft();
left.setValueFormatter(new MyYAxisValueFormatter());

String[] values = new String[] { ... };

XAxis xAxis = chart.getXAxis();
xAxis.setValueFormatter(new MyXAxisValueFormatter(values));
```

Instead of the default values ranging from axis minimum value to axis maximum value, the axis will now plot the data specified by the formatter.

### Restricting Intervals

In case you are using a formatter based on array indices (like above), it makes sense to restrict the minimum interval of your axis to "1":

```java
axis.setGranularity(1f); // restrict interval to 1 (minimum)
```

This will prevent the formatter from drawing duplicate axis labels (caused by axis intervals < 1). As soon as the "zoom level" of the chart is high enough, it will stop recalculating smaller intervals.

### Predefined Formatters

 - [LargeValueFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/main/java/com/github/mikephil/charting/formatter/LargeValueFormatter.java): Can be used for formatting large values > "1.000". It will turn values like "1.000" into "1k", "1.000.000" will be "1m" (million), "1.000.000.000" will be "1b" (billion) and values like one trillion will be e.g. "1t".
 - [PercentFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/main/java/com/github/mikephil/charting/formatter/PercentFormatter.java): Used for displaying a "%" sign after each value with 1 decimal digit. Especially useful for the `PieChart`. 50 -> 50.0 %

### Example Formatters

 - [DayAxisValueFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartExample/src/com/xxmassdeveloper/mpchartexample/custom/DayAxisValueFormatter.java): This formatter converts the provided value to plot into a date `String`, altering the string depending on scale.

### Legacy Formatters

Prior to release v3.0.0, there were separate formatters for `XAxis` and `YAxis`. The documentation for these formatters can be found here:

 - [XAxisValueFormatter](https://github.com/PhilJay/MPAndroidChart/wiki/The-XAxisValueFormatter-interface)
 - [YAxisValueFormatter](https://github.com/PhilJay/MPAndroidChart/wiki/The-YAxisValueFormatter-interface)