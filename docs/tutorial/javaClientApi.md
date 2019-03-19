---
title: Java Client API Basics
---

Keikai also comes with a complete set of Java API which let you control Keikai to achieve spreadsheet related functions including editing, like set/get data, style, format, manipulating cells/rows/columns, and all other operations that you can do on a toolbar/context menu. In the following sections, you will learn how to use these APIs.


# Load an xlsx File
You can import a file with the API of `Spreadsheet` below:

**MyEditor.java**

`spreadsheet.importAndReplace(defaultXlsx, defaultFile);`

In the [tutorial project](https://github.com/keikai/keikai-tutorial), we load xlsx files from the default folder `/WEB-INF/book/`.


# Access Cell Values
Next, you may want to change a cell's value or insert a column. Then you must know `Range` API.

## Range API
A `Range` object can represent a single cell or a range of cells in a worksheet. It is the main class that allows you to manipulate values, styles, and formats of cells. You can also perform an user action such as "insert"/"delete" cell/row/column, "merge", "sort", "filter", or "auto fill" or any other operations you can do on a toolbar/context menu.

Keikai Java client offers different ways to get a `Range` for different purposes, including:

**One cell:**

```java
spreadsheet.getRange(0, 0); //rowIndex, columnIndex
spreadsheet.getRange("A1");
```

**Multiple cells**

```java
spreadsheet.getRange(0, 0, 2, 2);  //rowIndex, columnIndex, numberOfRows, numberOfColumns
spreadsheet.getRange("A1:B2");
```

**Active cell**

Active cell means the cell being selected currently in a browser.

```java
spreadsheet.getActiveCell();
```

If you didn't specify a sheet index in those methods, by default it will return cells in the active sheet, which is the currently selected sheet.

To select cells in a specific sheet:

```java
// bookName, sheetIndex, rowIndex, columnIndex
spreadsheet.getRange("app.xlsx", 0, 0, 0);
// bookName, sheetIndex, numberOfRows, numberOfColumns
spreadsheet.getRange("app.xlsx", 0, 2, 2);
```
For complete API list, please refer to [Javadoc]({{page.javadoc}}io/keikai/client/api/Spreadsheet.html).

## Set a Cell Value
You can pass a `String` or a `Number` to set a cell's value.

```java
range.setValue("text");
range.setValue(123);
range.setValue(3.5);
```
If the `range` contains multiple cells, then it will fill all cells in the range with a same value.

## Get a Cell Value
The simplest way is: 

```java
String text = range.getValue();
Number number = range.getValue();
```

This method will return `String` or `Number`, so you have to assign to the expected type.

If you want a specific return type, you can call the following methods:

```java
range.getRangeValue().getCellValue().getStringValue();
range.getRangeValue().getCellValue().getDoubleValue();
range.getRangeValue().getCellValue().getBooleanValue();
range.getRangeValue().getCellValue().getDateValue();
```

### Get Multiple Cell Values at Once
From the architecture above, you can know that each method calling of Keikai Java client requires to communicate with Keikai server via the network. To have better performance and shorter network transmission time, it's better to get multiple values at once than one cell by one cell.


```java
List<String> cellValues = spreadsheet.getRange(row, col, 1, 4).getValues();
String value = cellValues.get(0);
```


## Insert Rows/Columns
To insert one/multiple rows, you have to select rows or columns first. Then, call `insert()` to insert the same number of rows in the `range`. For example, if the `range` contains 3 rows, then `insert()` will insert 3 rows. 

**Insert 3 Rows**

```java
Range range = spreadsheet.getRange("1:3")
range.insert(InsertShiftDirection.ShiftDown, InsertFormatOrigin.LeftOrAbove);
```

The 1st parameter specifies the direction Keikai shifts existing rows. We usually shift rows down so we specify `InsertShiftDirection.ShiftDown` here. The 2nd parameter specifies where Keikai should copy the style from. In this case, the new 3 rows will copy the styles from the row above them. 

**Insert 3 Columns**

The same rule applies to column insertion. You need to get a column range and call `insert()` with similar parameters.

```java
spreadsheet.getRange("A:C");
range.insert(InsertShiftDirection.ShiftToRight, InsertFormatOrigin.LeftOrAbove);
```


## Delete Rows/Columns
The deletion API is simpler than insertion because you only need to specify the shift direction:

```java
Range range = spreadsheet.getRange("1:3");
range.delete(DeleteShiftDirection.ShiftUp);
```


## Convert to Entire Row/Column
Sometimes you only have a range of cells returned by a method:
`Range range = findRange(); //return a range of A1:A3`

But you want to perform an operation that works on the whole row/column. Keikai offers an easy way to turn your range selection into row/column selection, just call:

```java
range.getEntireRow();
range.getEntireColumn();
```

If `range` is `A1:A3`, then `getEntireRow()` returns a range `1:3`, row 1 to row 3.

For details, please refer to [Javadoc]({{page.javadoc}}io/keikai/client/api/Range.html).


# Applying Styles & Formats 
To apply a style, we have to:

1. Create the style related object, e.g. `Font`, `Borders`, or `PatternFill`

2. Assign the style object to the `Range`

For example, to make a cell text bold:

```java
Font font = range.createFont();
font.setBold(true);
range.setFont(font);
```

You can follow a similar way to apply borders:

```java
Borders borders = range.createBorders(Borders.BorderIndex.EdgeBottom);
borders.setStyle(Border.Style.Thin);
borders.setColor("#000000");
range.setBorders(borders);
```

## Number/Date/Time Format
`setNumberFormat()` can be used to set numbers, dates, or time formats:

```java
range.setNumberFormat("###");
range.setNumberFormat("@");
range.setNumberFormat("yyyy-mm-dd");
range.setNumberFormat("h:mm:ss");
```


At this point, you already can load an xlsx file in Keikai and access cells to perform basic operations like getting/setting values, insertion, deletion, and formatting. In the next section we will quickly go through some of the advanced features that you can do with `Range`.