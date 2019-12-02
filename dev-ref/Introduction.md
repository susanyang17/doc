\_\_TOC\_\_

# Overview

keikai spreadsheet is an AJAX component that delivers Excel-like experience
for your Java web application. It has a grid-like user interface with
toolbar, formula bar, and sheet bar and it provides necessary features
such as editing text and styles, merging, sorting cells and inserting,
deleting, and freezing rows and columns. Spreadsheet not only supports
over 75% of Excel formulas and you can even add your own ones. Some
handy features like "auto fill", "auto filter", and protection are also
included in Spreadsheet.

Being able to import and export Excel files are just the top of the
features iceberg. Unlike other online spreadsheet such as Google Docs or
Microsoft Office 2010 online suite, you can integrate keikai spreadsheet
with your enterprise back-end systems seamlessly and create
collaborative and dynamic enterprise applications at minimal cost. You
can call versatile Java APIs to control and configure the keikai spreadsheet
component(s). You can register event listeners so an action can be
automatically triggered if any specified cell, range, or name changes.
You can make cells reference to the backend Java beans, so any changes
on the backend data can automatically reflect on keikai spreadsheet. You can
create your own customized formulas in Java and use them in the
spreadsheet like other built-in formulas. You can even create an online
spreadsheet service with keikai spreadsheet component.

keikai spreadsheet is an extensible, customizable, and integrable Java AJAX
web spreadsheet solution, with both built-in browser AJAX user interface
and back-end server side Excel-like data and logic. No ActiveX or other
plug-ins are required.

# Architecture

**Overview** ![ center](essentials-app-architecture.png " center")

**More Inner Details** ![ center | 900px](essentials-architecture.png
" center | 900px")

keikai spreadsheet component consists of three major parts -- the
client-side UI , the server-side component, and the book data model with
the formula evaluation engine. The UI is a grid like widget that you can
in-place edit the content of each cell. The component is a server-side
instance which your controller usually works with. The data model stores
the actual Spreadsheet data. The formula evaluation engine is
responsible for formula parsing and calculations.

# Using in JSP or JSF

You can use Spreadsheet in JSP with custom tag library and interact with
it by writing Javascript. Please refer to [ Using Spreadsheet in
JSP](ZK_Spreadsheet_Essentials_3/Using_Spreadsheet_in_JSP "wikilink")
for details. For JSF, we provides a Spreadsheet JSF component which can
be used within a JSF page and interact with other components by AJAX
tag. Please refer to [ Using Spreadsheet in
JSF](ZK_Spreadsheet_Essentials_3/Using_Spreadsheet_in_JSF "wikilink")
for details.

# Difference from 2.5.0

In 3.0.0, we have made some significant changes including new APIs for
accessing book model, event name change, and the new way to customize
toolbar handling. For complete details, please refer to
<http://books.zkoss.org/wiki/Small_Talks/2013/August/ZK_Spreadsheet_3.0.0_RC:Upgrade_Notes>.

# Difference from 3.0.0

In 3.5.0, we introduce a brand new model implementation. This
enhancement doesn't change the way you use the Spreadsheet's public API
mostly, but reduces Spreadsheet's memory consumption. Also we have
established a new theme mechanism that you can design your own theme
with CSS and change it dynamically. We have as well designed a new
Skyline theme as the default theme for the version 3.5. There are other
enhancements; please refer to
<http://books.zkoss.org/wiki/Small_Talks/2014/July/New_Features_of_ZK_Spreadsheet_3.5.0>
for details.

# Supported Browsers

For the best user experience, we recommend using one of the following
browsers: Internet Explorer 9 and higher, latest version of FF, Chrome,
or Safari

# Next Step

You can <http://zssdemo.zkoss.org/zssdemo> or [ get Spreadsheet running
at your local
site](ZK_Spreadsheet_Essentials/Using_Spreadsheet_in_ZK/Get_Spreadsheet_Up_and_Running_Quickly "wikilink").
