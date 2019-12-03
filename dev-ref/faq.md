# Does ZSS support user permission control?

  -   
    We provide API for you to build your owned permission control. User
    permission feature involves authentication and authorization which
    is out of ZSS function's scope. Since ZSS cannot identify a user, it
    cannot assign a user with corresponding permissions. But you can
    easily integrate existing framework like Spring Security and
    implement your user permission features with ZSS. Please refer to
    the following sections:
      - Hide the toolbar and the context menu to prevent editing. Please
        refer to [Keikai spreadsheet Essentials/Working with
        Spreadsheet/Control
        Components](ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Control_Components "wikilink").
      - Disable available functions for different users. Please refer to
        [Keikai spreadsheet Essentials/Working with
        Spreadsheet/Advanced/Disable
        Functions](ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Advanced/Disable_Functions "wikilink").
      - Protect sheets and set available actions. Refer to
        <javadoc directory='zss' method='protectSheet(java.lang.String , boolean , boolean , boolean , boolean , boolean , boolean , boolean , boolean , boolean , boolean , boolean allowSorting, boolean , boolean , boolean , boolean )'>io.keikai.api.Range</javadoc>

You can see an example at
<http://books.zkoss.org/wiki/ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Use_Case/User_Permission>.

# How do I save the content of ZSS or even save it to a database?

To save the content of ZSS, we recommend to export it as an Excel file
instead of saving it rows by rows. It is also the way we implement the
"Save" function in zssapp. After exporting, you can save the file into a
BLOB type column of a database.

:\* How to export: [ Export to
Excel](ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Handling_Data_Model/Export_to_Excel "wikilink")

:\* Integrate custom saving process to ZSS toolbar's Save button: [
Toolbar
Customization](ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Advanced/Toolbar_Customization#Save_Book "wikilink")

# After exporting to a PDF file, the PDF shows unexpected fonts or has missing characters

There are many reasons, but we list the most possible ones:

:\* You choose a wrong encoding for some characters.

  -   
    For example, you apply "Calibri" on a Chinese character. You can
    resolve it by applying the correct font.
      - The computer of your PDF viewer software doesn't install
        corresponding fonts.
    For ZSS doesn't embed fonts into a exported PDF file, your computer
    should install the corresponding fonts to display the file
    correctly. You can test it by opening the PDF file in another
    computer or different OS. Please check installed fonts on your
    computer. Installing missing fonts can solve this problem.

The ZSS bundled iText will find fonts from the following paths. Please
check the fonts you apply are available in these paths: **Won't scan its
subdirectories**

`   c:/windows/fonts`  
`   c:/winnt/fonts`  
`   d:/windows/fonts`  
`   d:/winnt/fonts`  
`   /Library/Fonts`  
`   /System/Library/Fonts`

**Will scan its subdirectories**

`   /usr/share/X11/fonts`  
`   /usr/X/lib/X11/fonts`  
`   /usr/openwin/lib/X11/fonts    `  
`   /usr/share/fonts`  
`   /usr/X11R6/lib/X11/fonts`

Extracted from FontFactoryImp com.lowagie.text.FontFactoryImp.

:\* The server to export a PDF doesn't install corresponding fonts.

  -   
    It might happen when you export a PDF on a Linux server without
    Microsoft fonts installed. (Unbuntu should install the package
    `ttf-mscorefonts-installer`, "installer for Microsoft TrueType core
    fonts"). You will find the exported PDF's size is smaller than the
    one exported correctly. Install the corresponding fonts can solve
    this issue.

# How do I know my file can be loaded correctly by ZSS?

In general, those functions we implement with the toolbar are supported.
However, the best way is to upload your files to the
<http://www.zkoss.org/download/zkspreadsheet>. It's a ready-to-use web
application based on ZSS component. You just run the war with a Java
application server, then you can upload files via the menu, File / Open
/ Upload.

# Does ZSS support VB macro?

No. Even
<https://www.microsoft.com/en-us/microsoft-365/blog/2014/04/14/weve-updated-excel-online-whats-new-in-april-2014/>
(or
<https://social.technet.microsoft.com/Forums/office/en-US/7c46823c-2581-47a6-baac-66fb99ac3ea8>).
The macro in a file will be lost after being imported since ZSS doesn't
keep the macro information.

If you need something similar, you can port your macro to Java within a
controller to achieve the same function.

# How to validate an XLSX format Excel file

Validate it with
<https://www.microsoft.com/en-us/download/details.aspx?id=30425>.

# Run out of heap when exporting / importing a large file

You might encounter an error like `java.lang.OutOfMemoryError: Java heap
space` when exporting / importing a large file, since it consumes more
memory at that process. Please increase your JVM heap size. (You can
refer to
<https://docs.oracle.com/cd/E15523_01/web.1111/e13814/jvm_tuning.htm#PERFM164>)

# What is the maximal rows and columns ZSS supports?

  - The max column is **16384** (2^14)
  - the max row is **1048576** (2^20)

ZSS renders cells on demand instead of rendering all cells at once in a
browser, but it loads a file's whole content into the memory. So the
bigger memory your server has, the more rows and columns ZSS can load.

Even if you have sufficient memory, loading time could be an issue.
Because loading time grows linearly with cell number. Under our test
machine, loading 1 million cells with texts takes 65 seconds, loading 2
million cells takes 139 seconds and loading 4 million cells takes 315
seconds. As the cell number grows, the time could be too long to be
acceptable by users. You can measure the loading time on your machine
first.

# Does ZSS support form control like the menu in Excel, **Developer \> Form Controls**?

No. But there are several alternatives:

  - Use ZK menu.

Please refer to the menu on top of ZSS at
<http://zssdemo.zkoss.org/zssdemo/excel_like>

  - Create a custom context menu.

Please refer to
<https://www.zkoss.org/wiki/ZK_Spreadsheet_Essentials/Working_with_Spreadsheet/Advanced/Custom_Context_Menu>

  - Insert special symbols in cells to simulate a checkbox, button.

You can insert icon-like symbols in a cell, so users think that cell is
a button like below: ![ center](Zss-essentials-symbol.png " center")
Then you can determine these cells in an event listener and perform your
business logic.

  - Data validation can produce a dropdown list

Please refer to
<https://www.zkoss.org/wiki/ZK_Spreadsheet_Essentials/Features_and_Usages#Data_Validation>

  - Show a component on a cell with a popup.

![ center](Zss-essentials-popup.png " center")

# Unable to get property 'appendCell' of undefined or null reference in IE

If you visit with IE11 and see such error message in developer tool's
console. This is mostly caused by compatibility mode. Please turn it off
and reload the page again since ZK/ZSS don't support such mode.

# See Errors When Copying Massive Cells

## Request Parameter Over a Server's Limit

You might see similar errors at your server console when copying massive
cells, for example, in Tomcat:

`25-Jun-2018 12:14:26.420 INFO [http-nio-8080-exec-8]
org.apache.tomcat.util.http.Parameters.processParameters More than the
maximum number of request parameters (GET plus POST) for a single
request ([10,000]) were detected. Any parameters beyond this limit have
been ignored. To change this limit, set the maxParameterCount attribute
on the Connector.` `Note: further occurrences of this error will be
logged at DEBUG level.`

You need to increase the limit of `maxParameterCount` of
<https://tomcat.apache.org/tomcat-7.0-doc/config/http.html>.
