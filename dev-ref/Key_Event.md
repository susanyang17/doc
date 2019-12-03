# Overview

There is one key event that Keikai spreadsheet supports:

## onCtrlKey

This event is fired when a user presses a key specified in `ctrlKeys`
attribute. By default, Spreadsheet handles keys including **ctrl+z,
ctrl+y, ctrl+x, ctrl+c, ctrl+v, ctrl+b, ctrl+i, ctrl+u, and delete key**
without specifying `ctrlKeys` on <spreadsheet>.

# Event Monitor Example

![ center](zss-essentials-events-key.png " center")

In [Event
Monitor](ZK_Spreadsheet_Essentials_3/Working_with_Spreadsheet/Handling_Events/Editing_Event#Event_Monitor_Example "wikilink")
example, the messages show that ctrl+c is pressed first then ctrl+v.
Let's see how to make it:

``` java
public class EventsComposer extends SelectorComposer<Component>{
    //omitted codes...

    @Listen("onCtrlKey = #ss")
    public void onCtrlKey(KeyEvent event){
        StringBuilder info = new StringBuilder();
        
        info.append("Keys : ").append(event.getKeyCode())
            .append(", Ctrl:").append(event.isCtrlKey())
            .append(", Alt:").append(event.isAltKey())
            .append(", Shift:").append(event.isShiftKey());
        
        //display info...
    }
}
```

  - Line 4: Apply `@Listen` to listen an event with the syntax `[EVENT
    NAME] = [COMPONENT SELECTOR]`. All event name can be found in
    <javadoc directory="keikai">io.keikai.ui.event.Events</javadoc>.
    The "\#ss" is the component selector which means the component with
    id "ss" on the ZUL page. (SelectorComposer supports various selector
    syntax that let you select components easily. Please refer to [ZK
    Developer's Reference/MVC/Controller/Wire
    Components](ZK_Developer's_Reference/MVC/Controller/Wire_Components "wikilink"))
    .
  - Line 8\~12: Except knowing which key is pressed, we can also know
    that control, alt, or shift key are pressed or not via `KeyEvent`.

# Add More Shortcut Keys

If you want to add more shortcut keys to a ZSS component, remember to
append the default shortcut keys:

  -   
    `^Z^Y^X^C^V^B^I^U#del`.

For example, if you want to add a shortcut key like **ctrl+a,** you
should set `ctrlKeys` to **`^A`**`^Z^Y^X^C^V^B^I^U#del`. Thus, you can
still benefit from built-in key handling function. For syntax used at
the property `ctrlKeys`, please refer to [ZK Developer%27s Reference/UI
Patterns/Keystroke
Handling](ZK_Developer%27s_Reference/UI_Patterns/Keystroke_Handling "wikilink").
When the corresponding event listener is invoked, a
<javadoc directory="keikai">io.keikai.ui.event.KeyEvent</javadoc>
object is passed as an argument.

# Overrideing Existing Shortcut Keys

Every shortcut key has a corresponding
<javadoc directory='zss'>io.keikai.ui.UserActionHandler</javadoc> to
perform its function like <javadoc directory='zss'>
io.keikai.ui.impl.ua.CopyHandler</javadoc>. Implementing your key
event listener cannot override existing shortcut keys' function because
the listener is executed after UserActionHandler. Therefore, to override
it you need to hook up your own UserActionHandler like:

``` java
Spreadsheet ss;
//...
UserActionManager manager = ss.getUserActionManager();
manager.registerHandler(Category.KEYSTROKE.getName(), "^V", new MyCustomPasteHandler());
```

Another way is:

``` java
Spreadsheet ss;
//...
UserActionManager actionManager = ss.getUserActionManager();
actionManager.setHandler(Category.KEYSTROKE.getName(), "^V", new MyCustomPasteHandler());
```

Please refer to [
Toolbar\_Customization](ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Advanced/Toolbar_Customization "wikilink")
for how to implement a UserActionHandler and the difference between
`registerHandler()` and `setHandler()`

# Known issue

There is a known issue <http://tracker.zkoss.org/browse/ZSS-920>, when
you add spreadsheet as the child of root, you may trigger onCtrlEvent to
server once you press delete key on BODY. To solve this issue, you can
enclose spreadsheet tag by any other tags like DIV:

``` xml
<zk>
    <div>
        <spreadsheet src="/issue3/book/blank.xlsx" height="300px" width="300px" 
            showSheetbar="true" showContextMenu="true" showFormulabar="true"/>
    </div>
</zk>
```
