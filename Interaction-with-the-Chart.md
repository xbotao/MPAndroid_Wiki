This library allows you to fully customize the possible touch (and gesture) interaction with the chart-view and react to the interaction via callback-methods.

### Enabling / disabling interaction
 - <code>setTouchEnabled(boolean enabled)</code>: Allows to enable/disable all possible touch-interactions with the chart.
 - <code>setDragEnabled(boolean enabled)</code>: Enables/disables dragging (panning) for the chart.
 - <code>setScaleEnabled(boolean enabled)</code>: Enables/disables scaling for the chart on both axes.
 - <code>setScaleXEnabled(boolean enabled)</code>:  Enables/disables scaling on the x-axis.
 - <code>setScaleYEnabled(boolean enabled)</code>:  Enables/disables scaling on the y-axis.
 - <code>setPinchZoom(boolean enabled)</code>: If set to true, pinch-zooming is enabled. If disabled, x- and y-axis can be zoomed separately.
 - <code>setDoubleTapToZoomEnabled(boolean enabled)</code>: Set this to false to disallow zooming the chart via double-tap on it.

### Chart fling / deceleration
 - <code>setDragDecelerationEnabled(boolean enabled)</code>: If set to true, chart continues to scroll after touch up. Default: true.
 - <code>setDragDecelerationFrictionCoef(float coef)</code>: Deceleration friction coefficient in [0 ; 1] interval, higher values indicate that speed will decrease slowly, for example if it set to 0, it will stop immediately. 1 is an invalid value, and will be converted to 0.9999 automatically.

### Highlighting Values

How to allow highlighting entries via tap-gesture and programmatically is described int the [highlightning section](https://github.com/PhilJay/MPAndroidChart/wiki/Highlighting).

### Gesture callbacks

The `OnChartGestureListener` will allow you to react to gestures made on the chart:
```java
public interface OnChartGestureListener {

    /**
     * Callbacks when a touch-gesture has started on the chart (ACTION_DOWN)
     *
     * @param me
     * @param lastPerformedGesture
     */
    void onChartGestureStart(MotionEvent me, ChartTouchListener.ChartGesture lastPerformedGesture);

    /**
     * Callbacks when a touch-gesture has ended on the chart (ACTION_UP, ACTION_CANCEL)
     *
     * @param me
     * @param lastPerformedGesture
     */
    void onChartGestureEnd(MotionEvent me, ChartTouchListener.ChartGesture lastPerformedGesture);

    /**
     * Callbacks when the chart is longpressed.
     * 
     * @param me
     */
    public void onChartLongPressed(MotionEvent me);

    /**
     * Callbacks when the chart is double-tapped.
     * 
     * @param me
     */
    public void onChartDoubleTapped(MotionEvent me);

    /**
     * Callbacks when the chart is single-tapped.
     * 
     * @param me
     */
    public void onChartSingleTapped(MotionEvent me);

    /**
     * Callbacks then a fling gesture is made on the chart.
     * 
     * @param me1
     * @param me2
     * @param velocityX
     * @param velocityY
     */
    public void onChartFling(MotionEvent me1, MotionEvent me2, float velocityX, float velocityY);

   /**
     * Callbacks when the chart is scaled / zoomed via pinch zoom gesture.
     * 
     * @param me
     * @param scaleX scalefactor on the x-axis
     * @param scaleY scalefactor on the y-axis
     */
    public void onChartScale(MotionEvent me, float scaleX, float scaleY);

   /**
    * Callbacks when the chart is moved / translated via drag gesture.
    *
    * @param me
    * @param dX translation distance on the x-axis
    * @param dY translation distance on the y-axis
    */
    public void onChartTranslate(MotionEvent me, float dX, float dY);
}
```

Simply let your class that should receive the callbacks implement this interface and set it as a listener to the chart:
```java
chart.setOnChartGestureListener(this);
```