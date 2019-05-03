---
title: "Component UI Configurations"
toc: false
---


Keikai UI is configurable through a data attribute:

![](/assets/images/tutorial/UI.png)

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
