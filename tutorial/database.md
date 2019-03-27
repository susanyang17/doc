---
title: Work with a Database
toc: false
---


In addition to importing & exporting xlsx files, with Keikai you can populate data from database and save it back.

In the Budget Summary Application Demo of tutorial project, we demonstrated a simple idea to work with a database. Keikai allows you to use any preferred database, but you need to implement a persistence layer to communicate with your database by yourself. Then retrieve or save data via the persistence layer.

Take Budget Summary Application Demo as an example, there are several classes:

* `AppServlet`: Works as a controller, handles HTTP requests. It calls `MyApp` to achieve business function.
* `MyApp`: Service layer. Implements application logic with Keikai Java client API. It relies on `SampleDataDao` to communicate (query/save) with the database.
* `SampleDataDao`: Persistence layer. Connects to a HSQL database with JDBC. This DAO (Data Access Object) class is responsible for query and save expense data into the database. 


![]({{ site.baseurl }}/assets/images/tutorial/with-database.png){: .align-center}

From this simple architecture, it is pretty clear that communicating with a database is independent of Keikai Java client. Therefore, you can implement the database connection in your preferred way.
