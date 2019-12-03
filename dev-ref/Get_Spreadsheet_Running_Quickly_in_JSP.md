\_\_TOC\_\_

# Quick Start ZSS JSP Demo Project

Suggest you to run Keikai spreadsheet JSP demo project in your local site
without coding, just <https://github.com/zkoss/zssjspdemo> and execute
the command below (require to install <https://maven.apache.org/>)

`mvn jetty:run`

then visit <http://localhost:8080/zssjspdemo>
<http://localhost:8080/zssjspdemo> with your browser.

# Create and Run a JSP Project

We suggest you to start your project based on the demo project above.
That will save you the setup effort.

The following sections tell you how to start a project from the scratch
for working with Spreadsheet in JSP.

## Prerequisites

Before developing a web application with Spreadsheet, you should prepare
the following softwares:

  - Install
    <http://www.oracle.com/technetwork/java/javase/downloads/index.html>
    1.6 or above
  - Install an application server
      - You can install any Java web server you like. If you don't have
        one, <http://tomcat.apache.org> is a good choice.
  - Install a development tool.
      - In this book, we will use <http://www.eclipse.org/downloads> as
        the default IDE to explain related setup.

## Prepare a Project

We introduce 2 ways: **By Maven**(recommended) or **By Eclipse**. You
just need to choose one of them:

### By a Maven Project

  -   
    1\. Create a Maven project.
      -   
        You should set packaging to **war**.

<!-- end list -->

  -   
    2\. Setup Maven dependency.
      -   
        First, you should [ setup zk maven
        repository](ZK_Installation_Guide/Setting_up_IDE/Maven/Use_ZK_Maven_Artifacts/Resolving_ZK_Framework_Artifacts_via_Maven#Add_to_your_Maven_projects "wikilink")
        to use "EE Evaluation" or "EE". Notice that different editions
        are available at different repositories, and EE [ requires
        authentication](ZK_Installation_Guide/Setting_up_IDE/Maven/Use_ZK_Maven_Artifacts/Resolving_ZK_Framework_Artifacts_via_Maven#Login_authentication "wikilink").

<!-- end list -->

  - 
    
      -   
        Because this feature is only available in EE, you should add
        following dependencies:

<!-- end list -->

``` xml

<dependency>
    <groupId>io.keikai</groupId>
    <artifactId>zssex</artifactId>
    <version>${zss.version}</version>
</dependency>
<dependency>
    <groupId>io.keikai</groupId>
    <artifactId>zssjsp</artifactId>
    <version>${zss.version}</version>
</dependency> 
```

  - You can browser ZK maven repository to know available zss.version

You can reference the pom.xml in our example project to verify your own
pom.xml.

  -   
    3\. Set up web.xml.
      -   
        Please refer to [Sample of
        web.xml](ZK_Installation_Guide/ZK_Background/Sample_of_web.xml "wikilink").

### By an Eclipse Dynamic Web Project

If you have to create a project by your own, you can follow the steps
below:

1.  Create a dynamic web project
2.  Install Spreadsheet library
    1.  Download Keikai spreadsheet component (binary). Choose
        <http://www.zkoss.org/download/zkspreadsheet> or licensed EE
        from <http://www.zkoss.org/download/premium>.
          - 
    2.  Extract the zip and copy those JAR files under **`/dist/lib`**
        and **`/dist/lib/ext`** to **`/WEB-INF/lib`** under your web
        project's root folder.
          -   
            Make sure **zssjsp.jar** existed under `/WEB-INF/lib`.
3.  Set up web.xml
      -   
        Please refer to [Sample of
        web.xml](ZK_Installation_Guide/ZK_Background/Sample_of_web.xml "wikilink").

### Trouble Shooting

If you have problem switching from the evaluation repository to the
licensed one, please check
<http://books.zkoss.org/wiki/ZK_Installation_Guide/Setting_up_IDE/Maven/Resolving_ZK_Framework_Artifacts_via_Maven#Trouble_Shooting>.

## Verify Your Project

After completing above steps, preparation for working with Spreadsheet
and JSP is done. You can use a simple page to verify your preparation.
Steps are as follows:

1.  Create a simple Excel file or use the sample file in our example
    project. Put the file under your web application's root folder.
2.  Create `index.jsp` with content below:

<!-- end list -->

``` xml
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@taglib prefix="zssjsp" uri="http://www.zkoss.org/jsp/zss"%> http://www.zkoss.org/jsp/zss"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
    "http://www.w3.org/TR/html4/loose.dtd"> http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>My First Keikai spreadsheet JSP application</title>
    <zssjsp:head/>
</head>
<body>
<div width="100%" style="height: 100%;">
    <zssjsp:spreadsheet
    id="myzss" src="/WEB-INF/hellozss.xlsx" width="100%"
    height="100%" maxVisibleRows="200" maxVisibleColumns="40" showSheetbar="true"/>
</div>
</body>
</html>
```

  - Line 3: Declare a taglib before using Spreadsheet JSP tag is
    necessary.
  - Line 9: The head tag generates ZK required JS and CSS.
  - Line 13: Use spreadsheet JSP tag with prefix you specified in
    taglib.

Now, deploy the project to your application server and visit `index.jsp`
to see if you can see the Spreadsheet.
