---
title: "Download and Installation"
---

Before using Keikai, you need to install and start Keikai engine. 

# Download Keikai engine

* [Windows 64-bit](https://keikai.io/download/?dl=JHSxw%2FX9s3wAuWyq6%2Bmw4Q%3D%3D%3A0FQRpIhVVPppGO9vG671GehNe1yTcwxarCA99Q%2B83dEAwyWY4%2FonBzqKiAIAhs4r)

* [Linux 64-bit](https://keikai.io/download/?dl=pMI%2BjAR4PXdQWWiCdBtUYg%3D%3D%3ATkQt2WMxQcErY8bN1ktPM69YduxD9wZt8mGdJVLuRFQI6yTij33s3DdWSp1vJDyZ)

* [Mac OS 64-bit](https://keikai.io/download/?dl=%2FEh7vutQMg8o0Amrlg9STA%3D%3D%3AY5IPQ%2FuSliTsxC8ezw%2F%2FqsecJf0bYtTpFG7udz34lshXwgd3rvX8C66%2B8d0dRrIP)

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