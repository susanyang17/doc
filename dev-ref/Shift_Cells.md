Shift a range of cells can be performed by calling `shift()` wit row and
column offset:

``` java
range.shift(rowOffset, columnOffset)
```

You can also use `CellOperationUtil.shift()` which checks protection for
you. The first Range object is your source range to be shifted. The
second argument is row offset. If it's positive, source range will be
shifted down, otherwise it will be shifted up. The third argument is
column offset. If it's positive, source range will be shifted right,
otherwise it will be shifted left.

Assume that we have selected a selected range of cells:

![ center](/assets/images/dev-ref/zss-essentials-shift-before.png " center")

We want to move the selected cells 3 columns to the right, we can write
the below code to shift it:

``` java
Range range = Ranges.range(spreadsheet.getSelectedSheet(), "F6:F10");
//move 3 columns to the right
CellOperationUtil.shift(range, 0, 3);
```

The result will be like: ![ center](/assets/images/dev-ref/zss-essentials-shift-after.png
" center")
