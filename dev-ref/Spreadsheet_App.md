# Overview

keikai spreadsheet App is a web-based Excel like application based on the ZK
Spreadsheet component. We created it to demonstrate Spreadsheet's
numerous powerful features. You can also use this application as a basis
of your application and add more functions like authentication.

Please follow these steps to run this application:

1.  Download keikai spreadsheet App from
    <http://www.zkoss.org/download/zkspreadsheet> (OSE or EE
    evaluation).
2.  Unzip the zip file and deploy the Spreadsheet App's WAR file to your
    application server according to its instruction.
      -   
        For Tomcat just put the war file in `[CATALINA_HOME]\webapps`.
3.  Start your application server and connect it with your browser.
      -   
        For Tomcat, just visit <http://localhost:8080/zssapp>
        <http://localhost:8080/zssapp> then you can start to experience
        the power of Spreadsheet App.

After you visit Spreadsheet App, you should see its user interface like
the screenshot below: ![ center](zss-essentials-zssapp.png " center")

You might notice that we add a menu on top of Spreadsheet component and
3 leftmost buttons ("New Book", "Save Book", and "Export to PDF") on the
toolbar are enabled because we have implemented them in keikai spreadsheet
App.

# Features

Here we will focus on those features which we create specially for
Spreadsheet App. For the Spreadsheet component's features, please refer
to [ Features and
Usage](ZK_Spreadsheet_Essentials_3/Features_and_Usage "wikilink").

## File Menu

The "File" menu contains many file operations including load, save, and
export. ![ center](zss-essentials-zssapp-file.png " center")

Each menu item and its function description are:

<table>
<thead>
<tr class="header">
<th><center>
<p>Menu Item</p>
</center></th>
<th><center>
<p>Description</p>
</center></th>
<th><center>
<p>EE Only</p>
</center></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>create a book with 2 blank sheets which equals to click <img src="zss-essentials-zssapp-newBook.png" title="fig:zss-essentials-zssapp-newBook.png" alt="zss-essentials-zssapp-newBook.png" /> on the toolbar</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Open or Manage Books</p></td>
<td><p>open a book list dialog that allows you to open, delete, and upload a file.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Save</p></td>
<td><p>save current book which equals to click <img src="zss-essentials-zssapp-saveBook.png" title="fig:zss-essentials-zssapp-saveBook.png" alt="zss-essentials-zssapp-saveBook.png" /> on the toolbar</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Save As</p></td>
<td><p>save current book as another file</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Save &amp; Close</p></td>
<td><p>save current book then close it</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Close</p></td>
<td><p>close current book</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Export</p></td>
<td><p>export current book as an Excel file</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Export PDF</p></td>
<td><p>export current book as a PDF file which equals to click <img src="zss-essentials-zssapp-exportPdf.png" title="fig:zss-essentials-zssapp-exportPdf.png" alt="zss-essentials-zssapp-exportPdf.png" /> on the toolbar</p></td>
<td><p>yes</p></td>
</tr>
</tbody>
</table>

When you select "Open or Manage Books", the dialog below appears and you
can open, delete, or upload a book. ![
center](zss-essentials-zssapp-file-booklist.png " center")

## Edit Menu

The "Edit" menu has "Undo" and "Redo" item and they also display
corresponding action they will perform when you click on them. ![
center](zss-essentials-zssapp-edit.png " center")

Each menu item and its function description are:

<table>
<thead>
<tr class="header">
<th><center>
<p>Menu Item</p>
</center></th>
<th><center>
<p>Description</p>
</center></th>
<th><center>
<p>EE Only</p>
</center></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Undo</p></td>
<td><p>erase the last change you made</p></td>
<td><p>yes</p></td>
</tr>
<tr class="even">
<td><p>Redo</p></td>
<td><p>revert the effects of the undo action</p></td>
<td><p>yes</p></td>
</tr>
</tbody>
</table>

## View Menu

The "View" menu can change view effects of current sheet. ![
center](zss-essentials-zssapp-view.png " center")

Each menu item and its function description are:

<table>
<thead>
<tr class="header">
<th><center>
<p>Menu Item</p>
</center></th>
<th><center>
<p>Description</p>
</center></th>
<th><center>
<p>EE Only</p>
</center></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Formula Bar</p></td>
<td><p>control visibility of the formula bar</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Freeze Rows &amp; Columns</p></td>
<td><p>freeze rows and columns according to current selection. It freezes the rows above and the columns left to the current selected cell.</p></td>
<td><p>yes</p></td>
</tr>
<tr class="odd">
<td><p>Unfreeze Rows &amp; Columns</p></td>
<td><p>unfreeze rows and columns</p></td>
<td><p>yes</p></td>
</tr>
<tr class="even">
<td><p>Freeze Row</p></td>
<td><p>shortcut menu to freeze row 1 to row 5</p></td>
<td><p>yes</p></td>
</tr>
<tr class="odd">
<td><p>Freeze Col</p></td>
<td><p>shortcut menu to freeze column A to column E</p></td>
<td><p>yes</p></td>
</tr>
</tbody>
</table>

The screenshot below shows a result after selecting "Freeze Rows &
Columns" when selection box stays in B2. It freezes the row above and
the column left to current selection: ![
center](zss-essentials-zssapp-freeze.png " center")

# Configuration

## Repository Root

You can assign your own folder as the drive storage via system property.

``` xml
zssapp.repository.root
```

For example, in Tomcat server, we can assign the following value into
TOMCAT\_HOME/conf/catalina.properties. In this case, Cloud Drive folder
will be changed into C:\\zssapp\\books.

``` xml
zssapp.repository.root=C:\\zssapp\\books
```

## Auto Save

`Since 3.8.0`

App supports auto save, and it is triggered in the following cases:

1.  Users changes a file content, and time period specified expires.
2.  Last editing user for the book leaves, e.g. open another book or
    close the browser.
3.  When server shuts down normally.

By default, we save all changes for you every 15 minutes, but you can
change this period via configuration. Following example configures the
period with 5 minutes.

**Example in zk.xml**

``` xml
<library-property>
    <name>zssapp.save.period.second</name>
    <value>300</value>
</library-property>
```
