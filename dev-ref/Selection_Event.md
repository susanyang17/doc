\_\_TOC\_\_

# Overview

The following events involve changing selected range of cells.

## onCellFocus

This event is fired when a cell gets focused by mouse clicking or using
key. When a corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.CellEvent</javadoc>
object is passed as an argument.

## onCellSelection

This event is fired when a user selects a cell by clicking or a group of
cells by dragging mouse. It is also fired if a user selects a row or a
column by clicking their headers which means selecting the whole row (or
column). When a corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.CellSelectionEvent</javadoc>
object is passed as an argument.

## onCellSelectionUpdate

This event is fired when a user drags to move cells or drags the fill
handle. When a corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.CellSelectionUpdateEvent</javadoc>
object is passed as an argument.

There are two features, "auto fill" and "move cells' content", depend on
this event. They listen the event and perform their operation like
filling cells. Notice that your event listener might affect these
features.

# Event Monitor Example

In our Event Monitor application, you can see the mouse pointer becomes
a 4-direction arrow pointer. That means we move the selection area.
Thus, you can selection update message on the right hand side panel.

![ center](/assets/images/dev-ref/zss-essentials-events-selection.png " center")

The following codes demonstrate how to listen above events and get
related data from them.

``` java
public class EventsComposer extends SelectorComposer<Component>{
    //omitted codes...

    @Listen("onCellFocus = #ss")
    public void onCellFocus(CellEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Focus on[")
        .append(Ranges.getCellRefString(event.getRow(),event.getColumn())).append("]");
        
        //show info...
    }
    
    @Listen("onCellSelection = #ss")
    public void onCellSelection(CellSelectionEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Select on[")
        .append(Ranges.getAreaRefString(event.getSheet(), event.getArea())).append("]");
        
        //show info...
    }
    
    @Listen("onCellSelectionUpdate = #ss")
    public void onCellSelectionUpdate(CellSelectionUpdateEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Selection update from[")
        .append(Ranges.getAreaRefString(event.getOrigRow(),event.getOrigColumn()
                , event.getOrigLastRow(),event.getOrigLastColumn()))
        .append("] to [")
        .append(Ranges.getAreaRefString(event.getSheet(), event.getArea())).append("]");

        //show info...
    }


}
```

  - Line 4, 13, 22: Apply `@Listen` to listen an event with the syntax
    `[EVENT NAME] = [COMPONENT SELECTOR]`. All event name can be found
    in <javadoc directory="keikai">io.keikai.ui.event.Events</javadoc>.
    The "\#ss" is the component selector which means the component with
    id `ss` on the ZUL page. (SelectorComposer supports various selector
    syntax that let you select components easily. Please refer to [ZK
    Developer's Reference/MVC/Controller/Wire
    Components](ZK_Developer's_Reference/MVC/Controller/Wire_Components "wikilink"))
    .
  - Line 8: You can get focused cell's row and column index (0-based).
  - Line 17: You can get selection area by `event.getArea()`.
  - Line 26: You can get the selection area before and after it changes.

# Range Selection Example

A pratical use case of `onCellSelection` event is to build a range
selection dialog, e.g. let users select a cell range for futher
processing without entering it by a keyboard. An example is showed by
the screenshot below:

![ center](/assets/images/dev-ref/zss-essentials-rangeSelectionDialog.png " center")

When opening the dialog to select a range, we can hide edit UI and
cancel `onStartEditing` event to forbid users editing.

In the code below, we put cell address string converted from
`CellSelectionEvent` in the Textbox of the dialog.

``` java
    @Listen("onCellSelection = #dialog")
    public void onCellSelection(CellSelectionEvent event){
        Textbox rangeBox  = (Textbox)dialog.getFellow("rangeBox");
        Range selection =Ranges.range(event.getSheet(), event.getArea()); 
        if (selection.isWholeRow()){
            rangeBox.setValue(Ranges.getRowRefString(event.getRow()));
        }else if (selection.isWholeColumn()){
            rangeBox.setValue(Ranges.getColumnRefString(event.getColumn()));
        }else{
            rangeBox.setValue(Ranges.getAreaRefString(event.getSheet(), event.getArea()));
        }
    }
```

You can find the implementation detail in our example source code.
