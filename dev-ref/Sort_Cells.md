Sorting a range of cell data is a commonly-used feature. To sort cells
with `Range` is quite easy like:

``` java
//true for descending order, false for ascending
range.sort(true);

//use CellOperationUtil, it checks sheet protection before sorting
CellOperationUtil.sort(range, true);
```

When sorting a range of texts and numbers In ascending order, numbers
will be arranged before text.

A range of cells before sorting:

![ center](/assets/images/dev-ref/zss-essentials-sortBefore.png " center")

A range of cells after sorting in ascending order:

![ center](/assets/images/dev-ref/zss-essentials-sortAfter.png " center")
