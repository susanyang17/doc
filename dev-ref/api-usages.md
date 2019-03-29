---
title: "API Usage"
---

# Creating a New Spreadsheet
```java
Spreadsheet spreadsheet = Keikai.newClient("http://remote-dart-server-address");
```

# Loading Keikai JS API
```java
// Java Part
String keikaiJsUri = spreadsheet.getURI(domElementId); // pass the DOM element id to it
```

```xml
// zul Part
<script async defer src="${keikaiJsUri}"></script>
```


# Current sheet
`Spreadsheet.getWorksheet()`


# Filling In Cells Data
```java
// The ready() returns a CompletableFuture, and then you call thenRun() with a lambda function. It will call the lambda function when keikai server is available to accept your commands
spreadsheet.ready()
.thenRun(() -> {
    for (int row = 0; row < 10; row++) {
        for (int col = 0; col < 10; col++) {
	    spreadsheet.getRange(row, col).applyValue(value); // The value is either String or Number value 
	}
    }
});
```

# Applying Cell Style
```java
// Font
Range range = spreadsheet.getRange("A1:B4");
Font font = range.createFont();
font.setName("Calibri");
font.setBold(true);
font.setSize(20);
range.applyFont(font);
```

Or using a CellStyle Object
```java
CellStyle cellStyle = range.createCellStyle();
Font font = cellStyle.createFont();
// styling with Font
cellStyle.setFont(font); // not applied to remote server yet.

// styling with Border
Border border = cellStyle.createBorder();
border.setColor("#ff00ff");
border.setStyle("dash"); 
cellStyle.setBorder("edgeBottom", border);

range.applyCellStyle(cellStyle); // now, it will apply to remote server.
```

# Importing an Excel file (xlsx only)
```java
spreadsheet.imports(new File("../foo/bar/baz.xlsx")); // load the excel file to the current workbook.
```

# Event Listeners
```java
//Events.ON_MOVE_FOCUS
spreadsheet.addEventListener(Events.ON_SELECTION_CHANGE, (RangeSelectEvent rangeSelectEvent) -> {});

// Events.ON_CELL_CLICK, Events.ON_CELL_RIGHT_CLICK, Events.ON_CELL_DOUBLE_CLICK
spreadsheet.addEventListener(Events.ON_CELL_RIGHT_CLICK, (CellMouseEvent cellMouseEvent) -> {});

spreadsheet.addEventListener(Events.ON_KEY_DOWN, (RangeKeyEvent rangeKeyEvent) -> {});
```

# Tooltip on a Sheet
`spreadsheet.getWorksheet().setTooltip("my tooltip")`


# disable a feature

```java
spreadsheet.setUserActionEnabled(AuxAction.ADD_SHEET, false);
```