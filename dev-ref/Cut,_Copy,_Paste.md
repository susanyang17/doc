# Overview

To copy a range of cells, you should use
<javadoc directory="keikai">io.keikai.api.Ranges</javadoc> to select
them and call `paste(Range)` with another `Range` object for destination
like:

``` java
        Range src = Ranges.range(ss.getSelectedSheet(), ss.getSelection());
        Range destination = Ranges.range(getDestinationSheet(), ss.getSelection());
        src.paste(destination);
```

Similarly, the steps to cut a range is to copy them first, after pasting
to destination, just clear the source range's content.

Cutting a range of cells is similar to copy:

``` java
        Range src = Ranges.range(ss.getSelectedSheet(), ss.getSelection());
        Range destination = Ranges.range(getDestinationSheet(), ss.getSelection());
        src.paste(destination, true);
```

There is also a `pasteSpecial()` to do special pasting like pasting
value only or pasting formula only.

With the help of
<javadoc directory="keikai">io.keikai.api.CellOperationUtil</javadoc>,
we can easily perform copying and cutting, and it also provides methods
for "paste special" such as `pasteValue()`, or `pasteFormula()`. These
methods all require 2 `Range` objects as arguments. One is source and
another is destination.

To **cut** a range of cells, you should use

``` java
CellOperationUtil.cut(srcRange, destRange);
```

To **copy** a range of cells, you should use

``` java
CellOperationUtil.paste(srcRange, destRange);
```

The usages for `pasteFormula()`, `pasteValue()`, `pasteTranspose()`, and
`pasteAllExceptBorder()` are all the same.

# Example

The following codes copy a selection range to the same position of
another sheet when a user clicks a button.

``` java

public class CopyCutComposer extends SelectorComposer<Component> {

    @Wire
    private Spreadsheet ss;


    @Listen("onClick = #copyButton")
    public void copyByUtil() {
        Range src = Ranges.range(ss.getSelectedSheet(), ss.getSelection());
        Range dest = Ranges.range(getResultSheet(), ss.getSelection());
        CellOperationUtil.paste(src, dest);
    }
    
    //omitted codes...
}
```
