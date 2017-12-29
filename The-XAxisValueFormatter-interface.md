Available since [v2.1.4](https://github.com/PhilJay/MPAndroidChart/releases)

The `XAxisValueFormatter` interface can be used to create custom-made formatter classes that allow to **dynamically adjust x-values** before drawing them to the screen.

For using the `XValueFormatter`, simply create a new class and let it implement the interface and return whatever you want to be displayed as a `XAxis` label from the `getXValue(...)` method.

**Example of a custom formatter**
```java
public class MyCustomXAxisValueFormatter implements XAxisValueFormatter {
    
    @Override
    public String getXValue(String original, int index, ViewPortHandler viewPortHandler) {
        // original is the original value to use, x-index is the index in your x-values array
        // implement your logic here ...
        return ...;
    }
}
```

Then, set your formatter to the `XAxis`:

```java
// usage on XAxis, get axis instance:
XAxis xAxis = chart.getXAxis();

// set the formatter
xAxis.setValueFormatter(new MyCustomXAxisValueFormatter());
```

**Predefined XAxisValueFormatters**
 - [DefaultXAxisValueFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/com/github/mikephil/charting/formatter/DefaultXAxisValueFormatter.java)

**Example XAxisValueFormatters**
 - [MyCustomXValueFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartExample/src/com/xxmassdeveloper/mpchartexample/custom/MyCustomXAxisValueFormatter.java)
