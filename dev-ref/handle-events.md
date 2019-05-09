---
title: "Handle Events"
---

# Event Listening
When you interact with Keikai component in a browser, it will fire various events to your Java client if you register the corresponding event listener. This is the major way you implement your application/business logic. To register an event listener is simple like:

```java
spreadsheet.addEventListener(Events.ON_CELL_CLICK, (CellMouseEvent event) -> {
    //implement the application/business logic here
    ...
});
```

# Event Name - Event Class 
Keikai passes different event objects for different events, here we list all constants in [`Events`](https://keikai.io/javadoc/latest/io/keikai/client/api/event/Events.html) for each passed event class:

## CellMouseEvent
* ON_CELL_CLICK 
* ON_CELL_RIGHT_CLICK
* ON_CELL_DOUBLE_CLICK
* ON_CELL_MOUSE_ENTER
* ON_CELL_MOUSE_LEAVE

## RangeSelectEvent
* ON_MOVE_FOCUS
* ON_SELECTION_CHANGE

## RangeDragEvent 
* ON_DRAG_FILL
* ON_DRAG_MOVE

## RangeKeyEvent
* ON_KEY_DOWN
* ON_KEY_UP
* ON_KEY_PRESS

## CellEditEvent
* ON_EDIT_SAVE
* ON_EDIT_START
* ON_EDIT_CANCEL

## SheetEvent
* ON_SHEET_VISIBLE
* ON_SHEET_ACTIVATE
* ON_SHEET_ADD
* ON_SHEET_DELETE
* ON_SHEET_MOVE
* ON_SHEET_RENAME

## AuxActionEvent
* ON_AUX_ACTION

## CellHyperlinkEvent
* ON_HYPERLINK_CLICK

## ShapeEvent
* ON_SHAPE_CLICK
* ON_SHAPE_ACTION

# Mouse Hover
Notice that if you enabled this feature, it will generate a mass of mouse events (onCellMouseEnter and onCellMouseLeave) to Keikai and Java server.

You need to enable this feature first.
```java
Settings mySettings = Settings.DEFAULT_SETTINGS.clone();
mySettings.set(Settings.Key.SPREADSHEET_CONFIG, Maps.toMap("enableMouseEvent", true));
Spreadsheet spreadsheet = Keikai.newClient(..., mySettings);
```

Then add listeners:
```java
spreadsheet.addEventListener(Events.ON_CELL_MOUSE_ENTER, mouseEnterHandler::apply);
spreadsheet.addEventListener(Events.ON_CELL_MOUSE_LEAVE, mouseEnterHandler::apply);
```
