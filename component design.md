# Design of Plot Components

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

