---
title: 'Keikai Tutorial'
permalink: /tutorial
---

# Overview
 [Keikai](https://keikai.io/) is an extensible, customizable, and integrable Java AJAX web spreadsheet component that delivers Excel-like experience for your Java web application. It has UI similar to Excel including a toolbar, formula bar, and sheet tabs and provides mostly-common features such as editing text and styles, merging, sorting cells and inserting, deleting, and freezing rows and columns. Keikai not only supports over 75% of Excel formulas and you can even add your own ones. 

You can import your xlsx file into Keikai and edit the file with your browser. Unlike other online spreadsheet such as Google Sheets or Microsoft Office online, you can integrate Keikai with your enterprise back-end systems seamlessly and create collaborative and dynamic enterprise applications at minimal cost. You can call versatile Java APIs to control and configure Keikai. Besides, you can listen to events triggered by user actions like clicking a cell, or selecting a sheet, then implement your application logic in an event listener. 

This tutorial introduce you how to use Keikai with several basic examples including setup and API usage.

# Quick Start
Just clone [tutorial project](https://github.com/keikai/keikai-tutorial) and follow the instructions in readme.md to start up the project with jetty. Then you can start to experience Keikai with your browser.


# Setup with Maven
If you want to create your own Maven project, you need to add the repository:

```xml
<repository>
    <id>CE</id>
    <name>CE</name>
    <url>http://mavensync.zkoss.org/maven2</url>
</repository>
```

Include the artifact below:

```xml
<dependency>
    <groupId>io.keikai</groupId>
    <artifactId>keikai-oss</artifactId>
    <version>${keikai.version}</version>
</dependency>
```