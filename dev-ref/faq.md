---
title: "Frequently Asked Questions"
---

# Wrong version between Keikai client and engine
When you visit a page with Keikai, if you see the error:

![](/assets/images/inconsistentVersion.png)

That means the version of Keikai Java client is inconsistent with the engine. The message also tells you both the client and engine version you use. You need to make both version consistent, so you can either:
* [Contact us](https://keikai.io/#contact) to download another version of Keikai engine
* Change Keikai client version to match engine's

## How to change the Keikai client version:
Just modify the version string in the corresponding file depending on which tool you run this project. 

### Maven
pom.xml

`<version>*-Eval</version>`

### Gradle

build.gradle

`compile "io.keikai:keikai-java-client:*-Eval"`

 
 
# Import Larger Files
Importing larger files require a larger heap size. Here are peak heap size consumed by an application server. Please reference it to specify your server's heap size.

| File size | Number of Cells| Peak Heap Size| 
| --------- | -------------- | ------------------ |
| 10 MB     | 1.4 millions  | 1.5G  |
| 20 MB     | 2.9 millions  | 1.9G  |
| 40 MB     | 8.7 millions  | 2.5G  |

If you wish to try importing large files, please increase your heap size accordingly. 
You can increase the heap size with JVM arguments:

## Gradle
`gradle appRun -Dorg.gradle.jvmargs=-Xmx4g`


## maven
modify the configurations of jetty-maven-plugin in pom.xml
```
<jvmArgs>-Xmx4096m</jvmArgs>
```
please refer to https://www.eclipse.org/jetty/documentation/9.4.x/jetty-maven-plugin.html



# Start Keikai engine with different port and address
`./keikai  -—port=9999 -—address=192.168.1.1`

* For complete options, you can check with the command:
`./keikai --help`



# Connect to a Different Keikai engine Address
By default, this project connects to a Keikai engine at `localhost:8888`. If you wish to connect to a different address, please append a query string with the `server` key:
 
 `http://localhost:8080/tutorial/editor?server=10.1.1.1:8888`



# How to start the tutorial project with gradle
##  Linux / Mac

### Gradle wrapper
`./gradlew appRun`

## Window

### Gradle wrapper
`gradlew appRun`

# Maximal column/row of a sheet
Just like [Excel](https://support.office.com/en-us/article/excel-specifications-and-limits-1672b34d-7043-467e-8e27-269d656771c3):
* Maximal column number: 16,384 (XFD)
* Maximal row number: 1,048,576


# How to debug

## Range API runtime error
Since Keikai client API actually sends a command to a Keikai engine to execute operations remotely instead of executing it locally. So such the error caused by setter API can't show a line number of your program. For example, if you call a Keikai java client API, and it produces an error. Please scoll down to check the last error stack trace:

```
socketPool-2-eventThread-1] ERROR io.keikai.client.kms.KMSClient - Remote server runtime error: ca3q13499ub36:["{"winId":"ca3q13499ub36","cmd":"Range.setValue","data":{"sheetId":"*nuv0HGJiwkBd4.XeDZOOTXPp","range":"a1a","bookName":"Book1.xlsx","value":"a1s"}}"]
Bad state: No element
#0      ...
```
Then You can check `"cmd":"Range.setValue"`, `"range":"a1a"` in that Json data, that means you the error is caused by `Range.setValue()` and the range is `a1a`. So you can search you code with the detail and found the root cause:

setting value on a non-existed cell: `spreadsheet.getRange("a1a").setValue("123");`


# Session Timeout
Keikai keeps sending requests to an application server to avoid session timeout.

If there is a proxy server between your application and browsers, and you see such message:
```
The action you request is no longer available.
This is normally caused by timeout.
You have to reload the page and try again.
```

Open developer tool to check if there is an error similar like:
`POST http://localhost:8080/appContextPath/kk 404 (Not Found)`

That's because the proxy maps [path-a] to [path-b] so that keikai keep-alive request doesn't send to the correct path. Then finally a session expires.

You need to specify the target context path:
```java
        Settings settings = Settings.DEFAULT_SETTINGS.clone();
        settings.set(Settings.Key.CONTEXT_PATH, "TheRealApplicationContentPath");
        Keikai.newClient(keikaiServerAddress, settings);
```

# Support to Run VB macro?
No. Even Microsoft Excel online doesn't support running VB macro (Please see [Editing files with VBA](https://www.microsoft.com/en-us/microsoft-365/blog/2014/04/14/weve-updated-excel-online-whats-new-in-april-2014/) or [here](https://social.technet.microsoft.com/Forums/office/en-US/7c46823c-2581-47a6-baac-66fb99ac3ea8/does-office-365-online-version-supports-vbavisual-basic-for-applications?forum=Office2016ITPro)). 

If you need do something similar, you need to port your VB macro to Java within [event listeners](/dev-ref/handle-events).
