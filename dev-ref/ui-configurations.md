---
title: "Component UI Configurations"
toc: false
---


Keikai UI has several parts:

![](/assets/images/tutorial/UI.png)


# Configure by Data Attributes

Their visibility are configurable through data attributes:

* `data-show-context-menu`
* `data-show-toolbar`
* `data-show-sheet-tabs`
* `data-show-formula-bar`
* `data-show-sheet-controls`

For example, to hide built-in context menu:

```xml
<div id="spreadsheet" data-show-context-menu="false"/>
```



# Configure by API

```java
spreadsheet.getUIService().showToolbar(false);
```

Check [UIService](https://keikai.io/javadoc/latest/io/keikai/client/api/UIService.html) for full method lists.


# Hide Protected Sheet Warning

`spreadsheet.getUIService().setProtectedSheetWarningEnabled(false);`
