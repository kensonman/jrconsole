JRConsole
=========
Generate the report in command-line thru JasperReports with mininal dependencies.

This is the small program that generating the report using the JasperReports in command line tools. 


Usage
-----
Generating report:
   `java -cp <jar-file> -jar jrconsole.jar <options>`

Showing the version number of JRConsole
   `java -jar jrconsole.jar -version`

Showing the help menu
   `java -jar jrconsole.jar -help`

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

   boolean, int, long, double, url, date, decimal, stream, string, properties

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