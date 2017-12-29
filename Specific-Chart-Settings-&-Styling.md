In chapter [1. Getting Started](https://github.com/PhilJay/MPAndroidChart/wiki/Getting-Started) general chart settings and styling methods applicable for all chart types were mentioned. This chapter focuses on specific settings for the individual chart types.

**Line-, Bar-, Scatter-, Candle- & BubbleChart**

 - <code>setAutoScaleMinMaxEnabled(boolean enabled)</code>: Flag that indicates if auto scaling on the y axis is enabled. If enabled the y axis automatically adjusts to the min and max y values of the current x axis range whenever the viewport changes. This is especially interesting for charts displaying financial data. Default: false
 - <code>setKeepPositionOnRotation(boolean enabled)</code>: Sets wether the chart should keep its position (zoom / scroll) after orientation change. Default: false

**BarChart**
 - <code>setDrawValueAboveBar(boolean enabled)</code>: If set to true, all values are drawn above their bars, instead of below their top.
 - <code>setDrawBarShadow(boolean enabled)</code>: If set to true, a grey area is drawn behind each bar that indicates the maximum value. Enabling his will reduce performance by about 40%.
 - <code>setDrawValuesForWholeStack(boolean enabled)</code>: If set to true, all values of stacked bars are drawn individually, and not just their sum on top of all.
 - <code>setDrawHighlightArrow(boolean enabled)</code>: Set this to true to draw the highlightning arrow above each bar when highlighted.

**PieChart**
 - <code>setDrawSliceText(boolean enabled)</code>: Set this to true to draw the x-value text into the pie slices.
 - <code>setUsePercentValues(boolean enabled)</code>: If this is enabled, values inside the chart are drawn in percent and not with their original value. Values provided for the `ValueFormatter` to format are then provided in percent.
 - <code>setCenterText(SpannableString text)</code>: Sets the text that is drawn in the center of the PieChart. Longer text will be automatically "wrapped" to avoid clipping into the pie-slices.
 - <code>setCenterTextRadiusPercent(float percent)</code>: Sets the rectangular radius of the bounding box for the center text, as a percentage of the pie hole default 1.f (100%).
 - <code>setHoleRadius(float percent)</code>: Sets the radius of the hole in the center of the piechart in percent of the maximum radius (max = the radius of the whole chart), default 50%
 - <code>setTransparentCircleRadius(float percent)</code>: Sets the radius of the transparent circle that is drawn next to the hole in the piechart in percent of the maximum radius (max = the radius of the whole chart), default 55% -> means 5% larger than the center-hole by default
 - <code>setTransparentCircleColor(int color)</code>: Sets the color of the transparent circle.
 - <code>setTransparentCircleAlpha(int alpha)</code>: Sets the amount of transparency (0-255) the transparent circle should have.
 - <code>setMaxAngle(float maxangle)</code>: Sets the max angle that is used for calculating the pie-circle. 360f means it's a full `PieChart`, 180f results in a half-pie-chart. Default: 360f

**RadarChart**

 - <code>setSkipWebLineCount(int count)</code>: Allows to skip web lines coming from the center of the chart. Especially useful if there are a lot of lines.