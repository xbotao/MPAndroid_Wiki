The `FillFormatter` interface **allows to customize** where the filled line of a `LineDataSet` should end. All that needs to be done is create a new class and implement the `FillFormatter` interface. Use the

```java
public float getFillLinePosition(LineDataSet dataSet, LineDataProvider provider)
```
method of the interface for implementing a custom logic that calculates the ending point of the fill line for the individual `LineDataSet`.

Creating a class the implements the interface:

```java
public class MyCustomFillFormatter implements FillFormatter {

    @Override
    public float getFillLinePosition(LineDataSet dataSet, LineDataProvider dataProvider) {

        float myDesiredFillPosition = ...;
        // put your logic here...

        return myDesiredFillPosition;
    }
}
```

And then set the custom-formatter to your `LineDataSet`:

```java
lineDataSet.setFillFormatter(new MyCustomFillFormatter());
```

Here is the default implementation (logic) of the [DefaultFillFormatter](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/com/github/mikephil/charting/formatter/DefaultFillFormatter.java).