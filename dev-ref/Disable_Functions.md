Spreadsheet provides API to disable its functions. The API can be very
useful when you implement your user permission features. In the example
application below, since we disable all sheet related functions except
one, you can see the corresponding menu items are disabled (in grey
color). ![ center](zss-essentials-disableFunctions.png " center")

To achieve this, simply call
<javadoc directory='zss' method="disableUserAction(org.zkoss.zss.ui.AuxAction, boolean)">org.zkoss.zss.ui.Spreadsheet</javadoc>

``` java
package org.zkoss.zss.essential.advanced.customization;

import org.zkoss.zk.ui.Component;
import org.zkoss.zk.ui.event.CheckEvent;
import org.zkoss.zk.ui.select.SelectorComposer;
import org.zkoss.zk.ui.select.annotation.*;
import org.zkoss.zss.ui.*;

/**
 * This class demonstrates how to disable functions.
 * @author Hawk
 *
 */
@SuppressWarnings("serial")
public class DisableFunctionsComposer extends SelectorComposer<Component> {

    @Wire
    private Spreadsheet ss;
    
    @Listen("onCheck = #add")
    public void disableAdd(CheckEvent event) {
        ss.disableUserAction(AuxAction.ADD_SHEET, !event.isChecked());
    }
...
}
```

Except sheet operations, you can also disable functions on the toolbar
and the context menu. Take a look at
<javadoc directory='zss'>org.zkoss.zss.ui.AuxAction</javadoc> for a
complete list of functions you can disable.
