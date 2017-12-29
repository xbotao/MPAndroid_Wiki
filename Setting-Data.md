
This chapter covers the topic of setting data to various kinds of `Charts`.

# LineChart

If you want to add values (data) to the chart, it has to be done via the 

```java
    public void setData(ChartData data) { ... }
```
method. The baseclass <code>ChartData</code> ([ChartData](https://github.com/PhilJay/MPAndroidChart/wiki/The-ChartData-class)) class encapsulates all data and information that is needed for the chart during rendering. For each type of chart, a different subclass of `ChartData` (e.g. `LineData`) exists that should be used for setting data for the chart. In the constructor, you can hand over an <code>List<? extends IDataSet></code> as the values to display. Below is an example with the class `LineData` (extends `ChartData`), which is used for adding data to a `LineChart`:

```java
    /** List constructor */
    public LineData(List<ILineDataSet> sets) { ... }

    /** Constructor with one or multiple ILineDataSet objects */
    public LineData(ILineDataSet...) { ... }
```

So, what is a <code>DataSet</code> and why do you need it? That is actually pretty simple. One <code>DataSet</code> object represents a group of entries (e.g. class <code>Entry</code>) inside the chart that belong together. It is designed to **logically separate different groups of values in the chart**. For each type of chart, a differnt object that extends `DataSet` (e.g. `LineDataSet`) exists that allows specific styling. 

As an example, you might want to display **the quarterly revenue of two different companies** over one year in a `LineChart`. In that case, it would be recommended to create two different <code>LineDataSet</code> objects, each containing four values (one for each quarter). 

Of course, it is also possible to provide just one <code>LineDataSet</code> object containing all 8 values for the two companys. 

So how to setup a <code>LineDataSet</code> object?
```java
    public LineDataSet(List<Entry> entries, String label) { ... }
```

When looking at the constructor (different constructors are available), it is visible that the <code>LineDataSet</code> needs an <code>List</code> of type <code>Entry</code> and a `String` used to describe the `LineDataSet` and as a label used for the `Legend`. Furthermore this label can be used to find the `LineDataSet` amongst other `LineDataSet` objects in the `LineData` object.

The <code>List</code> of type <code>Entry</code> encapsulates all values of the chart. A <code>Entry</code> object is an additional wrapper around an entry in the chart with a x- and y-value:
```java
    public Entry(float x, float y) { ... }
```

Putting it all together (example of two companies with quarterly revenue over one year):

At first, create the lists of type <code>Entry</code> that will hold your values:

```java
    List<Entry> valsComp1 = new ArrayList<Entry>();
    List<Entry> valsComp2 = new ArrayList<Entry>();
```
Then, fill the lists with <code>Entry</code> objects. Make sure the entry objects contain the correct indices to the x-axis. (of course, a loop can be used here, in that case, the counter variable of the loop could be the index on the x-axis).

```java
    Entry c1e1 = new Entry(0f, 100000f); // 0 == quarter 1
    valsComp1.add(c1e1);
    Entry c1e2 = new Entry(1f, 140000f); // 1 == quarter 2 ...
    valsComp1.add(c1e2);
    // and so on ...
    
    Entry c2e1 = new Entry(0f, 130000f); // 0 == quarter 1
    valsComp2.add(c2e1);
    Entry c2e2 = new Entry(1f, 115000f); // 1 == quarter 2 ...
    valsComp2.add(c2e2);
    //...
```

Now that we have our lists of <code>Entry</code> objects, the <code>LineDataSet</code> objects can be created:
```java
    LineDataSet setComp1 = new LineDataSet(valsComp1, "Company 1");
    setComp1.setAxisDependency(AxisDependency.LEFT);
    LineDataSet setComp2 = new LineDataSet(valsComp2, "Company 2");
    setComp2.setAxisDependency(AxisDependency.LEFT);
```
By calling `setAxisDependency(...)`, the axis the `DataSet` should be plotted against is specified.
Last but not least, we create a list of <code>IDataSets</code> and build our <code>ChartData</code> object:

```java

    // use the interface ILineDataSet
    List<ILineDataSet> dataSets = new ArrayList<ILineDataSet>();
    dataSets.add(setComp1);
    dataSets.add(setComp2);
    
    LineData data = new LineData(dataSets);
    mLineChart.setData(data);
    mLineChart.invalidate(); // refresh
```

After calling `invalidate()` the chart is **refreshed** and the provided data is drawn.

If we want to add more descriptive values to the x-axis (instead of numbers ranging from 0 to 3 for the different quarters), we can do so by using the `IAxisValueFormatter` interface. This interface allows custom styling of values drawn on the `XAxis`. In this example, the formatter could look like this:

```java

// the labels that should be drawn on the XAxis
final String[] quarters = new String[] { "Q1", "Q2", "Q3", "Q4" };

IAxisValueFormatter formatter = new IAxisValueFormatter() {

    @Override
    public String getFormattedValue(float value, AxisBase axis) {
        return quarters[(int) value];
    }

    // we don't draw numbers, so no decimal digits needed
    @Override
    public int getDecimalDigits() {  return 0; }
};

XAxis xAxis = mLineChart.getXAxis();
xAxis.setGranularity(1f); // minimum axis-step (interval) is 1
xAxis.setValueFormatter(formatter);
```

Detailed information concerning the `IAxisValueFormatter` interface can be found [here](https://github.com/PhilJay/MPAndroidChart/wiki/The-AxisValueFormatter-interface).

If additional styling is applied, the `LineChart` resulting from this example should look similar to the one below:

<img src="https://raw.github.com/PhilJay/MPChart/master/screenshots/linechart_wiki.png" width="700">

Setting data for normal `BarChart`, `ScatterChart`, `BubbleChart` and `CandleStickChart` works similar to the `LineChart`. A special case is the `BarChart` with multiple (grouped) bars, which will be explained below.

### The order of entries

Please be aware that this library **does not officially support** drawing `LineChart` data from an `Entry` list not sorted by the x-position of the entries in ascending manner. Adding entries in an unsorted way may result in correct drawing, but may also lead to unexpected behaviour. A `List` of `Entry` objects can be sorted manually or using the `EntryXComparator`:

```java
List<Entry> entries = ...;
Collections.sort(entries, new EntryXComparator());
```
The reason why this is required is because the library uses [binary search algorithms](https://en.wikipedia.org/wiki/Binary_search_algorithm) for better performance only working on sorted lists.

# BarChart

The way data can be set for a `BarChart` is very similar to the `LineChart`. The major difference are the data objects that need to be used for setting the data (e.g. `BarEntry` instead of `Entry`). In addition to that, the `BarChart` has different styling options. 

Consider the following example of filling a `BarChart` with data:

```java

List<BarEntry> entries = new ArrayList<>();
entries.add(new BarEntry(0f, 30f));
entries.add(new BarEntry(1f, 80f));
entries.add(new BarEntry(2f, 60f));
entries.add(new BarEntry(3f, 50f)); 
                                    // gap of 2f
entries.add(new BarEntry(5f, 70f));
entries.add(new BarEntry(6f, 60f));

BarDataSet set = new BarDataSet(entries, "BarDataSet");
```

In the above example, five `BarEntry` objects were created and added to a `BarDataSet`. Notice that there is a gap of "2" on the x-position between the fourth and fifth entry. In this example, this gap is used to explain how the positioning of bars in the `BarChart` works. The screenshot in the end of this tutorial will show the resulting `BarChart` for the given data. As a next step, a `BarData` object needs to be created:

```java

BarData data = new BarData(set);
data.setBarWidth(0.9f); // set custom bar width
chart.setData(data);
chart.setFitBars(true); // make the x-axis fit exactly all bars
chart.invalidate(); // refresh
```

In the above snippet, a `BarData` object was created. When the `BarEntry` objects for the chart were created, we left a space of "1f" on the x-axis between (the centres) of each bar. By setting the bar-width to 0.9f, we effectively create a space of 0.1f between each bar. The `setFitBars(true)` call will tell the chart to adjust it's range of x-axis values to exactly fit all bars, and no bars are cut off on the sides.

After creating the `BarData` object, we set it to the chart and refresh. The result should look close to the one shown below:

<img src="https://raw.github.com/PhilJay/MPChart/master/screenshots/normal_barchart_wiki.png" width="700">

# Grouped BarChart

Since release [v3.0.0](https://github.com/PhilJay/MPAndroidChart/releases), MPAndroidChart supports drawing bars explicitly grouped (in this case the library will handle the x-position), or user defined, which means that the user can place the bars anywhere he wants by altering the x-position of the bar.

This section will focus on explicit grouped `BarChart`, which means that the library will handle the x-positions of the bars. Consider the following example setup:

```java

YourData[] group1 = ...;
YourData[] group2 = ...;

List<BarEntry> entriesGroup1 = new ArrayList<>();
List<BarEntry> entriesGroup2 = new ArrayList<>();

// fill the lists
for(int i = 0; i < group1.length; i++) {
    entriesGroup1.add(new BarEntry(i, group1.getValue()));
    entriesGroup2.add(new BarEntry(i, group2.getValue()));
}

BarDataSet set1 = new BarDataSet(entriesGroup1, "Group 1");
BarDataSet set2 = new BarDataSet(entriesGroup2, "Group 2");
```

In this example case, we will have two groups of bars, each represented by an individual `BarDataSet`. In case of explicit (library handled) groups, the actual x-position of the entries does not matter. Grouping is performed based on the position of the `BarEntry` in the entries `List`.

```java

float groupSpace = 0.06f;
float barSpace = 0.02f; // x2 dataset
float barWidth = 0.45f; // x2 dataset
// (0.02 + 0.45) * 2 + 0.06 = 1.00 -> interval per "group"

BarData data = new BarData(set1, set2);
data.setBarWidth(barWidth); // set the width of each bar
barChart.setData(data);
barChart.groupBars(1980f, groupSpace, barSpace); // perform the "explicit" grouping
barChart.invalidate(); // refresh
```

In the code snippet above, the `BarDataSet` objects are added to a `BarChart`. The `groupBars(...)` method performs the grouping of the two `BarDataSet` objects. The method takes the following parameters:

```java
public void groupBars(float fromX, float groupSpace, float barSpace) { ... }
```

The `fromX` parameter determines where on the `XAxis` the grouped bars should start (in this case "1980"), the `groupSpace` determines the space left in between each group of bars, and the `barSpace` determines the space between individual bars of a group. Based on these parameters, the `groupBars(...)` method alters the position of each bar on the `XAxis` towards a grouped appearance, preserving the order of the individual `BarEntry` objects.

The "interval" (occupied space) each group has on the `XAxis` is also defined by the `groupSpace` and `barSpace` parameters, and the `barWidth`.

The result should look somewhat like this:

<img src="https://raw.github.com/PhilJay/MPChart/master/screenshots/grouped_barchart_wiki.png" width="700">

Of course a grouped `BarChart` can also be achieved without the use of the `groupBars(...)` method, by simply positioning the individual bars correctly on the `XAxis` manually.

In order to make sure the labels of the `XAxis` are centered above the groups like in the screenshot above, you can use the `setCenterAxisLabels(...)` method:

```java
XAxis xAxis = chart.getXAxis();
xAxis.setCenterAxisLabels(true);
```

# Stacked BarChart

The stacked `BarChart` setup is completely similar to normal `BarChart`, with the exception being the way the individual `BarEntry` objects are created. In case of stacked bars, a different constructor for the `BarEntry` has to be used:

```java
public BarEntry(float x, float [] yValues) { ... }
```

This constructor allows to provide multiple `yValues`, which represent the values of the "stack" of each bar. Consider the following example object:

```java
BarEntry stackedEntry = new BarEntry(0f, new float[] { 10, 20, 30 });
```

This `BarEntry` has consists of a stack of three values, having a "height" of "10", "20" and "30". 

# PieChart

Unlike other chart types, the `PieChart` takes data in form of `PieEntry` objects. The constructor for these objects looks as follows:

```java
public PieEntry(float value, String label) { ... }
```

The first parameter of the constructor is used for the actual "value" that should be drawn as a pie-slice in the `PieChart`. The second `String` parameter called "label" is used to provide additional description of the slice. Consider the following example `PieChart` setup:

```java

List<PieEntry> entries = new ArrayList<>();

entries.add(new PieEntry(18.5f, "Green"));
entries.add(new PieEntry(26.7f, "Yellow"));
entries.add(new PieEntry(24.0f, "Red"));
entries.add(new PieEntry(30.8f, "Blue"));

PieDataSet set = new PieDataSet(entries, "Election Results");
PieData data = new PieData(set);
pieChart.setData(data);
pieChart.invalidate(); // refresh
```

The `PieEntry` objects to not hold a value for the x-position because the order of the `PieEntry` objects displayed in the chart is determined by their order in the `entries` list.

When adding some additional styling, the resulting `PieChart` with the data used above could look similar to this:

<img src="https://raw.github.com/PhilJay/MPChart/master/screenshots/piechart_wiki.png" width="350">

# RadarChart

# CombinedChart