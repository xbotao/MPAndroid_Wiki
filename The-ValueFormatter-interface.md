Available since [v1.6.2](https://github.com/PhilJay/MPAndroidChart/releases) - changed (improved) in [v2.1.4](https://github.com/PhilJay/MPAndroidChart/releases)

The `IValueFormatter` interface can be used to create custom-made formatter classes that allow to format values within the chart (from `DataSets`) in a specific way before drawing them.

For using the `IValueFormatter`, simply create a new class and let it implement the interface and return whatever you want to be displayed from the `getFormattedValue(...)` method.

### Creating a Formatter
```java
public class MyValueFormatter implements IValueFormatter {

    private DecimalFormat mFormat;
    
    public MyValueFormatter() {
        mFormat = new DecimalFormat("###,###,##0.0"); // use one decimal
    }
    
    @Override
    public String getFormattedValue(float value, Entry entry, int dataSetIndex, ViewPortHandler viewPortHandler) {
        // write your logic here
        return mFormat.format(value) + " $"; // e.g. append a dollar-sign
    }
}
```

Then, set your formatter to the `ChartData` or `DataSet` object:

```java

// usage on whole data object
lineData.setValueFormatter(new MyValueFormatter());

// usage on individual dataset object
lineDataSet.setValueFormatter(new MyValueFormatter());

```

### Predefined Formatters

 - [LargeValueFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/main/java/com/github/mikephil/charting/formatter/LargeValueFormatter.java): Can be used for formatting large values > "1.000". It will turn values like "1.000" into "1k", "1.000.000" will be "1m" (million), "1.000.000.000" will be "1b" (billion) and values like one trillion will be e.g. "1t".
 - [PercentFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/main/java/com/github/mikephil/charting/formatter/PercentFormatter.java): Used for displaying a "%" sign after each value with 1 decimal digit. Especially useful for the `PieChart`. 50 -> 50.0 %
 - [StackedValueFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/main/java/com/github/mikephil/charting/formatter/StackedValueFormatter.java): A formatter specifically designed to be used with stacked `BarChart`. It allows to specify whether all stack values should be drawn or just the top value.