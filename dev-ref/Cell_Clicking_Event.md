\_\_TOC\_\_

# Overview

There are 3 events related to cell clicking:

## onCellClick

This event is fired when a user left clicks on a cell. When a
corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.CellMouseEvent</javadoc>
object is passed as an argument.

## onCellDoubleClick

This event is fired when a user double clicks on a cell. When a
corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.CellMouseEvent</javadoc>
object is passed as an argument.

## onCellRightClick

This event is fired when a user right clicks on a cell. When a
corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.CellMouseEvent</javadoc>
object is passed as an argument.

# Event Monitor Example

During [Handling
Events](ZK_Spreadsheet_Essentials_3.x/Working_with_Spreadsheet/Handling_Events "wikilink")
section, we will use a "Event Monitor" application as an example to
present how to listen an event and what data you can get from an event.
The image Below is a screenshot of "Event Monitor" application, when we
interact with the Spreadsheet on the left hand side, the panel on the
right hand side will shows messages about related events.

![ center](/assets/images/dev-ref/zss-essentials-events-cellClicking.png " center")

As you can see in the right panel, it shows messages when I click a
cell. We can achieve this in a controller very easily with `@Listen`. We
omit lots of similar codes and leave those codes that are worth for your
reference.

{% highlight java linenos %}
public class EventsComposer extends SelectorComposer<Component>{
    //omitted codes...

    @Listen("onCellClick = #ss")
    public void onCellClick(CellMouseEvent event){
        StringBuilder info = new StringBuilder();
        info.append("Click on cell ")
        .append(Ranges.getCellRefString(event.getRow(),event.getColumn()));
        
        //show event information...
    }
    @Listen("onCellRightClick = #ss")
    public void onCellRightClick(CellMouseEvent event){
        //show event information...
    }
    @Listen("onCellDoubleClick = #ss")
    public void onCellDoubleClick(CellMouseEvent event){
        //show event information...
    }
    
}
    
{% endhighlight %}

  - Line 4,12,16: Apply `@Listen` to listen an event with the syntax
    `[EVENT NAME] = [COMPONENT SELECTOR]`. All event name can be found
    in <javadoc directory="keikai">io.keikai.ui.event.Events</javadoc>.
    The "\#ss" is the component selector which means the component with
    id `ss` on the ZUL page. (SelectorComposer supports various selector
    syntax that let you select components easily. Please refer to [ZK
    Developer's Reference/MVC/Controller/Wire
    Components](ZK_Developer's_Reference/MVC/Controller/Wire_Components "wikilink"))
    .
  - Line 8: The `getRow()` returns 0-based row index of the cell which
    is in editing and `getColumn()` returns column index. The cell A1's
    row and column index are both 0. `Ranges.getCellRefString()` is a
    utility method which converts row and column index into a cell
    reference like A1.
