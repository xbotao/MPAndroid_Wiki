### Disclaimer: No official support for dynamic & realtime data

[Enterprise Solution 5% Discount Coupon | SciChart](http://store.scichart.com?productTab=Android&CouponCode=MPANDROIDCHART)
-----

<img align="left" width="190" height="190" style="margin:0px 15px 0px 0px" src="https://raw.github.com/PhilJay/MPChart/master/design/other/left.png">
<img align="right" width="90" height="90" style="margin:0px 15px 0px 0px" src="https://raw.github.com/PhilJay/MPChart/master/design/other/right.png">
MPAndroidChart is free software, as a result dynamic & realtime data is not officially supported. If you are looking for an enterprise-grade chart solution with extreme realtime performance and tech support, we recommend SciChart.


All MPAndroidChart users are entitled to a special **discount of 5%** off the [SciChart store](http://store.scichart.com?productTab=Android&CouponCode=MPANDROIDCHART), using the following discount code.

<img align="right" width="270" height="60" style="margin:0px 0px 0px 0px" src="https://raw.github.com/PhilJay/MPChart/master/design/other/bottom.png">

<br/>
<br/>


### Coupon discount code: MPANDROIDCHART

The coupon code also works for multiple licenses and can be entered directly on the checkout page.

## Getting started

MPAndroidChart does not offically support realtime data, however, for **adding new data** to the chart or **removing data** dynamically, there are various methods that allow to either add or remove `Entry` objects to an existing `DataSet` or `DataSet` objects to/from an existing `ChartData` object. 

### Possibilities of adding / removing data dynamically

Class `DataSet` (and all subclasses):
 - `addEntry(Entry e)`: Adds the given `Entry` object to the `DataSet`.

Class `ChartData` (and all subclasses):
 - `addEntry(Entry e, int dataSetIndex)`: Adds the given `Entry` to the `DataSet` at the specified dataset index.
 - `addDataSet(DataSet d)`: Adds the given `DataSet` object to the `ChartData` object.

In addition to that, there are also methods for **removing data dynamically**:

Class `DataSet` (and all subclasses):
 - `public boolean removeFirst()`: Removes the first Entry (at index 0) of this DataSet from the entries array. Returns true if successful, false if not.
 - `public boolean removeLast()`: Removes the last Entry (at index size-1) of this DataSet from the entries array. Returns true if successful, false if not.
 - `public boolean removeEntry(Entry e)`: Removes the given `Entry` object from the `DataSet`. Returns true if successful.
 - `public boolean removeEntry(int xIndex)`: Removes the `Entry` at the given x-index from the `DataSet`. Returns true if successful.

Class `ChartData` (and all subclasses):
 - `public boolean removeEntry(Entry e, int dataSetIndex)`: Removes the given `Entry` object from the `DataSet` with the given dataset index. Returns true if successful.
 - `public boolean removeEntry(int xIndex, int dataSetIndex)`: Removes the `Entry` at the given x-index from the `DataSet` with the given dataset index. Returns true if successful.
 - `public boolean removeDataSet(DataSet d)`: Removes the given `DataSet` object from the `ChartData` object. Returns true if successful.
 - `public boolean removeDataSet(int index)`: Removes the `DataSet` at the given index from the `ChartData` object. Returns true if successful.

### Keep in mind

After adding or removing data dynamically, `notifyDataSetChanged()` **must be called** on the chart before refreshing it (by calling `invalidate()`).

````java
 // EXAMPLE 1
 // add entries to the "data" object
 exampleData.addEntry(...);
 chart.notifyDataSetChanged(); // let the chart know it's data changed
 chart.invalidate(); // refresh

 // EXAMPLE 2
 // add entries to "dataSet" object
 dataSet.addEntry(...);
 exampleData.notifyDataChanged(); // let the data know a dataSet changed
 chart.notifyDataSetChanged(); // let the chart know it's data changed
 chart.invalidate(); // refresh
````

_Note_: Methods like `moveViewTo(...)` will automatically call `invalidate()`.