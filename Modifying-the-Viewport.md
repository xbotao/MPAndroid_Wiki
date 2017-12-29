This library has various methods for modifying the viewport (what is visible on the chart, aim of the view). Please note that these methods are **only available** for the `LineChart`, `BarChart`, `ScatterChart` and `CandleStickChart`.

The methods mentioned below are provided by the `Chart` class. Another way to modify the viewport is to directly access it (without the in-between safety provided by the chart) via the [ViewPortHandler](https://github.com/PhilJay/MPAndroidChart/wiki/The-ViewPortHandler). This is only recommended for advanced users who are familiar with the API.

> Please note that **all methods modifying the viewport** need to be called on the `Chart` **after setting data**.

### Restraining what's visible
 - <code>setVisibleXRangeMaximum(float maxXRange)</code>: Sets the size of the area (range on the x-axis) that should be maximum visible at once. If this is e.g. set to 10, no more than 10 values on the x-axis can be viewed at once without scrolling.
 - <code>setVisibleXRangeMinimum(float minXRange)</code>: Sets the size of the area (range on the x-axis) that should be minimum visible at once. If this is e.g. set to 10, it is not possible to zoom in further than 10 values on the x-axis.
 - <code>setVisibleYRangeMaximum(float maxYRange, AxisDependency axis)</code>: Sets the size of the area (range on the y-axis) that should be maximum visible at once. You also need to provide the axis this constraint should apply to.
 - <code>setViewPortOffsets(float left, float top, float right, float bottom)</code>: Sets custom offsets for the current ViewPort (the offsets on the sides of the actual chart window). Setting this will prevent the chart from automatically calculating it's offsets. Use `resetViewPortOffsets()` to undo this. USE THIS ONLY WHEN YOU KNOW WHAT YOU ARE DOING.
 - <code>resetViewPortOffsets()</code>: Resets all custom offsets set via `setViewPortOffsets(...)` method. Allows the chart to again calculate all offsets automatically.
 - <code>setExtraOffsets(float left, float top, float right, float bottom)</code>: Sets extra offsets (around the chart view) to be appended to the auto-calculated offsets. This does not change the auto-calculated offsets, but adds extra space to them.

**Moving the view** (where it is aimed)
 - <code>fitScreen()</code>: Resets all zooming and dragging and makes the chart fit exactly it's bounds (fully zoom out).
 - <code>moveViewToX(float xValue)</code>: Moves the left side (edge) of the current viewport to the specified x-value.
 - <code>moveViewToY(float yValue, AxisDependency axis)</code>: Centers the viewport to the specified y-value on the provided y-axis (left or right).
 - <code>moveViewTo(float xValue, float yValue, AxisDependency axis)</code>: This will move the left side of the current viewport to the specified x-value on the x-axis, and center the viewport to the specified y-value on the provided y-axis (makes sense in combination with `setVisibleXRange(...)` and `setVisibleYRange(...)`.
 - <code>centerViewTo(float xValue, float yValue, AxisDependency axis)</code>: This will move the center of the current viewport to the specified x-value and y-value (makes sense in combination with `setVisibleXRange(...)` and `setVisibleYRange(...)`.

### Moving the view with animations
(since release [v2.2.3](https://github.com/PhilJay/MPAndroidChart/releases))

- <code>moveViewToAnimated(float xValue, float yValue, AxisDependency axis, long duration)</code>: This will move the left side of the current viewport to the specified x-value on the x-axis, and center the viewport to the specified y-value on the provided y-axis in an animated way.
- <code>centerViewToAnimated(float xValue, float yValue, AxisDependency axis, long duration)</code>: This will move the center of the current viewport to the specified x-value and y-value (according to axis) in an animated way.

_Note_: All `moveViewTo(...)` methods will **automatically** `invalidate()` (refresh) the chart. There is no need for further calling `invalidate()`.
 
**Zooming** (programmatically)
- <code>zoomIn()</code>: Zooms in by 1.4f, into the charts center.
- <code>zoomOut()</code>: Zooms out by 0.7f, from the charts center.
- <code>zoom(float scaleX, float scaleY, float x, float y)</code>: Zooms in or out by the given scale factor. x and y are the coordinates (in pixels) of the zoom center. Remember that a scale of 1f = no zoom.
- <code>zoom(float scaleX, float scaleY, float xValue, float yValue, AxisDependency axis)</code>: Zooms in or out by the given scale factor. xValue and yValue are the actual data values (not pixels) of the zoom center. Remember that a scale of 1f = no zoom.

### Zooming with animations
(since release [v2.2.3](https://github.com/PhilJay/MPAndroidChart/releases))

- <code>zoomAndCenterAnimated(float scaleX, float scaleY, float xValue, float yValue, AxisDependency axis, long duration)</code>: Zooms by the specified scale factor and centers the viewport to the specified values on the specified axis in an animated way.

### Full example
```java
chart.setData(...); // first set data

// now modify viewport
chart.setVisibleXRangeMaximum(20); // allow 20 values to be displayed at once on the x-axis, not more
chart.moveViewToX(10); // set the left edge of the chart to x-index 10
// moveViewToX(...) also calls invalidate()
```