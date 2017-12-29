# First Chapter

This chapter covers the basic setup for using this library.

### \#\#\# Add dependency

As a first step, add a dependency to this library to your project. How to do that is described in the \[usage\]\([https://github.com/PhilJay/MPAndroidChart\#usage\](https://github.com/PhilJay/MPAndroidChart#usage\)\) section of this repository. \_Gradle\_ is the recommended way of using this library as a dependency.

\#\#\# Creating the View

For using a &lt;code&gt;LineChart, BarChart, ScatterChart, CandleStickChart, PieChart, BubbleChart or RadarChart &lt;/code&gt;, define it in .xml:

\`\`\`xml

```
&lt;com.github.mikephil.charting.charts.LineChart

    android:id="@+id/chart"

    android:layout\_width="match\_parent"

    android:layout\_height="match\_parent" /&gt;
```

\`\`\`

And then retrieve it from your \`Activity\`, \`Fragment\` or whatever:

\`\`\`java

```
// in this example, a LineChart is initialized from xml

LineChart chart = \(LineChart\) findViewById\(R.id.chart\);
```

\`\`\`

or create it in code \(and then \*\*add it to a layout\*\*\):

\`\`\`java

```
// programmatically create a LineChart

LineChart chart = new LineChart\(Context\);



// get a layout defined in xml

RelativeLayout rl = \(RelativeLayout\) findViewById\(R.id.relativeLayout\);

rl.add\(chart\); // add the programmatically created chart
```

\`\`\`

\#\#\# Adding data

After you have an instance of your chart, you can create data and add it to the chart. This example uses the \`LineChart\`, for which the \`Entry\` class represents a single entry in the chart with x- and y-coordinate. Other chart types, such as \`BarChart\` use other classes \(e.g. \`BarEntry\`\) for that purpose.

To add data to your chart, wrap each data object you have into an \`Entry\` object, like below:

\`\`\`java

YourData\[\] dataObjects = ...;

List&lt;Entry&gt; entries = new ArrayList&lt;Entry&gt;\(\);

for \(YourData data : dataObjects\) {

```
// turn your data into Entry objects

entries.add\(new Entry\(data.getValueX\(\), data.getValueY\(\)\)\); 
```

}

\`\`\`

As a next step, you need to add the \`List&lt;Entry&gt;\` you created to a \`LineDataSet\` object. \`DataSet\` objects hold data which belongs together, and allow individual styling of that data. The below used "Label" has only a descriptive purpose and shows up in the \`Legend\`, if enabled.

\`\`\`java

LineDataSet dataSet = new LineDataSet\(entries, "Label"\); // add entries to dataset

dataSet.setColor\(...\);

dataSet.setValueTextColor\(...\); // styling, ...

\`\`\`

As a last step, you need to add the \`LineDataSet\` object \(or objects\) you created to a \`LineData\` object. This object holds all data that is represented by a \`Chart\` instance and allows further styling. After creating the data object, you can set it to the chart and refresh it:

\`\`\`java

LineData lineData = new LineData\(dataSet\);

chart.setData\(lineData\);

chart.invalidate\(\); // refresh

\`\`\`

Please consider the scenario above a very basic setup. For a \*\*more detailed explanation\*\* please refer to the \[setting data\]\([https://github.com/PhilJay/MPAndroidChart/wiki/Setting-Data\](https://github.com/PhilJay/MPAndroidChart/wiki/Setting-Data\)\) section, which explains how to add data to various \`Chart\` types based on examples.

\#\#\# Styling

For information about settings & styling of the chart surface and data, visit the \[general settings & styling\]\([https://github.com/PhilJay/MPAndroidChart/wiki/General-Chart-Settings-&-Styling\](https://github.com/PhilJay/MPAndroidChart/wiki/General-Chart-Settings-&-Styling\)\) section. Regarding more specific styling & settings for individual chart types, please have a look at the \[specific settings & styling\]\([https://github.com/PhilJay/MPAndroidChart/wiki/Specific-chart-settings\](https://github.com/PhilJay/MPAndroidChart/wiki/Specific-chart-settings\)\) wiki page.

