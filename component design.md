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

### LabelTextColor

Set the text color of labels in the chart. Only available in designer panel.

### LabelTextSize

Set the text size of labels in the chart. Only available in designer panel.

### ValueTextColor

Set the text color of values in the chart. Only available in designer panel.

### ValueTextSize

Set the text size of values in the chart. Only available in designer panel.


