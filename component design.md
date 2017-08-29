# Design of Chart Components

## General Design

The Chart Components uses the MPAndroidChart library for implementation. Users code will be processed by my methods, and then invoke the corresponding library methods. In this project, I designed three kinds of charts: Line Chart, Pie Chart and Bar Chart.  I created three sepreate components for that. The reason of creating separate components is clear: Data of pie chart is one-dimensional, but line chart and bar chart require data of two-dimensional. Besides that, the styling of different kinds of charts are also different, so I choose to create separate component for each kind of chart. 

The design of chart components mainly consists of two parts: 
- Setting data
- Styling

**Setting data** is the central part of the plot design. In pie chart data are one-dimensional while in bar chart and line chart, data are two-dimensional. One chart includes several data sets, and one data set includes several data entries. One entry is a bar in bar chart or a point in line chart.

In pie chart, the method is easy because data is only one-dimensional. Data can be easily added or removed with methods ```AddEntry``` or ```RemoveEntry``` explained below.

However in line chart or bar chart, data can be grouped into several data sets. In line chart, one data set is a polygonal line, which can be represented with a list of (x,y) points. One restriction is that x values in the list must be incremental, since Z-shaped lines are not supported by the library. X values don't have to be continuous. So I designed two methods of adding data. One is ```AddDataSet```, it requires a string label and then create a empty data set with it. The other is ```AddEntry```, it requires the data set label string, x value and y value. A new point will be added and a line will connect the new point and the previous point in the same data set.

In bar chart, problem is a little bit more complicated. Users often want to have multiple bars in the same x value in order to show their difference. But the reality is that their x value are not equal (otherwise they will coincide). Users shouldn't be required to calculate the offsets and set their different x values. The library offers a method ```groupBars``` which can automatically modify the position of bars. However, after grouping the bars, the original x values will be changed to 0,1,2...,an number array incremented by 1, regardless of their original value. So setting the x values are meaningless, they will be replaced in the future.

I designed two methods of setting data. One is ```AddDataSet```, it requires a label, which is the label of data set. It also requires a list of numbers, which will be the length of bars in the data set. The other is ```AddEntry```, it requires the dataset label and y value. A new bar will be added to the data set specified by the label, to the right of previous bars. Fail if the data set does not exist.

In line chart or bar chart, x axis values might have their special meaning. Users should be able to customize the axis values. I provided a simple solution: ```SetXAxisValues```. It requires a list of strings. The first string in the list will be shown in position 0 of the x label. Second string in 1, etc.

MPAndroidChart library supports many different styling methods. My component didn't include all of them. I chose some important methods. Supported methods are shown below.


## API Documentation

## Pie Chart

### AddEntry
```java
void AddEntry(float value,String label);
```
Add an entry to the chart, a new sector will be added to the chart after calling this method.

### SetColorList
```java
void SetColorList(YailList list);
```
Set the colors of every sectors of the chart, in the order of time when the sector is created by ```AddEntry```.

### RemoveEntry
```java
void removeEntry(String label);
```
Remove one sector of the pie chart specified by the label. If more than one sectors with same label exists, the earlist created one will be removed.

### RemoveAllData
```java
void removeAllData();
```
The pie chart will be cleared.

### CenterHoleRadius

Set the radius of center hole of the pie chart. Only available in designer panel.

### LabelEnabled

Set whether the label of entry is shown in the chart. Only available in designer panel.

### LabelEnabled

Set whether the legend is shown in the chart. Only available in designer panel.

### LabelTextColor

Set the text color of labels in the chart. Only available in designer panel.

### LabelTextSize

Set the text size of labels in the chart. Only available in designer panel.

### ValueTextColor

Set the text color of values in the chart. Only available in designer panel.

### ValueTextSize

Set the text size of values in the chart. Only available in designer panel.

## Line Chart

### AddDataSet

```java
void AddDataSet(String label)
```
Add a new data set to the line chart. One data set is one polygonal line in the chart. the label string will be shown in the legend. Labels shouldn't be duplicate.

### AddEntry

```java
void AddEntry(String label, float xVal, float yVal)
```
Create a new point in the line chart. a new line will connect the new point and the last point of data set specified by label. If multiple data sets has same label, the entry will only be added to the first one. If no data set has the particular label, the call will fail. If the x value is less than the x value of last data entry, it will also not perform, because line chart doesn't support Z-shaped lines.

### SetColorList

```java
void SetColorList(YailList colors)
```
Set the colors of every polygonal lines of the chart, in the order of time when the data set is created by ```AddDataSet```.

### SetXAxisValues
```java
void SetXAxisValues(YailList list)
```
Set the values that will be shown in the x axis, replacing the original values (0,1,2...).

### RemoveDataSet
```java
void RemoveDataSet(String label)
```
Remove a data set and all its entries specified by the label. Fails if no data set is named by the label.


### LegendEnabled

Same method described in Pie Chart.

### DisplayValue

If enabled, the y value will be shown near the entry point. Only available in designer panel.

### ScaleEnabled

If enabled, the chart can be scaled by two fingers slipping on the screen in opposite direction. Only available in designer panel.

### DragEnabled

If enabled, the chart can be dragged by one finger slipping on the screen. Only available in designer panel.


### DrawVerticalAxisLine

If enabled, vertical axis lines will be drawn.

### DrawHorizontalAxisLine

If enabled, horizontal axis lines will be drawn.

### OtherTextSize

Set the text size other than data value text.(axis, lenends, etc)

### ValueTextColor

Set the color of value texts.

### ValueTextSize

Set the size of value texts.

## BarChart

### AddDataSet
```java
void AddDataSet(String label,YailList data)
```
Add a new data set to the bar chart. One data set is a group of bars in the bar chart. Argument 'data' is a list of numbers, corresponding to the value of every natural numbers in x axis. For example, if the data argument is a list of \[2,3,4\], three bars will be drawn. The first is at position 0 in x axis and its height is 2. The second is at position 1 in x axis and its height is 3, etc. 'data' can also be an empty list.

### AddEntry
```java
void AddEntry(String label, float yVal)
```
Add an entry to a data set specified by string label. The entry will be added to the right of the last entry of the particular data set. Fails if the particular label does not exist.


### DrawVerticalAxisLine

Same method described in Line Chart.

### DrawHorizontalAxisLine

Same method described in Line Chart.

### SetColorList

```java
void SetColorList(YailList colors)
```
Set the colors of every bar groups of the chart, in the order of time when the data set is created by ```AddDataSet```. Different bars in the same data set share the same color.

### RemoveDataSet
```java
void RemoveDataSet(String label)
```
Remove a data set and all its entries specified by the label. Fails if no data set is named by the label.

### SetXAxisValues

Same as described in Line Chart.

### DisplayValue

Same as described in Line Chart.

### FontSize

Set the size of every text in the chart.

### LegendEnabled

Same as described in Pie Chart.

### ValueTextColor

Same as described in Pie Chart.


## User Feedback

I asked my friend to test my components, and he provided me with the following feedback. 

### About App Inventor

- App Inventor provides a way to set a list of data of unfixed length. But it is too inconvenient. Everytime when user add a block, he has to drag a new 'Item' block. Users should be able to set the length of the list explicitly.

- Sometimes two blocks can join even if their type doesn't match.

### About Chart Component

- The line chart should support two different Y axises(on left and right).
