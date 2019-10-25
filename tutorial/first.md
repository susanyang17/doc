---
title: 'Create First Keikai'
toc: false
---


Keikai bases on [ZK UI framework](http://www.zkoss.org), and it provide [a powerful, XML format UI language](https://www.zkoss.org/wiki/ZK_Developer%27s_Reference/UI_Composing/ZUML). You can easily creae a Keikai by an XML tag. So we start from a simple zul:

**editor.zul**
```xml
<spreadsheet width="100%" height="100%"
            showToolbar="true" showFormulabar="true" 
            showSheetbar="true" showContextMenu="true"
            src="/WEB-INF/books/demo_sample.xlsx"/>
```

You can specify different path in `src` attribute to load your file into Keikai.

Then visit the page URL (http://localhost:8080/tutorial/editor.zul) with your browser. You will see a spreadsheet loaded the specified xlsx file with toolbar, formula bar, sheet bar and content menu.


![](/assets/images/tutorial/keikaiUi.png)

1. Toolbar
2. Formula bar
3. Current Sheet
4. Context menu
5. Sheet bar