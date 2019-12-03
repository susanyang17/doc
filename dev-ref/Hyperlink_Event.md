# Overview

There is only one hyperlink event that Keikai spreadsheet supports.

## onCellHyperlink

This event is fired when a user clicks a hyperlink in a cell. A browser
will open the specified hyperlink and send the event to a server. When a
corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.CellHyperlinkEvent</javadoc>
object is passed as an argument.

# Event Monitor Example

The [ Event
Monitor](ZK_Spreadsheet_Essentials_3/Working_with_Spreadsheet/Handling_Events/Cell_Clicking_Event#Event_Monitor_Example "wikilink")
application's screenshot when we click the link <http://www.zkoss.org>
<http://www.zkoss.org> in A7. ![
center](/assets/images/dev-ref/zss-essentials-events-hyperlink.png " center")

``` java
public class EventsComposer extends SelectorComposer<Component>{
    //omitted codes...

    @Listen("onCellHyperlink = #ss")
    public void onCellHyperlink(CellHyperlinkEvent event){
        StringBuilder info = new StringBuilder();
        
        info.append("Hyperlink ").append(event.getType())
            .append(" on : ")
            .append(Ranges.getCellRefString(event.getRow(),event.getColumn()))
            .append(", address : ").append(event.getAddress());
        
        //show info...
    }       

}
```

  - Line 11: We can get the clicked hyperlink address.
