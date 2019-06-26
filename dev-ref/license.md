---
title: "License an Engine"
---

# Evaluation Engine
When starting up a Keikai engine under this state, there is a limited trial time message:

```
INFO: This is an evaluation copy of Keikai 1.0.0-beta.22@jvw6wenz. Your trial will end at "2019/08/19 00:00:00", if you wish to continue using Keikai please contact us at info@keikai.io.
1:8888:2019-06-26 06:49:44.009437Z:stream:4

```

Besides, you should see a evaluation mark at the right-bottom corner of each sheet:

![]({{ site.baseurl }}/assets/images/evaluationMark.png)



# Licensed Engine

## Install License file

* Default Path

put the license file under `keikai/license`

* Custom Path

specify the license folder when run the keikai engine.

`./keikai --lic-dir=AbsolutePath`


If you install a license file successfully, you should see the your license information like the one below when you start a Keikai engine:

```
Keikai Engine Installed Licenses: 1

*** Potix Corporation License Information (0) ***

  Licensed Company: Test Compnay
  Certificate Number: 123456789       
  Licensed Product: keikai component
  Maximum Licensed Number: 
  API Key: abcdefghiojklmnop
  Extended Trial until Oct. 10, 2019
```

## Java Client Requires an API key
At this state, you should create a new Java client with the corresponding API key:

```java
Settings settings = Settings.DEFAULT_SETTINGS.clone();
settings.set(Settings.Key.API_KEY, "abcdefghiojklmnop");

spreadsheet = Keikai.newClient(keikaiEngineAddress, settings);
```

If you connect the engine without a valid key (or without key), you will see the error message in your application server console:

```
java.lang.RuntimeException: io.keikai.client.kms.KMSException: The API key has invalid. Please contact us at info@keikai.io to obtain a valid API key.
Caused by null
```