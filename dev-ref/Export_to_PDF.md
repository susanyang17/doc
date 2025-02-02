\_\_TOC\_\_

# PDF Exporter

In addition to the Excel format, you can also export a book model as a
PDF file with
<javadoc directory="keikai">io.keikai.api.Exporter</javadoc>

**Example to export as a PDF**

``` java
package io.keikai.essential;

import java.io.*;

import org.zkoss.util.media.AMedia;
import org.zkoss.zk.ui.Component;
import org.zkoss.zk.ui.select.SelectorComposer;
import org.zkoss.zk.ui.select.annotation.*;
import io.keikai.api.*;
import io.keikai.api.model.Book;
import io.keikai.ui.Spreadsheet;
import org.zkoss.zul.*;

public class ExportPdfComposer extends SelectorComposer<Component> {

    @Wire
    private Spreadsheet ss;
    @Wire("combobox")
    private Combobox combobox;

    Exporter exporter = Exporters.getExporter("pdf");
    
    
    @Listen("onClick = #exportPdf")
    public void doExport() throws IOException{
        Book book = ss.getBook();
        
        File file = File.createTempFile(Long.toString(System.currentTimeMillis()),"temp");
        FileOutputStream fos = null;
        try {
            fos = new FileOutputStream(file);
            exporter.export(book, file);
        }finally{
            if(fos!=null){
                fos.close();
            }
        }
        Filedownload.save(new AMedia(book.getBookName()+".pdf", "pdf", "application/pdf", file, true));
    }

    //omit some code for brevity
}
```

Line 21: Get an Exporter instance for PDF format.

# Export Server Setup

`Since 3.7.0`

Since 3.7.0, the default chart engine has become ZK Charts. With this
engine, exporting spreadsheets that include charts to PDF needs extra
export server chart data rendering at the server side. The easiest way
is to adopt Highcharts official solution which is based on PhantomJS, a
headless Webkit browser.

1.  download and install PhantomJS at
    <http://phantomjs.org/download.html>.
    <http://phantomjs.org/download.html>.
2.  download Highcharts project at <http://www.highcharts.com/download>.
    <http://www.highcharts.com/download>.
    1.  in this project, go to exporting-server -\> phantomjs
3.  start export server by commanding "phantomjs highcharts-convert.js
    -host 127.0.0.1 -port 3003"
    1.  you should move the PhantomJS executable file into this folder
        1.  On Windows, the full name is phantomjs.exe
        2.  On Mac or Linux, the full name is phantomjs
    2.  you can customize host and port respectively by parameter -host
        and -port
4.  add properties into zk.xml
    1.  there are three library properties to be used

**Library properties about export server**

This is the location to export server. When it doesn't find this
definition, JFreechart will be used to generate chart graphs. (Required)

``` xml
<library-property>
    <name>io.keikai.chart.render.server.url</name>
    <value>http://127.0.0.1:3003</value> http://127.0.0.1:3003</value>
</library-property>
```

Scale is a zoom factor that affects pixel density relative to the
original, for example, 2 means double the resolution of the original.
(Optional)

``` xml
<library-property>
    <name>io.keikai.chart.render.server.scale</name>
    <value>1</value>
</library-property>
```

Default timeout is 10000 milliseconds (10 seconds) for waiting response
from export server. (Optional)

``` xml
<library-property>
    <name>io.keikai.chart.render.server.timeout</name>
    <value>10000</value>
</library-property>
```

After restarting server, ZK Charts will be shown when exporting PDF.

# Load Excel Printing Setup

`Since 3.6.0`

Spreadsheet exports its book model to a PDF file according to the page
print setup you specify in Excel.

![ center](/assets/images/dev-ref/ExcelPageSetup.png " center")

For example, you can add a header and footer, and it would look like:

![ center](/assets/images/dev-ref/pdfExporting-HeaderFooter.png " center")

You can also scale a sheet to fit into one page with row and column
heading: ![ center](/assets/images/dev-ref/_pdfExporting-FitOnePage.png " center")

# Supported Page Setup

The page setup properties of Excel which are supported by Spreadsheet
are listed below:

**Page**

  - Orientation
      - Portrait, Landscape
  - Scaling
      - Adjust to % normal size
      - Fit to pages wide by tall
  - Page size
  - First page number

**Margins**

  - Top
  - Header
  - Right
  - Footer
  - Bottom
  - Left

*' Center on Page*'

  - Horizontally
  - Vertically

**Header/Footer**

  - Custom Header...
  - Custom Footer...
  - Different odd and even pages
  - Different first page

`Custom header and footer is supported since 3.8.1`

**Sheet**

  - Print area
  - Print titles
      - Rows to repeat at top
      - Columns to repeat at left
  - Print
      - Gridlines
      - Row and column headings
  - Page order
      - Down, then over
      - Over, then down
