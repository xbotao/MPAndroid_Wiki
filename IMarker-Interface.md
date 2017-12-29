
Since release [v3.0.0](https://github.com/PhilJay/MPAndroidChart/releases), markers (popup views) in the chart are represented by the `IMarker` interface.

### IMarker interface

This interface allows you to create custom marker views displayed at highlighted entries in your chart. The methods provided by the interface look as follows:

```java
public interface IMarker {

    /**
     * @return The desired (general) offset you wish the IMarker to have on the x- and y-axis.
     *         By returning x: -(width / 2) you will center the IMarker horizontally.
     *         By returning y: -(height / 2) you will center the IMarker vertically.
     */
    MPPointF getOffset();

    /**
     * @return The offset for drawing at the specific `point`. This allows conditional adjusting of the Marker position.
     *         If you have no adjustments to make, return getOffset().
     *
     * @param posX This is the X position at which the marker wants to be drawn.
     *             You can adjust the offset conditionally based on this argument.
     * @param posY This is the X position at which the marker wants to be drawn.
     *             You can adjust the offset conditionally based on this argument.
     */
    MPPointF getOffsetForDrawingAtPos(float posX, float posY);

    /**
     * This method enables a specified custom IMarker to update it's content every time the IMarker is redrawn.
     *
     * @param e         The Entry the IMarker belongs to. This can also be any subclass of Entry, like BarEntry or
     *                  CandleEntry, simply cast it at runtime.
     * @param highlight The highlight object contains information about the highlighted value such as it's dataset-index, the
     *                  selected range or stack-index (only stacked bar entries).
     */
    void refreshContent(Entry e, Highlight highlight);

    /**
     * Draws the IMarker on the given position on the screen with the given Canvas object.
     *
     * @param canvas
     * @param posX
     * @param posY
     */
    void draw(Canvas canvas, float posX, float posY);
}
```

### Creating a MarkerView

In order to create your custom marker view, you need to create a new class that implements the `IMarker` interface:

```java
public class YourMarkerView implements IMarker { ... }
```
What you return from the methods provided by the interface depends on your personal requirements. Have a look at the above shown documentation of the methods for better understanding.

I addition to implementing the `IMarker` interface, you can create your own class and extend it by one of the predefined markers mentioned below. This approach is easier and does not require to implement all methods provided by the `IMarker` interface. Only particular methods can be overridden and customised. The most important thing is then to override the `refreshContent(...)` method to adjust the data drawn by the marker. A simple example could look like this:

```java
public class YourMarkerView extends MarkerView {

    private TextView tvContent;

    public MyMarkerView(Context context, int layoutResource) {
        super(context, layoutResource);

        // find your layout components
        tvContent = (TextView) findViewById(R.id.tvContent);
    }

    // callbacks everytime the MarkerView is redrawn, can be used to update the
    // content (user-interface)
    @Override
    public void refreshContent(Entry e, Highlight highlight) {

        tvContent.setText("" + e.getY());

        // this will perform necessary layouting
        super.refreshContent(e, highlight);
    }

    private MPPointF mOffset; 

    @Override
    public MPPointF getOffset() {

        if(mOffset == null) {
           // center the marker horizontally and vertically
           mOffset = new MPPointF(-(getWidth() / 2), -getHeight());
        }

        return mOffset;
    }
}
```

### Getting / Setting the Marker

In order to set your marker to the chart, use the `setMarker(...)` method:

```java

IMarker marker = new YourMarkerView();
chart.setMarker(marker);
```

To access an existing marker set to the chart, use the `getMarker()` method:

```java
IMarker marker = chart.getMarker();
```

### Predefined Markers

Besides creating your own custom marker view, this library provides a few predefined markers for easier and faster use. Those markers include:

 - [MarkerView](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/main/java/com/github/mikephil/charting/components/MarkerView.java): The basic marker. Allows to provide a layout resource that is rendered on the chart surface representing the marker. Extend this class and override the `refreshContent(...)` method for adjusting marker data.
 - [MarkerImage](https://github.com/PhilJay/MPAndroidChart/blob/master/MPChartLib/src/main/java/com/github/mikephil/charting/components/MarkerImage.java): A marker for drawing images. Allows to provide a drawable resource that is rendered on the chart surface representing the marker. Extend this class and override the `refreshContent(...)` method for adjusting marker data.

### Legacy MarkerView

In versions prior to [v3.0.0](https://github.com/PhilJay/MPAndroidChart/releases), the `MarkerView` class was responsible for drawing markers at highlighted positions in the chart. For detailed information regarding this class, please visit the old [MarkerView wiki page](https://github.com/PhilJay/MPAndroidChart/wiki/MarkerView).