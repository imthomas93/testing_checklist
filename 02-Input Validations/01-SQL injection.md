# SQL injection

|ID          |
|------------|
|GTRT-INPV-01|

## Summary

SQL injection testing checks if it is possible to inject data into the application so that it executes a user-controlled SQL query in the database. Testers find a SQL injection vulnerability if the application uses user input to create SQL queries without proper input validation. A successful exploitation of this class of vulnerability allows an unauthorized user to access or manipulate data in the database.

An SQL injection attack consists of insertion or "injection" of either a partial or complete SQL query via the data input or transmitted from the client (browser) to the web application. A successful SQL injection attack can read sensitive data from the database, modify database data (insert/update/delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file existing on the DBMS file system or write files into the file system, and, in some cases, issue commands to the operating system. SQL injection attacks are a type of injection attack, in which SQL commands are injected into data-plane input in order to affect the execution of predefined SQL commands.

SQL Injection attacks can be divided into the following three classes:

- Inband: data is extracted using the same channel that is used to inject the SQL code. This is the most straightforward kind of attack, in which the retrieved data is presented directly in the application web page.
- Out-of-band: data is retrieved using a different channel (e.g., an email with the results of the query is generated and sent to the tester).
- Inferential or Blind: there is no actual transfer of data, but the tester is able to reconstruct the information by sending particular requests and observing the resulting behavior of the DB Server.

## How to Test

### Detection Techniques

The first step in this test is to understand when the application interacts with a DB Server in order to access some data.

The tester has to make a list of all input fields whose values could be used in crafting a SQL query, including the hidden fields of POST requests and then test them separately, trying to interfere with the query and to generate an error. Consider also HTTP headers and Cookies.

The very first test usually consists of adding a single quote or a semicolon to the field or parameter under test. The first is used in SQL as a string terminator and, if not filtered by the application, would lead to an incorrect query. The second is used to end a SQL statement and, if it is not filtered, it is also likely to generate an error.

Monitor all the responses from the web server and have a look at the HTML/JavaScript source code. Sometimes the error is present inside them but for some reason (e.g. JavaScript error, HTML comments, etc) is not presented to the user. A full error message provides a wealth of information to the tester in order to mount a successful injection attack. However, applications often do not provide so much detail: a simple '500 Server Error' or a custom error page might be issued, meaning that we need to use blind injection techniques. In any case, it is very important to test each field separately: only one variable must vary while all the other remain constant, in order to precisely understand which parameters are vulnerable and which are not.

### Fingerprinting the Database

Even though the SQL language is a standard, every DBMS has its peculiarity and differs from each other in many aspects like special commands, functions to retrieve data such as users names and databases, features, comments line etc.

When the testers move to a more advanced SQL injection exploitation they need to know what the back end database is.

1. #### Errors Returned by the Application

   The first way to find out what back end database is used is by observing the error returned by the application.

2. ####  Concatenation techniques

   If there is no error message or a custom error message, the tester can try to inject into string fields using varying concatenation techniques as each database use different concatenation techniques.

### Tools

- [SQL Injection Fuzz Strings (from wfuzz tool) - Fuzzdb](https://github.com/fuzzdb-project/fuzzdb/tree/master/attack/sql-injection)
- [sqlbftools](http://packetstormsecurity.org/files/43795/sqlbftools-1.2.tar.gz.html)
- [Bernardo Damele A. G.: sqlmap, automatic SQL injection tool](http://sqlmap.org/)
- [Muhaimin Dzulfakar: MySqloit, MySql Injection takeover tool](https://github.com/dtrip/mysqloit)

## References

Application Development Security 1.1/S1(c) Ensure the immutability of database query structures by using means such as parameterised SQL queries, whenever possible 

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/05-Testing_for_SQL_Injection.md