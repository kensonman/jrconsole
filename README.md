JRConsole
=========
Generate the report in command-line thru JasperReports with mininal dependencies.

This is the small program that generating the report using the JasperReports in command line tools. 

License
-------
Copyright 2013 kenson.idv.hk

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


Installation
------------
Simply execute the Apache Ant (1.8 or above) to building the console.
`ant build`

Before you execute the applciation with database connection, you have to download the related jdbc driver by yourself.
You can paste it into the `lib` folder. It will make the ant execution work.

And also, you have to export the related fonts (that used in your report) in a jar and put it into your classpath.

Usage
-----
Generating report:
   `java -cp <jar-file> -jar jrconsole.jar <options>`

Showing the version number of JRConsole
   `java -jar jrconsole.jar -version`

Showing the help menu
   `java -jar jrconsole.jar -help`

Executing the application in ant (It will load all jar files, which located in the lib folder, into your classpath automatically)
   `ant run [-jvmargs [-DdateFormat|-DdecimalFormat]] -args <Options>`

Options
-------
-   -driver             : The jdbc driver class name
-   -source             : The datasource specification. It can be the jdbc-url or file path
-   -type               : The datasource type. It can be 'jdbc', 'csv', 'json' or 'xml'. Default is 'jdbc'
-   -username           : The username of the data-source
-   -password           : The password of the data-source
-   -jrxml              : The path of the jrxml file. I'll compile it automatically
-   -jasper             : The compiled jasper file
-   -outputtype         : The report file type. Default is PDF
-   -output             : The output path of the report (Currently support 'pdf' and 'odt')
-   -locale             : Specified the locale. [See More](http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html)
-   -bundle             : Specified the resource-bundle during filling the report. It can be the 
                          classpath resource (started with "classpath:" prefix) or filesystem path.
-   -Dparam             : The parameter that passed into JasperReport. See Parameters section for more details.

### Parameters
JRConsole support to parsing the parameter into jasperreports library when filling report.

Due to JasperReport required the parameter in java classes, the JRConsole will parsing the parameter into related java object (according to the data-type-prefix, separated by colon) and pass into JasperReports.

#### Supported Parameter Types:

- boolean: true|false
- int: An integer
- long: A long integer
- double: A double floating number
- url: An instance of java.lang.URL
- date: An instance of java.util.Date. Parsing by "dateFormat" system property
- decimal: A number that parsing by "decimalFormat" system property
- stream: A stream opened by URL
- string: A String
- properties: The properties

* Date Format can be specified by system property "dateFormat". Default is: yyyy-MM-dd
* Decimal Format can be specified by system property "decimalFormat". Default is: #,##0.0

Examples
--------
   `java -cp jasperreport.jar:postgresql.jar:itext.jar -DdateFormat yyyy-MM-dd -jar jrconsole.jar 
        -type jdbc 
        -driver org.postgresql.Driver 
        -source jdbc:postgresql://localhost:5432/dbname 
        -username test -password abc123 
        -jrxml /home/test/report.jrxml 
        -output /home/test/report.pdf -outputtype pdf 
        -Dabc boolean:true -DreportDate date:2013-01-28 -DDemo string:abcdefg`
