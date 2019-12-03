# Overview

These events are related to sheet operation such as creating, selecting,
deleting, and renaming a sheet.

## onSheetSelect

This event is fired when a user clicks on sheet bar to select a sheet.
When a corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.SheetSelectEvent</javadoc>
object is passed as an argument.

## onAfterSheetCreate

This event is fired after a user creates a new sheet. When a
corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.SheetEvent</javadoc>
object is passed as an argument.

## onAfterSheetNameChange

This event is fired after a user has renamed a sheet. When a
corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.SheetEvent</javadoc>
object is passed as an argument.

## onAfterSheetOrderChange

This event is fired after a user changes the order of a sheet. When a
corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.SheetEvent</javadoc>
object is passed as an argument.

## onAfterSheetDelete

This event is fired after a user deletes a sheet. When a corresponding
event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.SheetDeleteEvent</javadoc>
object is passed as an argument.

# Event Monitor Example

Below is a [ Event
Monitor](ZK_Spreadsheet_Essentials_3/Working_with_Spreadsheet/Handling_Events/Cell_Clicking_Event#Event_Monitor_Example "wikilink")
application's screenshot about sheet operations. You can see from the
right hand side panel that we create a "sheet3", select it, move it,
rename it to "essentials", and delete it finally.

![ center](/assets/images/dev-ref/zss-essentials-events-sheet.png " center")

``` java
public class EventsComposer extends SelectorComposer<Component>{
    //omitted codes...
    
    @Listen("onSheetSelect = #ss")
    public void onSheetSelect(SheetSelectEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Select sheet : ").append(event.getSheetName());
        
        //show info...
    }

    @Listen("onAfterSheetCreate = #ss")
    public void onAfterSheetCreate(SheetEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Create sheet : ").append(event.getSheetName());
        
        //show info...
    }
    
    @Listen("onAfterSheetNameChange = #ss")
    public void onAfterSheetNameChange(SheetEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Rename sheet to ").append(event.getSheetName());
        
        
        //show info...
    }
    
    @Listen("onAfterSheetOrderChange = #ss")
    public void onAfterSheetOrderChange(SheetEvent event){
        StringBuilder info = new StringBuilder();
        Sheet sheet = event.getSheet();
        info.append("Reorder sheet : ").append(event.getSheetName())
        .append(" to ").append(sheet.getBook().getSheetIndex(sheet));
        
        if(isShowEventInfo(event.getName())){
            addInfo(info.toString());
        }
    }
    
    @Listen("onAfterSheetDelete = #ss")
    public void onAfterSheetDelete(SheetDeleteEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Delete sheet : ").append(event.getSheetName());
        
        //show info...
    }
    
}
```

  - Line 4, 12, 20, 29, 41: Apply `@Listen` to listen an event with the
    syntax `[EVENT NAME] = [COMPONENT SELECTOR]`. All event name can be
    found in
    <javadoc directory="keikai">io.keikai.ui.event.Events</javadoc>.
    The "\#ss" is the component selector which means the component with
    id "ss" on the ZUL page. (SelectorComposer supports various selector
    syntax that let you select components easily. Please refer to [ZK
    Developer's Reference/MVC/Controller/Wire
    Components](ZK_Developer's_Reference/MVC/Controller/Wire_Components "wikilink"))
    .
