---
title: Run Your First Keikai Application
toc: false
---

Now that the Keikai engine is up and running, we can run tutorial project. After extracting Keikai engine, there should be a folder `keikai-tutorial` which is a clone from [Keikai tutorial project](https://github.com/keikai/keikai-tutorial). There are several demos in the tutorial project.

We have packaged this project containing a built-in jetty server with Maven wrapper so that you can run it without having to install anything in advance (the wrapper will download and install required files for you, so be sure that you are connected to the internet). 

Just switch to the keikai-tutorial folder and run the following command in your command line interface:

##  Linux / Mac

`./mvnw jetty:run-forked`


## Window

`mvnw.cmd jetty:run-forked`

After it finishes, visit [http://localhost:8080/tutorial/](http://localhost:8080/tutorial/) with your browser.

(You can press `Ctrl+c` to stop the jetty.)
