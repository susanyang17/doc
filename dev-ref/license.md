
# Evaluation Engine
When starting up a Keikai engine under this state, there is a limited trial time message:

```
INFO: This is an evaluation copy of Keikai 1.0.0@jvw6wenz. 
Your trial will end at "2019/08/19 00:00:00", if you wish to continue using Keikai please contact us at info@keikai.io.
1:8888:2019-06-26 06:49:44.009437Z:stream:4

```

Besides, you should see a evaluation mark at the right-bottom corner of each sheet:

![]({{ site.baseurl }}/assets/images/evaluationMark.png)

## Expired Engine
If you start an engine whose trial period expired,  you will see the messsage below: 

```
INFO: This is an evaluation copy of Keikai 1.0.0-beta.11@jqlrv3br. 
The trial period has expired, please contact us at info@keikai.io for assistance.
```

Then the engine will exit.


# Licensed Engine
**Each machine requires one license**. If you run 2 engines on 2 different machines, you need to accquire 2 different licenses for 2 machines.

## Install a License File

* Default Path

put the license file under a specific folder in Keikai engine:  `keikai/license`

* Custom Path

specify the license folder when running a Keikai engine.

`./keikai --lic-dir=AbsolutePath`


If you install a license file successfully, you should see the your license information like the one below when you start a Keikai engine:

```
Keikai Engine Installed Licenses: 1

*** Potix Corporation License Information (0) ***

  Licensed Company: Test Compnay
  Certificate Number: 123456789       
  Licensed Product: keikai component
  Maximum Licensed Number: 1 installation
  API Key: abcdefghiojklmnop
  Extended Trial until Oct. 10, 2029
```

## Java Client Requires an API key
In your license information, you can see there is an API key printed:
```
API Key: abcdefghiojklmnop
```

To connect to a licensed engine, you should create a Java client with the matched API key:

```java
Settings settings = Settings.DEFAULT_SETTINGS.clone();
settings.set(Settings.Key.API_KEY, "abcdefghiojklmnop");

spreadsheet = Keikai.newClient(keikaiEngineAddress, settings);
```

If you connect the engine without a valid key (or without key), you will see the error message in your application server console and browser:

```
io.keikai.client.kms.KMSException: The API key is invalid. 
Please contact us at info@keikai.io to obtain a valid API key.
Caused by null
```

## Inconsistent License File
Each license file is generated for a specific machine. If you install the license file to another machine, you will see the error below when you start the engine:

```
WARNING: The license issued to "MyCompanyName" with "a-long-keikai-engine-serial-number" has a wrong Keikai engine serial number. 
Please contact info@keikai.io to obtain a valid license.
License file: license\Keikai_License_Signature_For_MyCompany.19062615
```