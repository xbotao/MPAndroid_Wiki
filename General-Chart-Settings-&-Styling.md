This section focuses on settings and styling of this library applicable for all `Chart` types.

**Refreshing**
- <code>invalidate()</code>: Calling this method on the chart will **refresh** (redraw) it. This is needed in order to make changes performed on the chart take effect.
- <code>notifyDataSetChanged()</code>: Lets the chart know it's underlying data has changed and performs all necessary recalculations (offsets, legend, maxima, minima, ...). This is needed especially when [adding data dynamically](https://github.com/PhilJay/MPAndroidChart/wiki/Dynamic-&-Realtime-Data).

**Logging**
- <code>setLogEnabled(boolean enabled)</code>: Setting this to true will activate chart logcat output. Enabling this is bad for performance, keep disabled if not necessary.

**General Chart Styling**

Here are some general styling methods you can directly use on the chart:

 - <code>setBackgroundColor(int color)</code>: Sets the background color that will cover the whole chart-view. In addition, a background-color can be set via `.xml` in the layout file.
 - <code>setDescription(String desc)</code>: Set a description text that appears in the bottom right corner of the chart.
 - <code>setDescriptionColor(int color)</code>: Sets the color of the description text.
 - <code>setDescriptionPosition(float x, float y)</code>: Sets a custom position for the description text in pixels on the screen.
 - <code>setDescriptionTypeface(Typeface t)</code>: Sets the <code>Typeface</code> used for drawing the description text.
 - <code>setDescriptionTextSize(float size)</code>: Sets the size of the description text in pixels, min 6f, max 16f.
 - <code>setNoDataText(String text)</code>: Sets the text that should appear if the chart is empty.
 - <code>setDrawGridBackground(boolean enabled)</code>: If enabled, the background rectangle behind the chart drawing-area will be drawn.
 - <code>setGridBackgroundColor(int color)</code>: Sets the color the grid-background should be drawn with.
 - <code>setDrawBorders(boolean enabled)</code>: Enables / disables drawing the chart borders (lines surrounding the chart).
 - <code>setBorderColor(int color)</code>: Sets the color of the chart border lines.
 - <code>setBorderWidth(float width)</code>: Sets the width of the chart border lines in dp.
 - <code>setMaxVisibleValueCount(int count)</code>: Sets the number of maximum visible drawn value-labels on the chart. This only takes affect when `setDrawValues()` is enabled.