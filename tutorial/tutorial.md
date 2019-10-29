---
title: 'Keikai Tutorial'
permalink: /tutorial
---

# Overview
 [Keikai](https://keikai.io/) is an embeddable Java Web spreadsheet component that delivers Excel-like functionalities to your Web application. It has an UI similar to Excel including a main sheet canvas, a toolbar, a formula bar, and sheet tabs and provides commonly used features such as editing text and styles, merging and sorting cells; and inserting, deleting, and freezing rows and columns. In addition Keikai provides built-in Excel formulas and allows you to plugin your own functions.

You can import your xlsx file into Keikai and edit the file within your browser. You can also populate data from your database or data source to Keikai and save it back to DB after editing. You can call versatile Java APIs to control and configure Keikai and seamlessly integrate it with your backend system. Besides, you can listen to events triggered by user actions like clicking a cell or selecting a sheet, and then implement your application logic in an event listener.

Keikai is the easiest way to bring in spreadsheet power to your Web applications!

# Quick Start
Just clone the [tutorial project](https://github.com/keikai/keikai-tutorial) and follow the instructions in readme.md to start up the project with Jetty. Then you can start to experience Keikai in your browser.
We take the tutorial project to introduce the most common use cases: [Online Editor](https://docs.keikai.io/tutorial/editor) and [Work with Database](https://docs.keikai.io/tutorial/database).

# Setup with Maven
If you wish to create your own Maven project instead of using the tutorial project, add the following repository:

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
