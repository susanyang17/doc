\_\_TOC\_\_

# MVC in Brief

ZK framework supports the MVC design pattern to develop a web
application. This pattern separates an application into 3 parts:
*Model*, *View*, and *Controller*. The Model is the data that an
application handles. The View is UI which indicates a ZUL page in a
ZK-based application. The Controller handles events from UI, controls
the UI, and accesses the Model. For complete explanation, please refer
to [ZK Developer%27s
Reference/MVC](ZK_Developer%27s_Reference/MVC "wikilink").

# Spreadsheet Properties

Each component is represented by a unique tag name, e.g. Spreadsheet is
<spreadsheet> in a ZUL page. The easiest way to control a component is
to set a component's properties via a tag's attribute. Each property has
its own effect, and you can change it by specifying values in a tag's
attribute.

## Excel File Path

The simplest way to load and display an Excel book file is setting
Spreadsheet's `src` attribute to the file path which is a relative URI
with respect to the web application root.

``` xml

<spreadsheet src="/TestFile2007.xlsx" .../>
```

  - In this case, TestFile2007.xlsx is under the web application's root
    folder.

Some UI part's visibility is configurable like toolbar, formula bar,
sheet bar, and context menu.

## Toolbar

The `showToolbar` attribute controls toolbar's visibility, and it only
accepts boolean literal.

Default: `false`

``` xml

    <spreadsheet showToolbar="true"/>
```

## Formula Bar

The `showToolbar` attribute controls formula bar's visibility, and it
only accepts boolean literal.

Default: `false`

``` xml

    <spreadsheet showFormulabar="true"/>
```

## Sheet Bar

The `showSheetbar` attribute controls sheet bar's visibility, and it
only accepts boolean literal.

Default: `false`

``` xml

    <spreadsheet showSheetbar="true"/>
```

## Context Menu

The `showToolbar` attribute controls context menu's visibility, and it
only accepts boolean literal.

Default: `false`

``` xml

    <spreadsheet showContextMenu="true"/>
```

## Selection Visiblility

<http://tracker.zkoss.org/browse/ZSS-1044-->\>

` Since 3.8.1`

Default: `true`

When it's `true`, ZSS keeps the selection area visible after opening a
dialog like "Format Cell". Specify `false` to remove this behavior.

``` xml
<spreadsheet keepCellSelection="false"  .../>
```

If you want to change the default value to `false`; you can do that by
setting the library property *org.zkoss.zss.ui.keepCellSelection* to
`false`[1](http://books.zkoss.org/wiki/ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Configuration#Keep_Cell_Selection)
<http://books.zkoss.org/wiki/ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Configuration#Keep_Cell_Selection>\]

## Preloaded Column / Row Size

In order to speed up rendering cells, keikai spreadsheet caches a range of
cell data at client-side to avoid getting data from the server-side when
scrolling. You can adjust this range by `preloadColumnSize` (default:
40) and `preloadRowSize` (default: 60) like:

``` xml
<spreadsheet preloadColumnSize="50" preloadRowSize="50"/>
```

If you specify a larger size, it will make a more smooth scrolling when
moving to adjacent cells. On the other hand, when you reach out of the
cached range, ZSS takes more time to get the cached data from a server.

### Pasting Lots of Cells Requires Larger Preloaded Size

If you paste lots of cell from Excel which is over cached cell range,
ZSS will fail to handle the pasting because of lack of corresponding
cached cell data at the client-side (you should see an error message in
the developer tool / Console tab). In such case, you need to increase
preloaded row/column size according to the expected row/column size for
copying.

### Underlying Details

There are 3 ranges behind the scene:

1.  **visible range**: the viewport that shows a sheet. By default is 40
    column \* 50 rows. It changes if resize a browser window, or
    scrolling, etc.

<!-- end list -->

1.  **rendered range**: the range with rendered DOM of cells.
    Spreadsheet could also render hidden rows if the next visible row is
    within the range, e.g. if row 25th\~30th are hidden, but row 31th is
    in the range, then Spreadsheet still renders row 25th\~30th.
2.  **cached range**: the browser cached cell data.

When the visible range moves by user scrolling, ZSS renders DOM of cells
from the cached. So the rendered range becomes larger. If the cache does
not cover the whole visible range, ZSS will send AU request
(`onZssFetchActiveRange`) to get the data back to the cache.

![ center](3Ranges.png " center")

## MaxRenderedCellSize

It's a threshold to remove cached cell data when scrolling. When you
scroll toward one direction, Spreadsheet will remove cached cell data in
reversed direction. For example, if you scroll toward right (east), it
will remove those cached cells data of the left (west) which are over
the `MaxRenderedCellSize` inside the "cached range" but outside the
"visible range".

## Max Visible Rows and Columns

The attribute `maxVisibleColumns` controls the maximum visible number of
columns in Spreadsheet. The minimal value of the attribute must be
larger than 0. For example, if you set it to 40, it will allow showing
only column `A` to column `AN`.

*(Since 3.8.1)* If you set this attribute to 0 or just do not set it, ZK
Spreadsheet will detect the sheet content and show as more columns as
needed. However, it will show at least 40 columns if you have a smaller
sheet.

Similarly, the attribute `maxVisibleRows` controls the maximum visible
number of rows in Spreadsheet. You can use above 2 attributes to set up
the visible area according to your requirement.

*(Since 3.8.1)* If you set this attribute to 0 or just do not set it, ZK
Spreadsheet will detect the sheet content and show as more rows as
needed. However, it will show at least 200 rows if you have a smaller
sheet.

**Usage:**

``` xml
    <spreadsheet maxVisibleRows="200" maxVisibleColumns="40"/>
```

## Other Inherited Properties

There are other properties inherited from parent component you can set,
such as `width`, or `height`. For the complete list, please look for
those inherited setter methods in the javadoc
<javadoc directory="zss">org.zkoss.zss.ui.Spreadsheet</javadoc>.

Each **setter** means a corresponding **attribute**, for example:

  - `setWidth()`

<!-- end list -->

``` xml
<spreadsheet width="100%">
```

  - `setHeight()`

<!-- end list -->

``` xml
<spreadsheet height="100%">
```

# Controller

After we create a ZUL page, we can apply a Controller to handle events
and control components of the page. In ZK, the simplest way to create a
Controller is to create a class that extends
<javadoc>org.zkoss.zk.ui.select.SelectorComposer</javadoc>. ( For
details, please refer to [ZK Developer%27s
Reference/MVC/Controller](ZK_Developer%27s_Reference/MVC/Controller "wikilink")).

**Controller example**

``` java
public class MyComposer extends SelectorComposer<Component> {
    //omitted codes...
}
```

Then we can apply this controller to a root component of a ZUL page.

**index.zul**

``` xml
    <window title="My First keikai spreadsheet Application" 
    apply="org.zkoss.zss.essential.MyComposer"
        border="normal" height="100%" width="100%">
        <spreadsheet id="ss"src="/WEB-INF/books/startzss.xlsx"
                height="100%"width="100%"
        maxVisibleRows="150" maxVisibleColumns="40"
         showToolbar="true" showSheetbar="true" showFormulabar="true"/>
    </window>
```

  - Line 2: We usually apply a controller on the root component (the
    outermost component) of a ZUL page so that we can gain control of
    all components in a page.
  - Line 4: The component's id, `ss`, can be used as a criteria in
    component selector to get Spreadsheet object in a controller and we
    will describe it in next section.

## Access Components on a ZUL Page

After applying a controller, we can easily get a component object on the
zul with the help of SelectorComposer and manipulate the component to
fulfill our business requirement.

Steps to get a component:

1.  Declare a member variable with the same type as the component you
    want to get.
2.  Apply the annotation `@Wire` with component selector syntax which
    specifies matching criteria against the components of the page which
    is applied with this controller.

When a ZUL page is applied with a controller, ZK will *wire*
corresponding components object to those variables annotated with
`@Wire` according to component selector.

If you want to initialize components in a Controller, you should
override `doAfterCompose()`. For complete explanation, please refer to
[ZK Developer%27s Reference/MVC/Controller/Wire
Components](ZK_Developer%27s_Reference/MVC/Controller/Wire_Components "wikilink").

Let's see an example to get Spreadsheet component in index.zul:

**@Wire usage**

``` java
public class MyComposer extends SelectorComposer<Component> {

    @Wire
    Spreadsheet ss;
    
    @Override
    public void doAfterCompose(Component comp) throws Exception {
        super.doAfterCompose(comp);  //wire variables and event listeners
        //access components after calling super.doAfterCompose()
    }

}
```

  - Line 3,4: If you specify nothing in `@Wire`, ZK will use the
    variable name as a component's id to look for matching component in
    the ZUL page. In our case, ZK will try to find a Spreadsheet
    component whose id is `ss` in index.zul.
  - Line 7: Override this method to write initializing codes in it.
  - Line 8: Remember to call `super.doAfterCompose()` before you
    accessing components because parent class wires components for you.

## Set Spreadsheet Properties by API

After we retrieve a reference to a component, we can use its API to
manipulate a component. The basic usage is to set (or get) a component's
properties. Each Spreadsheet's property listed in previous section has a
corresponding getter and setter. For example, there are
`setShowToolbar()` and `isShowToolbar()` corresponding to attribute
`showToolbar`. You can read Javadoc for complete list of getter and
setter.

**Setter usage**

``` java
public class MyComposer extends SelectorComposer<Component> {

    @Wire
    Spreadsheet ss;
    
    @Override
    public void doAfterCompose(Component comp) throws Exception {
        super.doAfterCompose(comp);  //wire variables and event listeners
        //access components after calling super.doAfterCompose()
        if (isConditionOne()){
            ss.setShowToolbar(true);
            ss.setSrc("/books/firstFile.xlsx");
        }
    }

}
```

  - Line 11,12: Using API allows you to set a component dynamically upon
    different conditions.

## Handling Events

In most scenarios, the controller is usually used to listen to
interested events of Spreadsheet and implement business logic to react
the events. When a user interacts with a Spreadsheet, it will send
various events according to user actions. Please refer to [ Handling
Events](ZK_Spreadsheet_Essentials_3/Working_with_Spreadsheet/Handling_Events "wikilink")
on how to listen events in a controller. To implement business logic,
you definitely will need to access Spreadsheet data model. Refer to
sections under [ Handling Data
Model](ZK_Spreadsheet_Essentials_3/Working_with_Spreadsheet/Handling_Data_Model "wikilink")
to know how to use it.
