\_\_TOC\_\_

# Overview

There are 4 events related to a header:

## onHeaderClick

This event is fired when a user left clicks on Spreadsheet's header.
When a corresponding event listener is invoked, a
<javadoc directory="zss">org.zkoss.zss.ui.event.HeaderMouseEvent</javadoc>
object is passed as an argument.

## onHeaderDoubleClick

This event is fired when a user double clicks on Spreadsheet header.
When a corresponding event listener is invoked, a
<javadoc directory="zss">org.zkoss.zss.ui.event.HeaderMouseEvent</javadoc>
object is passed as an argument.

## onHeaderRightClick

This event is fired when a user right clicks on Spreadsheet header. When
a corresponding event listener is invoked, a
<javadoc directory="zss">org.zkoss.zss.ui.event.HeaderMouseEvent</javadoc>
object is passed as an argument.

## onHeaderUpdate

This event is fired when a user resize a row (or column) header. When a
corresponding event listener is invoked, a
<javadoc directory="zss">org.zkoss.zss.ui.event.HeaderUpdateEvent</javadoc>
object is passed as an argument.

# Popup Menu Example

Look at the screenshots below, we can show different custom popup menus
when a users click a column or row header.

![ center](zss-essentials-events-columnMenu.png " center")

![ center](zss-essentials-events-rowMenu.png " center")

To popup our custom menu, we should disable built-in context menu
(`showContextMenu="false"` or un-specified) first and listen
onHeaderRightClick event.

``` xml
    <window title="ZSS Mouse Events" border="normal" width="100%"
        height="100%" apply="org.zkoss.zss.essential.events.MouseEventsComposer">
        <spreadsheet width="600px" height="300px" 
            maxVisibleRows="100" maxVisibleColumns="40" 
        showFormulabar="true" showToolbar="true" src="/WEB-INF/books/blank.xlsx" >
        </spreadsheet>

        <menupopup id="topHeaderMenu">
            <menuitem id="insertLeftMenu" label="Insert Left" />
            <menuitem id="insertRightMenu" label="Insert Right" />
            <menuitem id="deleteColumnMenu" label="Delete" />
        </menupopup>
        <menupopup id="leftHeaderMenu">
            <menuitem id="insertAboveMenu" label="Insert Above" />
            <menuitem id="insertBelowMenu" label="Insert Below" />
            <menuitem id="deleteRowMenu" label="Delete" />
        </menupopup>
    </window>
```

  - Line 3, 4: Do not specify `showContextMenu` to disable built-in
    context menu.
  - Line 8, 13: Create custom popup menus.

<!-- end list -->

``` java

public class MouseEventsComposer extends SelectorComposer<Component> {

    @Wire
    private Menupopup topHeaderMenu;
    @Wire
    private Menupopup leftHeaderMenu;
    
    @Listen("onHeaderRightClick = #ss")
    public void onHeaderRightClick(HeaderMouseEvent event) {
        
        switch(event.getType()){
        case COLUMN:
            topHeaderMenu.open(event.getClientx(),  event.getClienty());
            break;
        case ROW:
            leftHeaderMenu.open(event.getClientx(),  event.getClienty());
            break;
        }
    }
}
```

  - Line 8: Annotate event listener to list onHeaderRightClick event.
  - Line 11: The `getType()` returns an enumeration
    <javadoc>org.zkoss.zss.ui.event.HeaderType</javadoc> that can tell
    you which header is clicked.
  - Line 13, 16: Show up custom menus at the position where a user right
    clicks.
