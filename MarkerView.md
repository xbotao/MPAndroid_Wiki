The `abstract` `MakerView` class can be extended by any user-created class in order to display a customized (popup) `View` whenever a value is highlighted in the chart. The baseclass `MarkerView` extends `RelativeLayout`.

```java

// extend MarkerView
public class YourCustomMarkerView extends MarkerView { ...
```

###Setting / getting the marker
 - <code>setMarkerView(MarkerView mv)</code>: Sets a `MarkerView` for the chart that will be displayed where values are selected.
 - <code>getMarkerView()</code>: Returns the `MarkerView` that has been set for the chart, or null.


###Creating a MarkerView

Below you can find an example of what a custom-implementation of the `MarkerView` could look like. Important is that you implement the following methods inherited from the abstract `MarkerView` class:
 - <code>refreshContent(Entry e, Highlight highlight)</code>: This method gets called everytime the `MarkerView` is redrawn, and gives you the chance to update the content it displays (e.g. set the text for a `TextView`, ...). It provides the currently highlighted `Entry` and corresponding `Highlight` object for further information.
 - <code>getXOffset(float xpos)</code>: Here, you should return the offset to the position on the x-axis where the marker is drawn. By default, the marker will be drawn with it's top left edge at the position of the entry. The `xpos` parameter represents the default drawing position of the marker.
 - <code>getYOffset(float ypos)</code>: Here, you should return the offset to the position on the y-axis where the marker is drawn. By default, the marker will be drawn with it's top left edge at the position of the entry. The `ypos` parameter represents the default drawing position of the marker.

```java
public class CustomMarkerView extends MarkerView {

    private TextView tvContent;

    public CustomMarkerView (Context context, int layoutResource) {
        super(context, layoutResource);
        // this markerview only displays a textview
        tvContent = (TextView) findViewById(R.id.tvContent);
    }

    // callbacks everytime the MarkerView is redrawn, can be used to update the
    // content (user-interface)
    @Override
    public void refreshContent(Entry e, Highlight highlight) {
        tvContent.setText("" + e.getVal()); // set the entry-value as the display text
    }

    @Override
    public int getXOffset(float xpos) {
        // this will center the marker-view horizontally
        return -(getWidth() / 2);
    }

    @Override
    public int getYOffset(float ypos) {
        // this will cause the marker-view to be above the selected value
        return -getHeight();
    }
}
```
After setting up the custom marker class, create a layout in .xml that will represent your marker. The layout in this example only consists of a `RelativeLayout` with a background image containing a `TextView`. Of course, **you can create any layout you want** here.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="wrap_content"
    android:layout_height="40dp"
    android:background="@drawable/markerImage" >

    <TextView
        android:id="@+id/tvContent"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:text=""
        android:textSize="12dp"
        android:textColor="@android:color/white"
        android:ellipsize="end"
        android:singleLine="true"
        android:textAppearance="?android:attr/textAppearanceSmall" />

</RelativeLayout>

```

Finally, after you have created your own `MarkerView`, set it to the chart. When creating your `MarkerView`, make sure that you provide the layout resource that you created in .xml.

```java
CustomMarkerView mv = new CustomMarkerView(Context, R.layout.custom_marker_view_layout);

// set the marker to the chart
chart.setMarkerView(mv);
```