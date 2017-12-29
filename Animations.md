Note: **ANIMATIONS ONLY WORK FOR API LEVEL 11 (Android 3.0.x) AND HIGHER**.

On lower Android versions, animations will not be executed (but will not crash).

All chart types support animations that can be used to create / build up the chart in an awesome looking way. Three different kinds of animation methods exist that animate either both, or x- and y-axis separately:

 - `animateX(int durationMillis)`: Animates the charts values on the horizontal axis, meaning that the chart will build up within the specified time from left to right.
 - `animateY(int durationMillis)`: Animates the charts values on the vertical axis, meaning that the chart will build up within the specified time from bottom to top.
 - `animateXY(int xDuration, int yDuration)`: Animates both horizontal and vertical axis, resulting in a left/right bottom/top build-up.

```java
mChart.animateX(3000); // animate horizontal 3000 milliseconds
// or:
mChart.animateY(3000); // animate vertical 3000 milliseconds
// or:
mChart.animateXY(3000, 3000); // animate horizontal and vertical 3000 milliseconds
```

If `animate(...)` (of any kind) is called, no further calling of `invalidate()` is necessary to refresh the chart.


**Animation easing**

This library allows you to apply nice easing functions to your animations. You can choose between the following static **predefined** `Easing.EasingOption`:

```java
  public enum EasingOption {
      Linear,
      EaseInQuad,
      EaseOutQuad,
      EaseInOutQuad,
      EaseInCubic,
      EaseOutCubic,
      EaseInOutCubic,
      EaseInQuart,
      EaseOutQuart,
      EaseInOutQuart,
      EaseInSine,
      EaseOutSine,
      EaseInOutSine,
      EaseInExpo,
      EaseOutExpo,
      EaseInOutExpo,
      EaseInCirc,
      EaseOutCirc,
      EaseInOutCirc,
      EaseInElastic,
      EaseOutElastic,
      EaseInOutElastic,
      EaseInBack,
      EaseOutBack,
      EaseInOutBack,
      EaseInBounce,
      EaseOutBounce,
      EaseInOutBounce,
  }
```

Basically, there are two ways of easing your animation: 

**1. Predefined easing options**: (this code will run on any Android version)
 ```java
 public void animateY(int durationmillis, Easing.EasingOption option); 
 ```

 Call any animation method with a predefined easing option:
 ```java
 // animate both axes with easing
 mChart.animateY(3000, Easing.EasingOption.EaseOutBack); 
 ```
 **Always use** `Easing.EasingOption` for predefined animation easing when you want your code to run below Android 3.0 (API level 11).

**2. Custom easing functions**: (custom easing functions will crash below Android 3.0)
 ```java
 public void animateY(int durationmillis, EasingFunction function); 
 ```

 **Create your own** easing functions by creating your own easing-function class and implementing the `EasingFunction` interface:

 ```java
 /**
  * Interface for creating custom made easing functions. 
  */
  public interface EasingFunction {
     /**
      * Called everytime the animation is updated.
      * @param input - the time passed since the animation started (value between 0 and 1)
      */
      public float getInterpolation(float input);
  }
 ```

 Then call it this way (be aware, this will not run below Android 3.0 and crash):
 ```java
 // animate both axes with easing
 mChart.animateY(3000, new MyEasingFunction()); 
 ```