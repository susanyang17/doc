---
title: 'Online Editor'
toc: false
---


First we talk about displaying a Keikai spreadsheet in your browser.
Keikai is based on [ZK UI framework](http://www.zkoss.org), and it provide [a powerful, XML format UI language](https://www.zkoss.org/wiki/ZK_Developer%27s_Reference/UI_Composing/ZUML). You can easily create a Keikai spreadsheet by the <spreadsheet> XML tag. So we start from a simple zul:

**editor.zul**
```xml
<spreadsheet width="100%" height="100%"
            showToolbar="true" showFormulabar="true" 
            showSheetbar="true" showContextMenu="true"
            src="/WEB-INF/books/demo_sample.xlsx"/>
```

Here we load an Excel file "demo_sample.xlsx" programmatically by specifying the `src` attribute. 

Then visit the page URL (http://localhost:8080/tutorial/editor.zul) with your browser. You will see the specified xlsx file loaded with toolbar, formula bar, sheet bar and context menu.


![](/assets/images/tutorial/keikaiUi.png)

1. Toolbar
2. Formula bar
3. Current Sheet
4. Context menu
5. Sheet bar

Keikai has a familiar spreadsheet UI interface, end users can edit the spreadsheet like changing cell content, font, color, format, formulas, ... in the way they already know.
