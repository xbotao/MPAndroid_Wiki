This section focuses on the topic of highlighting entries in the chart, both via tap-gesture and programmatically based on release [v3.0.0](https://github.com/PhilJay/MPAndroidChart/releases).

### Enabling / Disabling highlighting

 - <code>setHighlightPerDragEnabled(boolean enabled)</code>: Set this to true on your `Chart` to allow highlighting per dragging over the chart surface when it is fully zoomed out. Default: true
 - <code>setHighlightPerTapEnabled(boolean enabled)</code>: Set this to false on your `Chart` to prevent values from being highlighted by tap gesture. Values can still be highlighted via drag or programmatically. Default: true
 - <code>setMaxHighlightDistance(float distanceDp)</code>: Sets the maximum highlight distance in dp. Taps on the chart further away from an entry than that distance will not trigger a highlight. Default: 500dp

In addition to that, highlighting can be configured for individual `DataSet` objects:

```java
  dataSet.setHighlightEnabled(true); // allow highlighting for DataSet

  // set this to false to disable the drawing of highlight indicator (lines)
  dataSet.setDrawHighlightIndicators(true); 
  dataSet.setHighlightColor(Color.BLACK); // color for highlight indicator
  // and more...
```

### Highlighting programmatically

 - <code>highlightValue(float x, int dataSetIndex, boolean callListener)</code>: Highlights the value at the given x-position in the given DataSet. Provide -1 as the dataSetIndex to undo all highlighting. The boolean flag determines wether the selection listener should be called or not.
 - <code>highlightValue(Highlight high, boolean callListener)</code>: Highlights the value represented by the provided `Highlight` object. Provide null to undo all highlighting. The boolean flag determines wether the selection listener should be called or not.
 - <code>highlightValues(Highlight[] highs)</code>: Highlights the values represented by the given `Highlight[]` array. Provide null or an empty array to undo all highlighting.
 - <code>getHighlighted()</code>: Returns an `Highlight[]` array that contains information about all highlighted entries, their x-index and dataset-index.

### Selection callbacks

This library provides a number of listeners for callbacks upon interaction. One of them is the `OnChartValueSelectedListener`, for callbacks when highlighting values via touch:

```java
public interface OnChartValueSelectedListener {
    /**
    * Called when a value has been selected inside the chart.
    *
    * @param e The selected Entry.
    * @param h The corresponding highlight object that contains information
    * about the highlighted position
    */
    public void onValueSelected(Entry e, Highlight h);
    /**
    * Called when nothing has been selected or an "un-select" has been made.
    */
    public void onNothingSelected();
}
```

Simply let your class that should receive the callbacks implement this interface and set it as a listener to the chart:
```java
chart.setOnChartValueSelectedListener(this);
```

### The Highlight class

The `Highlight` class represents all data associated with a highlighted `Entry`, such as the highlighted `Entry` object itself, the `DataSet` it belongs to, it's position on the drawing surface and more. It can be used to get information about an already highlighted `Entry`, or used to provide information to the `Chart` for an `Entry` to be highlighted. Regarding that purpose, the `Highlight` class provides two constructors:

```java 

 /** constructor for standard highlight */
 public Highlight(float x, int dataSetIndex) { ... }

 /** constructor for stacked BarEntry highlight */
 public Highlight(float x, int dataSetIndex, int stackIndex) { ... }

```

These constructors can be used to create a `Highlight` object which allows to perform highlighting programmatically:

```java

// highlight the entry and x-position 50 in the first (0) DataSet
Highlight highlight = new Highlight(50f, 0); 

chart.highlightValue(highlight, false); // highlight this value, don't call listener
```

### Custom highlighter

All user input in the form of highlight gestures is internally processed by the default `ChartHighlighter` class. It is possible to replace the default highligher with a custom implementation using the below method:
 - <code>setHighlighter(ChartHighlighter highlighter)</code>: Sets a custom highligher object for the chart that handles / processes all highlight touch events performed on the chart-view. Your custom highlighter object needs to extend the `ChartHighlighter` class.