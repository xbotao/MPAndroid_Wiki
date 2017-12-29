Since release [v1.4.0](https://github.com/PhilJay/MPAndroidChart/releases/tag/v1.4.0), the `ColorTemplate` object that was responsible for setting colors in previous releases is no longer needed. Nevertheless, it still holds all predefined color arrays (e.g. `ColorTemplate.VORDIPLOM_COLORS` and provides convenience methods for transforming colors from the resources (resource integers) into "real" colors.

Instead of the `ColorTemplate`, colors can now be specified directly via `DataSet` object, which allows **separate styling** for each `DataSet`.

In this short example, we have our two different `LineDataSet` objects representing the quarterly revenues of two companies (previously mentioned in the [Setting Data](https://github.com/PhilJay/MPAndroidChart/wiki/Setting-Data) tutorial), for which we now want to set different colors.

What we want:

 - the values of "Company 1" should be represented by four different variations of the color "red"
 - the values of "Company 2" should be represented by four different variations of the color "green"

This is what the code looks like:

```java
  LineDataSet setComp1 = new LineDataSet(valsComp1, "Company 1");
  // sets colors for the dataset, resolution of the resource name to a "real" color is done internally
  setComp1.setColors(new int[] { R.color.red1, R.color.red2, R.color.red3, R.color.red4 }, Context);
  
  LineDataSet setComp2 = new LineDataSet(valsComp2, "Company 2");
  setComp2.setColors(new int[] { R.color.green1, R.color.green2, R.color.green3, R.color.green4 }, Context);
```

Besides that, there are many other ways for setting colors for a `DataSet`. Here is the full documentation:

 - `setColors(int [] colors, Context c)`: Sets the colors that should be used fore this DataSet. Colors are reused as soon as the number of Entries the DataSet represents is higher than the size of the colors array. You can use "new int[] { R.color.red, R.color.green, ... }" to provide colors for this method. Internally, the colors are resolved using **getResources().getColor(...)**.
 - `setColors(int [] colors)`: Sets the colors that should be used fore this DataSet. Colors are reused as soon as the number of Entries the DataSet represents is higher than the size of the colors array. Make sure that the colors are already prepared (by calling **getResources().getColor(...)**) before adding them to the DataSet.
 - `setColors(ArrayList<Integer> colors)`: Sets the colors that should be used fore this DataSet. Colors are reused as soon as the number of Entries the DataSet represents is higher than the size of the colors array. Make sure that the colors are already prepared (by calling getResources().getColor(...)) before adding them to the DataSet.
 - `setColor(int color)`: Sets the one and ONLY color that should be used for this DataSet. Internally, this recreates the colors array and adds the specified color.

`ColorTemplate` example:

```java
LineDataSet set = new LineDataSet(...);
set.setColors(ColorTemplate.VORDIPLOM_COLORS);
```

If no colors are set for a `DataSet`, default colors are used.
