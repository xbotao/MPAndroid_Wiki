The `ViewPortHandler` class is responsible for handling the view-port of the chart. This means it's responsible for what is visible in the chart-view, it's current state in terms of translation and zoom / scale level, the size of the chart and it's drawing area and current offsets. The `ViewPortHandler` allows to directly access all the above mentioned properties and modify them.

Unlike modifying the view-port via the `Chart` class, as described [here](https://github.com/PhilJay/MPAndroidChart/wiki/Modifying-the-Viewport), modifying the `ViewPortHandler` directly is not always a completely safe way of changing what is visible and should be performed with care by a person familiar with the API. Incorrect use can lead to unexpected behaviour. However, the `ViewPortHandler` offers more advanced methods of view-port modification.

**Getting an instance**

An instance of the `ViewPortHandler` can be acquired the following way only:

```java
ViewPortHandler handler = chart.getViewPortHandler();
```

**Scale & Translation**

 - `getScaleX()`: Returns the current scale / zoom level on the x-axis.
 - `getScaleY()`: Returns the current scale / zoom level on the y-axis.
 - `getTransX()`: Returns the current translation (movement) on the x-axis.
 - `getTransY()`: Returns the current translation (movement) on the y-axis.

**Chart dimensions & content**

 - `getChartWidth()`: Returns the width of the chart.
 - `getChartHeight()`: Returns the height of the chart.
 - `getContentRect()`: Returns the current content area as a `RectF` object.

More methods can be found in the [JavaDocs](https://github.com/PhilJay/MPAndroidChart/wiki#javadoc) or via studying the API.