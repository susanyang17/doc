---
title: Customize Toolbar
---

# Hide Toolbar
Keikai spreadsheet UI is customizable. In some cases, you may need only the data grid without letting the user use the toolbar, just like the Budget Summary Application Demo in the tutorial project. You can simply hide the entire toolbar with a data attribute specified on the anchor element:

**app.jsp**

`<div id="spreadsheet" data-show-toolbar="false" >`

# Hide Buttons
If you wish to hide some of the buttons on the toolbar, you need to provide a different `Settings` when getting `Spreadsheet`.

**MyEditor.java**

`spreadsheet = Keikai.newClient(keikaiServerAddress, getSettings());`

Then override the toolbar configuration in `Settings` with :

**MyEditor.java**

```java
    protected Settings getSettings() {
        Settings settings = Settings.DEFAULT_SETTINGS.clone();
        String customToolbarConfig = "{\"items\": \"upload,newBook,exportToFile|" +
                "paste,cut,copy|" +
                "fontName,fontSize,fontItalic,fontBold,fontUnderline,fontStrike," +
                "fontColor,border,fillColor|" +
                "verticalAlign,horizontalAlign,wrapText,mergeAndCenter|" +
                "numberFormat|" +
                "insert,delete|" +
                "clear,sortAndFilter|" +
                "gridlines,protectSheet|" +
                "freeze,hyperlink\"}";
        settings.set(Settings.Key.SPREADSHEET_CONFIG, Maps.toMap("toolbar", customToolbarConfig));
        return settings;
    }
```

Toolbar config is a JSON format string. In the Online Editor Demo of the tutorial project, we hide "Save Book" button by removing `saveBook` from the string.