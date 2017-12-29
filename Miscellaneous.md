**Chart content**
 - <code>clear()</code>: Clears the chart of all data (by setting the data object to null). Calls `invalidate()` to refresh the chart.
 - <code>clearValues()</code>: Clears the chart of all DataSet objects and thereby all Entries. **Does not** remove the provided x-values from the chart. Calls `invalidate()` to refresh the chart.
 - <code>isEmpty()</code>: Will return true if the charts data object is null, or if it contains no entries.

**Useful getter methods**
 - <code>getData()</code>: Will return the data object you set for the chart.
 - <code>getViewPortHandler()</code>: Will return `ViewPortHandler` object of the chart that contains information about the charts size and bounds (offsets, content-area), as well as about the charts current scale (zoom) and translation (scrolling) state.
 - <code>getRenderer()</code>: Returns the main `DataRenderer` that is responsible for drawing the chart data.
 - <code>getCenter()</code>: Returns the center point of the whole chart-view.
 - <code>getCenterOffsets()</code>: Returns the center point of the chart drawing-area.
 - <code>getPercentOfTotal(float value)</code>: Returns the percentage the provided value makes up of the total value-sum inside the chart.
 - <code>getYMin()</code>: Returns lowest value the chart holds.
 - <code>getYMax()</code>: Returns biggest value the chart holds.
 - <code>getLowestVisibleXIndex()</code>: Returns the lowest x-index (value on the x-axis) that is still visible on the chart.
 - <code>getHighestVisibleXIndex()</code>: Returns the highest x-index (value on the x-axis) that is still visible on the chart.

**Some more methods** (of the `Chart` class)

 - <code>saveToGallery(String title)</code>: Saves the current chart state as an image to the gallery. **Don't forget to add "WRITE_EXTERNAL_STORAGE" permission to your manifest**.
 - <code>saveToPath(String title, String pathOnSD)</code>: Saves the current chart state as an image to the specified path. **Don't forget to add "WRITE_EXTERNAL_STORAGE" permission to your manifest**.
 - <code>getChartBitmap()</code>: Returns the `Bitmap` object that represents the chart, this `Bitmap` always contains the latest drawing state of the chart.
 - <code>setHardwareAccelerationEnabled(boolean enabled)</code>: Allows to enable/disable hardware acceleration for the chart, only API level 11+.