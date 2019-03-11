---
title: "Component UI Customization"
---


Keikai UI is configurable through a data attribute:

![](/assets/images/keikaiUI.png)

* `data-show-context-menu`
* `data-show-toolbar`
* `data-show-sheet-tabs`
* `data-show-formula-bar`
* `data-show-sheet-controls`

For example, to hide built-in context menu:

```xml
<div id="spreadsheet" data-show-context-menu="false"/>
```