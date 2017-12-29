Since [v2.2.0](https://github.com/PhilJay/MPAndroidChart/releases), MPAndroidChart allows you to easily create your own custom `DataSet` objects and use them in the charts.

**What you need to do**
- Create your own custom class (e.g. `CustomDataSet`)
- Let it `extend` `BaseDataSet<? extends Entry>`
- Let it implement the `IDataSet` interface of your choice (e.g. `IBarDataSet`) - depending on the kind of chart you want to create
- Implement all (by you) required methods and let them return your values of choice

**Example**

Creating a custom `BarDataSet` to be used in a `BarChart`.

````java
public class CustomBarDataSet extends BaseDataSet<BarEntry> implements IBarDataSet {
    // implement all by the extended class and interface required methods
}
````

After creating the `CustomBarDataSet` and implementing all methods required by the interface it can be used in any `BarChart` just like a normal `BarDataSet`.