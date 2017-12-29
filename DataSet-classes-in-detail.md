This wiki entry focuses on the subclasses of the `DataSet` class. 
All other subclasses of `DataSet` not mentioned here do not provide any specific enhancements.

**Line-, Bar-, Scatter-, Bubble- & CandleDataSet** (below mentioned methods can be used for any of the mentioned `DataSet` classes)
 - <code>setHighLightColor(int color)</code>: Sets the color that is used for drawing the highlight indicators. Don't forget to resolve the color using `getResources().getColor(...)` or `Color.rgb(...)` (or simply `Color.BLACK`).

**Line-, Bar-, Scatter-, Candle- & RadarDataSet**
 - <code>setDrawHighlightIndicators(boolean enabled)</code>: Enables / disables both vertical and horizontal highlight indicator lines. Call `setDrawVerticalHighlightIndicator(...)` and `setDrawHorizontalHighlightIndicator(...)` for individual configuration.
 - <code>setHighlightLineWidth(float width)</code>: Sets the width of the highlight lines (crosshairs) in dp.

**Line- & RadarDataSet** (methods only for `LineDataSet` and `RadarDataSet`)
 - <code>setFillColor(int color)</code>: Sets the color that is used for filling the line surface.
 - <code>setFillAlpha(int alpha)</code>: Sets the alpha value (transparency) that is used for filling the line surface (0-255), default: 85, 255 = fully opaque, 0 = fully transparent
 - <code>setFillDrawable(Drawable d)</code>: Sets a `Drawable` that should cover the fill-area. This also allows to use gradients.
 - <code>setDrawFilled(boolean filled)</code>: Set to true if the DataSet should be drawn filled (surface, area), and not just as a line, disabling this will give a performance boost. Please note that this method uses the `canvas.clipPath(...)` method for drawing the filled area. For devices with API level < 18 (Android 4.3), hardware acceleration of the chart should be turned off - see [here](http://stackoverflow.com/a/30354461/1590502). Default: false
 - <code>setLineWidth(float width)</code>: Set the line width for this DataSet (min = 0.2f, max = 10f); default 1f NOTE: thinner line == better performance, thicker line == worse performance

Below mentioned methods are only applicable for the specifically mentioned `DataSet` subclass.

**LineDataSet** (class `LineDataSet`)
 - <code>setCircleRadius(float size)</code>: Sets the size (radius) of the circle shaped value indicators, default size = 4f
 - <code>setDrawCircles(boolean enabled)</code>: Set this to true to enable the drawing of circle indicators for this `LineDataSet`, default true
 - <code>setDrawCubic(boolean enabled)</code>: If set to true, the linechart lines are drawn in cubic-style instead of linear. This has a **negative effect on performance**! Default: false
 - <code>setCubicIntensity(float intensity)</code>: Sets the intensity for cubic lines (if enabled). Max = 1f = very cubic, Min = 0.05f = low cubic effect, Default: 0.2f
 - <code>setCircleColor(int color)</code>: Sets the color all circle indicators of this dataset should have.
 - <code>setCircleColors(List<Integer> colors)</code>: Sets the colors the outer-circles of this `LineDataSet` should have. There are various other methods for setting circle colors as well.
 - <code>setCircleColorHole(int color)</code>: Sets the color of the inner circle of the line-circles (the hole).
 - <code>setDrawCircleHole(boolean enabled)</code>: Set this to true to allow drawing a hole in each circle of this dataset. If set to false, circles will be drawn filled (without hole).
 - <code>enableDashedLine(float lineLength, float spaceLength, float phase)</code>: Enables the line to be drawn in dashed mode, e.g. like this "- - - - - -". "lineLength" is the length of the line pieces, "spaceLength" is the length of space in between the pieces, "phase" is the offset, in degrees (normally, use 0)

**BarDataSet** (class `BarDataSet`)
 - <code>setBarSpacePercent(float percent)</code>: Sets the space between the bars in percent of the total bar width.
 - <code>setBarShadowColor(int color)</code>: Sets the color used for drawing the bar-shadows. The bar shadows is a surface behind the bar that indicates the maximum value. Don't for get to use `getResources().getColor(...)` to set this. Or `Color.rgb(...)`.
 - <code>setHighLightAlpha(int alpha)</code>: Set the alpha value (transparency) that is used for drawing the highlight indicator bar. min = 0 (fully transparent), max = 255 (fully opaque).
 - <code>setStackLabels(String[] labels)</code>: Sets labels for different values of bar-stacks, in case there are one.

**ScatterDataSet** (class `ScatterDataSet`)
 - <code>setScatterShapeSize(float size)</code>: Sets the size in density pixels the drawn scattershape will have. This only applies for non custom shapes.
 - <code>setScatterShape(ScatterShape shape)</code>: Sets the shape that is drawn on the position where the values are at.

**CandleDataSet** (class `CandleDataSet`)
 - <code>setBodySpace(float space)</code>: Sets the space that is left out on the left and right side of each candle body, default 0.1f (10%), max 0.45f, min 0f
 - <code>setShadowWidth(float width)</code>: Sets the width of the candle-shadow-line in dp. Default 3f.
 - <code>setShadowColor(int color)</code>: Sets the color of the candle-shadow-line.
 - <code>setDecreasingColor(int color)</code>: Sets the one and ONLY color that should be used for this `DataSet` when open > close. 
 - <code>setIncreasingColor(int color)</code>: Sets the one and ONLY color that should be used for this DataSet when  open <= close. 
 - <code>setDecreasingPaintStyle(Paint.Style style)</code>: Sets paint style when open > close (fill or stroke).
 - <code>setIncreasingPaintStyle(Paint.Style style)</code>: Sets paint style when open <= close (fill or stroke).

**BubbleDataSet** (class `BubbleDataSet`)
 - <code>setHighlightCircleWidth(float width)</code>: Sets the width of the circle that surrounds the bubble when in highlighted state, in dp.

Information concerning `CandleDataSet` colors: The usual `setColors(...)`, `setColor(...)`, ... methods can still be used for coloring the chart all at once. If specific colors (for body, shadow, ...) are needed, use the above mentioned methods.

**PieDataSet** (class `PieDataSet`)
 - <code>setSliceSpace(float degrees)</code>: Sets the space that is left out between the piechart-slices in dp, default: 0 --> no space, maximum 20, minimum 0 (no space)
 - <code>setSelectionShift(float shift)</code>: Sets the distance the highlighted piechart-slice of this DataSet is "shifted" away from the center of the chart, default 12f