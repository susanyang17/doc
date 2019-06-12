# Keikai - Spreadsheet for Your Web Application
Keikai is a component that can empower your web application with spreadsheet features. With frame-based rendering and super light-weight data structure, it brings true Excel functionalities into your web application swiftly. Finally, there is a good reason for your business users to move on from Excel!

![]({{ site.baseurl }}/assets/images/tutorial/architecture.png)


**Keikai-based Web Application:** 

It's a web application developed by you that implements your business logic. It manipulates keikai spreadsheet with Keikai Java API (Java client) including get/set cell values, change formats/styles, insert/delete rows/columns/sheets, etc. The API can do all user actions.


**Keikai engine:** 

It plays 2 roles. The first role is to provide spreadsheet functions to java clients and UI clients. It contains all spreadsheet functions like formatting rules, formula engines, data validation, and all imported data, and you can invoke such power with Java API. It receives commands from java clients and renders the result in a browser, e.g. set cell values. If users input a formula, it calculates the result and renders in the browser.

The 2nd role is to forward events from a browser, your web application can listen to predefined events triggered by user actions e.g. cell clicking, selecting a sheet, end of editing, etc, then you can implement application logic in an event listener.

Keikai supports 9 UI controls, therefore you can create a button and implement the application logic on the button clicking event.

**UI client:** 

A javascript widget running in your browser, cooperates with the engine to render the spreadsheet. Respond to user actions and send events to the engine.

**Data source:** 

Keikai doesn't limit your data source. It's on your own to grab data from an Excel file, a database, or any data service. After you get the data, you can import data into Kekai with Java API.

This introductory article demonstrates how you can start up a Keikai spreadsheet and manipulate cells with Java client API to implement your application logic .


# [Demo](http://keikai.io/demo/)
A demo is worth a thousand words, you can immediately experience Kaikai with our [Demo](http://keikai.io/demo/).


# Prerequisite
To better understand this article and how tutorial project works, we assume you have basic knowledge of Java EE web components (JSP and servlet) and HTML.
