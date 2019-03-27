---
title: Run Your First Keikai Application
toc: false
---

Now that the Keikai engine is up and running, we can run tutorial project. After extracting Keikai engine, there should be a folder `keikai-tutorial` which is a clone from [Keikai tutorial project](https://github.com/keikai/keikai-tutorial). There are several demos in the tutorial project.

You can run this project on a built-in jetty server with Maven wrapper without installing anything in advance (the wrapper will download and install required files for you). Just run the following command in your command line interface:

##  Linux / Mac

### Maven wrapper
`./mvnw jetty:run-forked`


## Window

### Maven wrapper
`mvnw.cmd jetty:run-forked`

Then visit [http://localhost:8080](http://localhost:8080)