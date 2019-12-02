
## Display Currency Symbol of Different Countries
Keikai can display currency symbol of different countries such as $, ¥, ₩,
€, and HKD on a cell with currency format.

## Localization of Number/Formula Input
Keikai accepts ','(comma) or '.'(dot) as the decimal point for decimal numbers.

## Smart Input
When you enter a text in a cell with the default format (General), Keikai
converts some number input patterns such as 1,234,567, \$123456,
$123456, $1,234,567, 1.2%, 123456E10 into a number value and sets
its corresponding cell format automatically.

## Date Format
Some date formats in Keikai are regional (starting with an
**asterisk, \***, same as Excel ) and some are international. Regional ones will
change its displaying format according to the system locale, but
international one doesn't change.


## Conditional Formatting
Keikai can display conditional formatting of an Excel file. This feature
allows you to highlight a cell with a certain color according to the
cell's value.

(Modify conditional formatting is not supported yet.)

## Support Different Zoom Level
Keikai supports viewing in different zoom level. You can change
zoom level within a browser according to your need.


# Supported Hotkeys

  
| Hotkey  |    Action |
| CTRL+B  |   bold |
| CTRL+C  | copy |
| CTRL+I  | italic |
| CTRL+U  | underline |
| CTRL+V  | paste |
| CTRL+X  | cut |
| CTRL+Y  | redo |
| CTRL+Z  | undo |
| Delete  | clear content |
| Esc     |clear copy/cut clipboard |
| CTRL+ARROW KEY  |  moves the selection box to the edge of the current data region in a sheet |

## Rich Text Editing

You can apply multiple styles to a cell with a rich text editor. To open
a rich-text editor, right clicking a cell, select "Right Text Edit" in
the context menu.


# Usages

The following sections will introduce usages of some noticeable features.

## Copy & Paste

-   If you copy and paste inside a Keikai component, it has full
    information at both server and client side, so such copy-paste can
    retain all information of cells including styles, a formula, format,
    data validation.
-   If you copy a whole column/row, Keikai also copy the width/height. But
    copying one or multiple cells doesn't copy the width and height to
    target cells.
-   If you want to copy almost a whole sheet to another Keikai component,
    please call `Range.cloneSheetFrom()`. It can clone a sheet from another `Book`
    object.

### Between Keikai and Other Applications like Excel
-   Such copy-paste only works with **Ctrl+c** and **Ctrl+v**. Click
    "Paste" on the toolbar or context menu only works for copying cells
    inside one Keikai component.
-   Such copy-paste is an action between 2 applications (Excel and
    browser) through a system clipboard. Currently, Keikai only extract
    text content from a system clipboard, so this copy-paste only pastes
    the "pure text" you see on the screen without any specified style on
    cells.
-   For example, a cell in Excel with a formula `=sum(1)`, if you copy
    the cell and paste it to Keikai, the cell in Keikai gets `1` as a number.
    Just like you type `1` in a Keikai cell.
-   If you enter edit mode, select the text `=sum(1)` and copy it in
    Excel, then paste to a cell in Keikai. Keikai gets a formula, just like
    you type a formula in a Keikai cell.

### Between 2 Keikai components

Copy-paste cells between 2 Keikai components also rely on the system
clipboard, so it's a similar case like Keikai and Excel, only copying pure
text.

### limitation
Keikai can't paste a cell that has a multiline text into one cell of Keikai,
and it will split the text into multiple cells by rows.

### Special Paste

In addition to normal pasting, Keikai also provides other special
pasting options on the toolbar. 

You can select "Paste Special" to access all available pasting options
in a dialog.


## Custom Sort

The "Ascending" and "Descending" function can sort data by only one
column but "Custom sort" can sort data by multiple columns. 

After selecting "Custom sort" on the toolbar, a dialog appears. You can
add sorting criteria to 3 columns at the most. If your data includes
column headings, make sure the "My data has headers" option is checked.


## Auto Fill

Auto fill is a handy feature to fill cells with data in a particular
pattern based on selected cells. Text will be copied and numbers and
dates will be increased (or decreased).

To use this, You should select one or more cells and drag the fill
handle across or down the cells that you want to fill.


Fill cells by dragging right, left, up, or down. 

The supported cell content are number, weekday (full/short), month
(full/short), and timestamp.

## Format Cell

A context menu appears when right clicking a cell, "Format Cell"
provides 10 different categories with total of 47 formats to apply on
cells. 


## Sheet Protection

If you enable "Protect Sheet" for a sheet in Excel, Keikai will
keep this setting when reading the Excel file, hence, when you edit a
protected sheet, you will receive an alert message on the top left-hand
corner.

When a sheet is under protection, you can only edit those unlocked
cells. For those locked cells, you still can specify which action you
allow users to do.


## Filters

The filter can help you screen out data and work with a subset of data
in a range of cells without moving or deleting them.

When you click on the filter icon, there are 3 menu items: **Filter**,
**Clear**, and **Reapply** related to filter. 

Click "Filter" can enable / disable filters. When filters are enabled, first row of
each column will show up a drop-down arrow icon. If you click the drop-down icon, a list of values appears and you can
select from the list as a filtering criterion to apply on data.


After you select some values click
Keikai will filter those data with selected values. Only those rows with matching
criteria will be displayed while others stay hidden.

You can also filter by multiple columns. Filters are additive, which
means that each filter is based on the existing filters and further
reduces the subset of data.

Click "Clear" removes all applied criteria and display all data available.

If you add new data row, you should click "Reapply". Then, drop-down list will update its values, and applied criteria will
also work on new data.


**Filter by search.** When you enter text in the search box, it will
instantly list and select all matched values. Press "Enter" and Keikai will
filter your data with those matched values. 


Keikai supports **number filter**, **color filter**, **date filter**, and
**text filter**. 


## Data Validation

Keikai can read data validation settings of Excel files including validation criteria of lists, numbers, decimals, dates, or time. If the validation criteria is a list, the cell will appear a drop-down
arrow icon. You can click the icon to select available values. 

When you click on the cell with validation, the input message you set
will appear automatically. 

If your input violates validation criteria, an error alert will pop up.


There are 3 types of alerts and each of them has a different icon in the
dialog. For an error alert, you can retry to enter again or cancel to revert back to the original
value. For a warning alert, you can click "Yes" to accept the invalid input, "No" to edit the
invalid input, or "Cancel" to remove the invalid input. For a
information alert, you can click "OK" to accept the invalid value or "Cancel" to reject it.

(custom validation is not supported yet.)


## Comment

To insert/edit/delete a comment, right clicking a cell, select
corresponding item in the context menu.