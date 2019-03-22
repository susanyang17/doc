---
title: "Download and Installation"
---

Before using Keikai, you need to install and start Keikai engine. 

# [Download Keikai Engine](keikai.io/download)

[Contact us](https://keikai.io/#contact) if you have problems to download.


# Extract the zip
We suggest you extract Keikai engine on the same machine as your application server at first to avoid problems. Later, you can move it to another place.

Just unzip the downloaded zip file, you complete the installation.


# Run Keikai Engine
Assume you extract the zip to a folder `[KEIKAI-ENGINE]`
1. go to `[KEIKAI-ENGINE]/keikai` folder
2. run the executable command:

* Mac/Linux

`./keikai`

* Windows

`keikai.bat`

After executing the command, you should see some messages like:
```
1:8888:2018-06-05 09:52:18.059549Z:keikai_dart_server:keikai_server:0
INFO: Keikai version: 1.0.0-beta@jhsioate
...
INFO: Rikulo Stream Server 1.7.0 starting on 0.0.0.0:8888
...
```

Then Keikai server should start up successfully at `localhost:8888