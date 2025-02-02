Hiding rows or columns may come in handy when we don't need some cells
temporarily. Before hiding (or unhiding) rows or columns by API, you
should make your selection become row selection or column selections by
`Range.toRowRange()` or `Range.toColumnRange()`. Here are examples:

**Hide and unhide selected row**

``` java
        //convert to column range or row range before hiding or unhiding.
        Range rowRange = Ranges.range(ss.getSelectedSheet(), ss.getSelection());
        rowRange = rowRange.toRowRange();
        rowRange.setHidden(true);

        //CellOperationUtil checks sheet protection before hiding a range
        CellOperationUtil.hide(rowRange);
        CellOperationUtil.unhide(rowRange);
```

**Hide a column**

``` java
Range columnRange = Ranges.range(ss.getSelectedSheet(), ss.getSelection());
columnRange = columnRange.toColumnRange();
columnRange.setHidden(true);
```

If you don't convert it before calling API, it won't take effect.
