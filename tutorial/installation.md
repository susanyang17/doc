---
title: "Download and Installation"
---

Before using Keikai, you need to install and start Keikai engine. 

# Download Keikai Engine
[Download Keikai Engine](https://keikai.io/download) according to the OS of the computer you are installing Keikai Engine.

[Contact us](https://keikai.io/#contact) if you have problems to download.


# Extract the zip
For simplicity, we suggest you to install and extract Keikai engine on the same machine as the one you are running your application server. That way you can quickly get your first application up and running.

Just unzip the downloaded zip file, and the installation of Keikai engine is completed.


# Run Keikai Engine
Assume you extract the zip to a folder `[keikai-version-os-x64]`
1. launch Command Prompt and switch to `[keikai-version-os-x64]/keikai` folder
2. run the executable command:

* Mac/Linux

`./keikai`

* Windows

`keikai.bat`

After executing the command, you should see some messages like:
```
...
INFO: Keikai version: 1.0.0-beta.20@jvbp5h5y
...
INFO: Starting Keikai engine on http://localhost:8888
...
```

It means Keikai server has started up successfully at `localhost:8888`
You can now leave this window as is, and prepare to run your Java Client Application.

(If you need to shutdown Keikai Engine, just press `Ctrl+c`.)
