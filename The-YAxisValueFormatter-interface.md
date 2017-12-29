Available since [v2.1.4](https://github.com/PhilJay/MPAndroidChart/releases)

The `YAxisValueFormatter` interface can be used to create custom-made formatter classes that allow to format the labels of the `YAxis` in a specific way before drawing them.

For using the `YAxisValueFormatter`, simply create a new class and let it implement the interface and return whatever you want to be displayed from the `getFormattedValue(...)` method.

**Example of a custom formatter**
```java
public class MyYAxisValueFormatter implements YAxisValueFormatter {

    private DecimalFormat mFormat;
    
    public MyYAxisValueFormatter () {
        mFormat = new DecimalFormat("###,###,##0.0"); // use one decimal
    }
    
    @Override
    public String getFormattedValue(float value, YAxis yAxis) {
        // write your logic here
        // access the YAxis object to get more information
        return mFormat.format(value) + " $"; // e.g. append a dollar-sign
    }
}
```

Then, set your formatter to the `YAxis` object:

```java
// get an instance of the YAxis (e.g. left axis)
YAxis leftAxis = chart.getAxisLeft();
leftAxis.setValueFormatter(new MyYAxisValueFormatter());
```

**Predefined custom formatters**

 - [LargeValueFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/com/github/mikephil/charting/formatter/LargeValueFormatter.java): Can be used for formatting large values > "1.000". It will turn values like "1.000" into "1k", "1.000.000" will be "1m" (million), "1.000.000.000" will be "1b" (billion) and values like one trillion will be e.g. "1t". It does not support numbers with decimal digits like "1.000,5".
 - [PercentFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/com/github/mikephil/charting/formatter/PercentFormatter.java): Used for displaying a "%" sign after each value with 1 decimal digit. Especially useful for the `PieChart`. 50 -> 50.0 %