---
title: "Features and Usages"
---

# Copy & Paste
Keikai currently doesn't support to paste content copied from an external application (e.g. Excel, text editor) via UI below:
* "Paste" button on the toolbar
* "paste" item in the context menu

It will show a warning:
`Please use shortcut ⌘V to paste what you cut or copied.`

Because a browser needs user-granted permission to access system clipboard.


# Supported Hotkeys
* Ctrl+C | Copy
* Ctrl+X | Cut
* Ctrl+V | Paste
* Ctrl+Z | Undo
* Ctrl+Y | Redo
* Ctrl+A | select all / selects the current region that contains data
* Delete  | Clear Content
* Esc                        | Clear or Copy/Cut Clipboard
* Up/Down/Left/Right         | Move Focus
* Shift + Up/Down/Left/Right | Update Selection
* Ctrl + Up/Down/Left/Right | Move the Focus to the Edge
* PageUp / PageDown |


# Language
Keikai will detect your browser's language setting to display the corresponding language with its UI.

Currently, the supported UI language are:
* English
* Tranditional Chinese

# Supported Chart Type:
* AreaChart
* LineChart 
* RadarChart
* ScatterChart scatterchart.xlsx scatterLineChart.xlsx
* PieChart
* Pie3DChart 
* DoughnutChart
* BarChart
* Bar3DChart 
* BubbleChar bubblechart.xlsx
<!-- https://github.com/zkoss/keikai/issues/901 -->


# Exceeding Maximal Column Warning
When you insert a column, if you see the alert:

`This operation cannot work because it will push non-empty cells out of the worksheet.`

That means there is data at the far right of your worksheet, and inserting columns will push the data out of the maximal column. Therefore, Keikai prevents you from inserting.

**Solution:**
Remove the data at the far right of your worksheet.