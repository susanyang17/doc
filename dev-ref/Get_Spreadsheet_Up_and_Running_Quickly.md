# Overview

This chapter tells you how to run Spreadsheet App and get ready to
develop with Spreadsheet. If you are interested in using spreadsheet in
JSP, please refer to [ Get Spreadsheet Running Quickly in
JSP](ZK_Spreadsheet_Essentials_3/Using_Spreadsheet_in_JSP/Get_Spreadsheet_Running_Quickly_in_JSP "wikilink").
If you are going to use Spreadhsheet in JSF, please refer to [ Get
Spreadsheet Running Quickly in
JSF](ZK_Spreadsheet_Essentials_3/Using_Spreadsheet_in_JSF/Get_Spreadsheet_Running_Quickly_in_JSF "wikilink").

# Download and Experience

## Start with WAR

If you want to quickly run Keikai spreadsheet at your local site, please
download <http://www.zkoss.org/download/zkspreadsheet> which is an
Excel-like web application. We created it to demonstrate Spreadsheet
numerous powerful features.

After you download, please:

1.  Deploy the Spreadsheet App's war file to your application server
    according to its instruction.
      -   
        For Tomcat just put the war file in `[CATALINA_HOME]\webapps`.
2.  Start your application server and connect it with your browser.
      -   
        For Tomcat, just visit <http://localhost:8080/zssapp>
        <http://localhost:8080/zssapp> then you can start to experience
        the power of Spreadsheet.

The full introduction of Spreadsheet App's function is covered in [
Spreadsheet
App](ZK_Spreadsheet_Essentials_3/Using_Spreadsheet_in_ZK/Spreadsheet_App "wikilink")
and the Spreadsheet's features are described in [ Features and
Usage](ZK_Spreadsheet_Essentials_3/Features_and_Usage "wikilink").

The purpose of following paragraphs is to tell you how to prepare an
environment for working with Spreadsheet in API.

## Start with Example Project

Clone <https://github.com/zkoss/zssessentials> and follow the steps in
readme to start it.

# Prerequisites

Before developing a web application with Spreadsheet, you should prepare
the following software:

  - Install
    <http://www.oracle.com/technetwork/java/javase/downloads/index.html>
    1.6 or above
  - Install an application server
      - You can install any Java web server you like. If you don't have
        one, <http://tomcat.apache.org> is a good choice.
  - Install a development tool.
      - In this book, we will use <http://www.eclipse.org/downloads> as
        the default IDE to explain related setup.

# Develop with Maven

## Example Project

Download <https://github.com/zkoss/zssessentials> that contains source
code in this book can save your time. You can base on that project to
start your owned one.

## Start from Scratch

  -   
    1\. Create a Maven project.
      -   
        You should set packaging to **war**.

<!-- end list -->

  -   
    2\. Setup Maven Repository.
      -   
        First, you should [ setup zk maven
        repository](ZK_Installation_Guide/Setting_up_IDE/Maven/Use_ZK_Maven_Artifacts/Resolving_ZK_Framework_Artifacts_via_Maven#Add_to_your_Maven_projects "wikilink")
        according to what Spreadsheet edition you use, and EE [ requires
        authentication](ZK_Installation_Guide/Setting_up_IDE/Maven/Use_ZK_Maven_Artifacts/Resolving_ZK_Framework_Artifacts_via_Maven#Login_authentication "wikilink").

## Repository for Open Source Edition (OSE)

``` xml
 <repositories>
    <repository>
      <id>ZK CE</id>
      <url>http://mavensync.zkoss.org/maven2</url> http://mavensync.zkoss.org/maven2</url>
    </repository>
  </repositories>
```

## Repository for EE Evaluation

``` xml
 <repositories>
    <repository>
      <id>ZK PE/EE Evaluation</id>
      <url>http://mavensync.zkoss.org/eval/</url> http://mavensync.zkoss.org/eval/</url>
    </repository>
  </repositories>
```

## Repository for EE Premium Users Only

Please refer to [setup Maven repository for premium
users](ZK_Installation_Guide/Setting_up_IDE/Maven/Use_ZK_Maven_Artifacts/Resolving_ZK_Framework_Artifacts_via_Maven#3._PE_.2F_EE_.28premium_users_only.29 "wikilink").

  -   
    3\. Setup Maven dependency.

## Open Source Edition (OSE)

  - 
    
      -   
        If you use Open Source Edition (OSE), add the dependency
        `io.keikai:zss`:

<!-- end list -->

``` xml

        <dependency>
            <groupId>io.keikai</groupId>
            <artifactId>zss</artifactId>
            <version>${zss.version}</version>
        </dependency>
```

  - `${zss.version}` can be 3.0.1 or above.

## Enterprise Edition (Evaluation and premium users )

  - 
    
      -   
        If you use Enterprise Edition (EE Evaluation or EE for premium
        users), you should add `io.keikai:zssex`.

<!-- end list -->

``` xml

        <dependency>
            <groupId>io.keikai</groupId>
            <artifactId>zssex</artifactId>
            <version>${zss.version}</version>
        </dependency>   
```

  - If `${zss.version}` is 3.0.1 or above.

You can reference the pom.xml in our example project to verify your own
pom.xml.

  -   
    4\. Set up web.xml.
      -   
        Please refer to [Sample of
        web.xml](ZK_Installation_Guide/ZK_Background/Sample_of_web.xml "wikilink").

## Sample of pom.xml

Here is a sample of pom.xml for a simple Java web project that uses the
Keikai spreadsheet.

``` xml
<project xmlns="http://maven.apache.org/POM/4.0.0" http://maven.apache.org/POM/4.0.0" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/POM/4.0.0 
        http://maven.apache.org/xsd/maven-4.0.0.xsd"> http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>io.keikai</groupId>
    <artifactId>sample</artifactId>
    <description>A project to demonstrate sample pom.xml.</description>
    <properties>
        <zss.version>3.9.5-Eval</zss.version>
        <zk.version>8.0.5-Eval</zk.version>
    </properties>
    <version>1.0.0</version>
    <packaging>war</packaging>
    <name>zss maven sample</name>
    <repositories>
        <repository>
            <id>ZK EVAL</id>
            <name>ZK Evaluation Repository</name>
            <url>http://mavensync.zkoss.org/eval</url> http://mavensync.zkoss.org/eval</url>
        </repository>        
    </repositories>
    <dependencies>        
        <!-- Required if using Keikai spreadsheet OSE -->
        <dependency>
            <groupId>io.keikai</groupId>
            <artifactId>zss</artifactId>
            <version>${zss.version}</version>
        </dependency>
        <!-- Required if using Keikai spreadsheet EE -->
        <dependency>
            <groupId>io.keikai</groupId>
            <artifactId>zssex</artifactId>
            <version>${zss.version}</version>
        </dependency>
        <!-- [Optional] Using Keikai spreadsheet PDF Exporter -->
        <dependency>
            <groupId>io.keikai</groupId>
            <artifactId>zsspdf</artifactId>
            <version>${zss.version}</version>
        </dependency>
        <!-- ZK -->
        <dependency>
            <groupId>org.zkoss.common</groupId>
            <artifactId>zcommon</artifactId>
            <version>${zk.version}</version>
        </dependency>     
        <dependency>
            <groupId>org.zkoss.zk</groupId>
            <artifactId>zkplus</artifactId>
            <version>${zk.version}</version>
        </dependency>
        <dependency>
            <groupId>org.zkoss.zk</groupId>
            <artifactId>zkex</artifactId>
            <version>${zk.version}</version>
        </dependency>
    </dependencies>
</project>
```

### Version Dependency and Naming

Different versions of Keikai spreadsheet depends on different ZK version.
Here are the suggested versions,

Keikai spreadsheet 3.5: ZK 7.0.3  
Keikai spreadsheet 3.9: ZK 8.0.5

For customers using 3.0.1, if you require "IE 11 support" feature, you
should override ZK dependencies with **6.5.5** because 3.0.1 depends on
ZK 6.5.4 by default. If we take above sample pom.xml as an example, just
uncomment those ZK dependencies and set property `zk.version` to 6.5.5.

Also note that starting from version 3.5, evaluation copies are renamed
with a post-fix of Eval. For example the version number of ZSS 3.5.0
evaluation copy is now 3.5.0-Eval.

## Trouble Shooting

If you have problem switching from the evaluation repository to the
licensed one, please check
<http://books.zkoss.org/wiki/ZK_Installation_Guide/Setting_up_IDE/Maven/Resolving_ZK_Framework_Artifacts_via_Maven#Trouble_Shooting>.

# Develop with Eclipse Dynamic Web Project

If you have to create a project by your own, you can follow the steps
below:

1.  Create a dynamic web project
2.  Install Spreadsheet library
    1.  Download Keikai spreadsheet component (binary). Choose "Open Source
        Downloads" or "Free Evaluation Downloads" from
        <http://www.zkoss.org/download/zkspreadsheet> or EE from
        <http://www.zkoss.org/download/premium>.
          - 
    2.  Extract the zip and copy those JAR files under **`/dist/lib`**
        and **`/dist/lib/ext`** to **`/WEB-INF/lib`** under your web
        project's root folder.
3.  Set up web.xml
      -   
        Please refer to [Sample of
        web.xml](ZK_Installation_Guide/ZK_Background/Sample_of_web.xml "wikilink").

# Verify Your Project

After completing above steps, preparation for working with Spreadsheet
is done. You can use a simple page to verify your preparation. Steps are
as follows:

  -   
    1\. Create a simple Excel file or use the sample file in our example
    project. Put the file under your web application's root folder.

<!-- end list -->

  -   
    2\. Create a index.zul file with content below:

**index.zul**

``` xml
<spreadsheet src="/sample.xlsx"
height="100%" width="100%" maxVisibleRows="150" maxVisibleColumns="40"
showToolbar="true" showSheetbar="true" showFormulabar="true"/>
```

  - Line 2: Specify your file path in `src` attribute.

<!-- end list -->

  -   
    3\. Deploy and run your project in an application server.

<!-- end list -->

  -   
    4\. Visit the index.zul in a browser.

If you see that Spreadsheet displays your sample Excel file in your
browser. Congratulation\! Your setup is correct.

# Work with ZK 8.5 or Later

Since ZK 8.5.0, the default theme is **iceblue** which is not supported
by Spreadsheet. You have to manually switch to the breeze theme with the
following steps:

## 1\. Add breeze jar

In maven pom.xml:

``` xml
        <dependency>
            <groupId>org.zkoss.theme</groupId>
            <artifactId>breeze</artifactId>
            <version>${zk.version}</version>
        </dependency>
```

## 2\. Specified Preferred Theme

In zk.xml

``` xml
    <library-property>
        <name>org.zkoss.theme.preferred</name>
        <value>breeze</value>
    </library-property>
```

# Working with Spreadsheet

After using for a while, you might think "Great\! But I hope its width
can be smaller". Don't worry. Spreadsheet provides various options which
can be configured via ZUL to fulfill your requirements, and you can even
use its API to implement your own business logic in order to react to
events. Please read [ Working with
Spreadsheet](ZK_Spreadsheet_Essentials_3/Working_with_Spreadsheet "wikilink")
for details.
