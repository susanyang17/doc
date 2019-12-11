---
title: 'Handling Events'
---
When a user interacts with Spreadsheet like clicking or editing, these
actions trigger events being sent to the server. We can implement our
business logic in a event listener, a method in a controller, to listen
events we are interested in. When the event we listen is triggered, our
special business logic is performed. This mechanism helps you customize
Spreadsheet furthermore to fulfill your business needs.

Keikai spreadsheet supports numerous events such as mouse events, key
events, selection events, editing events and hyperlink events. You can
listen to these events to apply customized function upon your business
requirement. For example by listening to editing events such as
onStartEditing and onStopEditing you can control which cell the user can
edit, what is entered/edited and possibly apply some styling or value
transformation once the editing is stopped. Similarly, you can also
listen to mouse events such as onCellClick or onCellRightClick and
update other ZK components or pop up a menu.

In following sections, we will present examples of listening events and
they all use <javadoc>org.zkoss.zk.ui.select.SelectorComposer</javadoc>
which provides a quite simple way to listen a event, just apply
`@Listen` on a method and specify listening event names and target
components. (For complete explanation, please refer to [ZK Developer%27s
Reference/MVC/Controller/Wire Event
Listeners](https://www.zkoss.org/wiki/ZK_Developer%27s_Reference/MVC/Controller/Wire_Event_Listeners)).
In a event listener, you can access book model with Spreadsheet provided
API or use your service classes to implement business logic.

A typical sample of defining an event listener is like:

{% highlight java linenos %}
public class EventsComposer extends SelectorComposer<Component>{
    //other codes...

    @Listen("onCellFocus= #ss")
    public void myEventListener(CellEvent event){
        //access book model or perform your business logic
    }
}
{% endhighlight %}

  - Line 4: In `@Listen`, "onCellFocus" is the event name we want to
    listen (All event name can be found in `io.keikai.ui.event.Events`)
    and "\#ss" is the component selector. (`SelectorComposer` supports
    various selector syntax that let you select components easily.
    Please refer to [ZK Developer's Reference/MVC/Controller/Wire
    Components](ZK_Developer's_Reference/MVC/Controller/Wire_Components "wikilink"))
    .
  - Line 5: The argument passed into a event listener depends on the
    event it listens. You can get event related data like row or column
    for further processing.

All Keikai events you can listen are listed in `io.keikai.ui.event.Events`
