---
title: Data Validation & Freeze
---

# Data Validation
Data validation allows you to make a list of the entries that restrict the values allowed in a cell. Input values will be checked against the restrictions. In the Budget Summary Application Demo of the tutorial project, quantity fields are restricted to accept only positive integers. It will prompt a warning when a non-positive integer is being inputted.

```java
DataValidation validation = selectedRange.createDataValidation();
validation.setFormula1("=A1:A4");
validation.setType(DataValidation.Type.List); //currently-supported type
validation.setAlertStyle(DataValidation.AlertStyle.Stop);
validation.setInputTitle("my input title");
validation.setInputMessage("please input");
validation.setErrorTitle("sorry");
validation.setErrorMessage("error value");
selectedRange.setDataValidation(validation);
```

# Freeze
You can lock rows/columns or an area so that the area is always displayed on the screen. To freeze cells in Keikai: 

Select a cell then call `range.freezePanes()`

You can explore more methods at [Range Javadoc](https://keikai.io/javadoc/latest/io/keikai/client/api/Range.html).