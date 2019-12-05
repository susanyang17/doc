---
title: 'Features and Usages'
---
# Spreadsheet User Interface Overview

![center](/assets/images/dev-ref/essentials-feature-ui.png)

This is the screenshot of Keikai spreadsheet's user interface, each section
is introduced as follows:

1.  Toolbar
      -   
        The toolbar contains all commonly-used features including controls to
        set cell's style, alignment, border, background color, font,
        font color, merging (and unmerging), sorting, auto
        filter, protection, grid line visibility and to insert charts, images, and hyperlinks.
        The 3 leftmost buttons, "New Book", "Save Book", and "Export to
        PDF" are not built-in features as they highly depend on your application settings. You will have to implement the logic by
        yourself and associate them with the buttons.
2.  Formula bar
      -   
        It displays text or formula of the current selected cell. It can also be used for entering or editing a formula or data.
3.  Sheet Area
      -   
        It displays the content of current selected sheet, this is also the area where users normally work with.
4.  Context menu
      -   
        A context menu is displayed when you right click on a cell, a column header, or a row header. It contains most options of the toolbar and works like a shortcut.
5.  Sheet bar
      -   
        Sheet bar displays a list of all sheets in this book. You can navigate to any sheet
        by clicking on it. You can add a sheet by clicking the + button on the left. If you right
        click on the sheet bar it pops up a context menu, and allows you to perform sheet operations.
        
        ![ center](/assets/images/dev-ref/essentials-feature-sheet-contextmenu.png)
        
        The hamburger menu next to the + icon is the sheet navigation button. It allows users to switch sheets conveniently.

# Features

## Integrated with ZK Charts

The charts in Keikai sheet is rendered by another ZK product called ZK Charts. When you hover your mouse
pointer over the charts, it will show related info in a tooltip. 

![ 900px |center](/assets/images/dev-ref/Zss-essential-zkchart.png " 900px | center")

## Rich Text Editing

You can apply multiple styles to a same cell by using the rich text editor. To open
a rich-text editor, right click a cell and select "Right Text Edit" in
the context menu.

![ center](/assets/images/dev-ref/essential-richtexteditor.png " center")

## Comment

To insert/edit/delete a comment, right click a cell and select
corresponding item in the context menu.

![ 550px](/assets/images/dev-ref/essential-edit-comment.png " 550px")

Show comment

![essential-display-comment.png](/assets/images/dev-ref/essential-display-comment.png
"essential-display-comment.png")

## Support Different Zoom Levels

Spreadsheet supports viewing in different zoom levels. You can change browser's
zoom level according to your needs.

## Display Currency Symbol of Different Countries

Keikai can display different currency symbols such as $, ¥, ₩,
€, and HKD in a cell with the currency format.

## Localization of Number/Formula Input

Keikai also accepts ','(comma) or '.'(dot) as the decimal point for decimal
numbers.

## Smart Input

When you enter numbers in a cell with the default format (General), Keikai
converts the numbers into the number format and sets its corresponding format automatically for you, for example 1,234,567, $123456,
($123456), ($1,234,567), 1.2% or 123456E10.

## Date Format

Some date formats in Keikai are regional (starting with an **asterisk,
\***, same as Excel ) and some are international. 

![center](/assets/images/dev-ref/zss-essentials-dateFormat.png " center") 

Regional ones will change its displaying format according to the system locale, but
international ones won't change. \[1\]

<references/>

## Conditional Formatting

Keikai can display conditional formatting set in an Excel file. This feature
allows you to highlight cells with the given conditions. In the case below, the values in the "Income" column has conditional formatting enabled: 

![center](/assets/images/dev-ref/zss-essentials-conditionalFormatting.png " center")

  - Modify conditional formatting in Keikai UI is not supported at the moment.

## Named Range
Keikai can read a named range from an xlsx file, so you can specify a named range in a formula like `=SUM(source)`. To create a named range, please reference javadoc [Range::createName](https://keikai.io/javadoc/).


# Supported Hotkeys

<table>
<thead>
<tr class="header">
<th><center>
<p>Hotkey</p>
</center></th>
<th><center>
<p>Action</p>
</center></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTRL+B</p></td>
<td><p>bold</p></td>
</tr>
<tr class="even">
<td><p>CTRL+C</p></td>
<td><p>copy</p></td>
</tr>
<tr class="odd">
<td><p>CTRL+I</p></td>
<td><p>italic</p></td>
</tr>
<tr class="even">
<td><p>CTRL+U</p></td>
<td><p>underline</p></td>
</tr>
<tr class="odd">
<td><p>CTRL+V</p></td>
<td><p>paste</p></td>
</tr>
<tr class="even">
<td><p>CTRL+X</p></td>
<td><p>cut</p></td>
</tr>
<tr class="odd">
<td><p>CTRL+Y (EE only)</p></td>
<td><p>redo</p></td>
</tr>
<tr class="even">
<td><p>CTRL+Z (EE only)</p></td>
<td><p>undo</p></td>
</tr>
<tr class="odd">
<td><p>Delete</p></td>
<td><p>clear content</p></td>
</tr>
<tr class="even">
<td><p>Esc</p></td>
<td><p>clear copy/cut clipboard</p></td>
</tr>
<tr class="odd">
<td><p>CTRL+ARROW KEY</p></td>
<td><p>moves the selection box to the edge of the current data region in a sheet.</p></td>
</tr>
</tbody>
</table>

# Usage

In the following sections we will introduce the usages of some noticeable features.

## Copy & Paste

  - If you copy and paste within a Keikai component, it has full
    information at both server and client side, so such copy-paste can
    retain all cell information including styles, formula, format, and
    data validation.
  - If you copy a whole column/row, Keikai also copy its width and height. But if you are only
    copying one or multiple cells, Keikai won't copy the width and height to
    target cells.
  - If you wish to copy a whole sheet to another Keikai component,
    please call
    <https://www.zkoss.org/javadoc/latest/zss/org/zkoss/zss/api/Range.html#cloneSheetFrom-java.lang.String-io.keikai.model.Sheet->.
    It can clone a sheet from another `Book` object and is more performant.

### Copy/Paste Between Keikai and Other Applications like Excel

  - Such copy-paste will only work with **Ctrl+C** and **Ctrl+V**. The toolbar or context menu "Paste" button only works for copying cells within the same Keikai component and will not work across different applications.
  - Such copy-paste is an action between 2 applications (Excel and
    browser) through a system clipboard. Currently, Keikai only extract
    text content from a system clipboard, so this copy-paste only pastes
    "pure text" without any styles.
  - For example, a cell in Excel has a formula `=sum(1,2)` which is `3`. If you copy
    this cell and paste it into Keikai, the cell in Keikai gets `3` as a number.
    Just like you type `3` in a Keikai cell.
  - If you enter edit mode, select the text `=sum(1)` and copy it in
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

In addition to normal pasting, Spreadsheet also provides other special
pasting options on the toolbar. ![ center](/assets/images/dev-ref/essentials-feature-paste.png
" center")

You can select "Paste Special" to access all available pasting options
in a dialog. ![ center](/assets/images/dev-ref/essentials-feature-pasteSpecial.png " center")

## Custom Sort

The "Ascending" and "Descending" function can sort data by only one
column but "Custom sort" can sort data by multiple columns. ![
center](/assets/images/dev-ref/essentials-feature-customSort.png " center")

After selecting "Custom sort" on the toolbar, a dialog appears. You can
add sorting criteria to 3 columns at the most. If your data includes
column headings, make sure the "My data has headers" option is checked.
![ center](/assets/images/dev-ref/essentials-feature-customSortDialog.png " center")

The sorting result of criteria above: ![
center](/assets/images/dev-ref/essentials-feature-customSort-after.png " center")

## Auto Fill

Auto fill is a handy feature to fill cells with data in a particular
pattern based on selected cells. Text will be copied and numbers and
dates will be increased (or decreased).

To use this, You should select one or more cells and drag the fill
handle across or down the cells that you want to fill.

![ center](/assets/images/dev-ref/essentials-feature-autoFill-select.png " center")

Fill cells by dragging right, left, up, or down. ![
center](/assets/images/dev-ref/essentials-feature-autoFill.png " center")

The supported cell content are number, weekday (full/short), month
(full/short), and timestamp.

## Format Cell

A context menu appears when right clicking a cell, "Format Cell"
provides 10 different categories with total of 47 formats to apply on
cells. ![ center](/assets/images/dev-ref/essentials-feature-formatCell.png " center")

## Sheet Protection

If you enable "Protect Sheet" for a sheet in Excel, Spreadsheet will
keep this setting when reading the Excel file, hence, when you edit a
protected sheet, you will receive an alert message on the top left-hand
corner.

When a sheet is under protection, you can only edit those unlocked
cells. For those locked cells, you still can specify which action you
allow users to do.

![ center](/assets/images/dev-ref/zss-essentials-feature-protection.png " center")

## Filters

The filter can help you screen out data and work with a subset of data
in a range of cells without moving or deleting them.

When you click on the filter icon, there are 3 menu items: **Filter**,
**Clear**, and **Reapply** related to filter. ![
center](/assets/images/dev-ref/zss-essentials-filter-menu.png " center")

Click "Filter"
![zss-essentials-filter-filter-icon.png](/assets/images/dev-ref/zss-essentials-filter-filter-icon.png
"zss-essentials-filter-filter-icon.png") can enable / disable filters.
When filters are enabled, first row of each column will show up a
drop-down arrow icon
![zss-essentials-filter-dropdown-icon.png](/assets/images/dev-ref/zss-essentials-filter-dropdown-icon.png
"zss-essentials-filter-dropdown-icon.png"). If you click the drop-down
icon, a list of values appears and you can select from the list as a
filtering criterion to apply on data.

![ center](/assets/images/dev-ref/zss-essentials-filter-enable.png " center")

After you select some values click
![zss-essentials-ok.png](/assets/images/dev-ref/zss-essentials-ok.png "zss-essentials-ok.png"),
Spreadsheet will filter those data with selected values. Only those rows
with matching criteria will be displayed while others stay hidden.

You can also filter by multiple columns. Filters are additive, which
means that each filter is based on the existing filters and further
reduces the subset of data.

Click "Clear"
![zss-essentials-filter-clear-icon.png](/assets/images/dev-ref/zss-essentials-filter-clear-icon.png
"zss-essentials-filter-clear-icon.png") removes all applied criteria and
display all data available.

If you add new data row, you should click "Reapply"
![zss-essentials-filter-reapply-icon.png](/assets/images/dev-ref/zss-essentials-filter-reapply-icon.png
"zss-essentials-filter-reapply-icon.png"). Then, drop-down list will
update its values, and applied criteria will also work on new data.

`since 3.8.1`

**Filter by search.** When you enter text in the search box, it will
instantly list and select all matched values. Press "Enter" and Keikai will
filter your data with those matched values. ![
center](/assets/images/dev-ref/zss-essentials-filterBySearching.png " center")

`since 3.9.0`

Keikai supports **number filter**, **color filter**, **date filter**, and
**text filter**. ![ center](/assets/images/dev-ref/zss-essentials-colorFilter.png " center")

![ center](/assets/images/dev-ref/zss-essentials-dateFilter.png " center")

## Data Validation

Spreadsheet can read data validation settings of Excel files including
validation criteria of lists, numbers, decimals, dates, or time.
(Spreadsheet OSE will ignore validation settings.)

![ center](/assets/images/dev-ref/zss-essentials-validation-dialog.png " center")

If the validation criteria is a list, the cell will appear a drop-down
arrow icon. You can click the icon to select available values. ![
center](/assets/images/dev-ref/zss-essentials-validation-list.png " center")

When you click on the cell with validation, the input message you set
will appear automatically. ![
center](/assets/images/dev-ref/zss-essentials-validation-message.png " center")

If your input violates validation criteria, an error alert will pop up.
![ center](/assets/images/dev-ref/zss-essentials-validation-alert.png " center")

There are 3 types of alerts and each of them has a different icon in the
dialog. For an error alert
![zss-essentials-validation-error-icon.png](/assets/images/dev-ref/zss-essentials-validation-error-icon.png
"zss-essentials-validation-error-icon.png"), you can retry to enter
again or cancel to revert back to the original value. For a warning
alert
![zss-essentials-validation-warning-icon.png](/assets/images/dev-ref/zss-essentials-validation-warning-icon.png
"zss-essentials-validation-warning-icon.png") , you can click "Yes" to
accept the invalid input, "No" to edit the invalid input, or "Cancel" to
remove the invalid input. For a information alert
![zss-essentials-validation-information-icon.png](/assets/images/dev-ref/zss-essentials-validation-information-icon.png
"zss-essentials-validation-information-icon.png"), you can click "OK" to
accept the invalid value or "Cancel" to reject it.

  - custom validation is not supported yet.

<!-- end list -->

1.  <https://support.office.com/en-us/article/Format-a-date-the-way-you-want-8e10019e-d5d8-47a1-ba95-db95123d273e?ui=en-US&rs=en-US&ad=US&fromAR=1>
