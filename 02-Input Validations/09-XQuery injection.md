# XQuery injection

|ID          |
|------------|
|GTRT-INPV-09|

## Summary

XQuery injection is a variant of the classic SQL injection attack against the XML XQuery Language. XQuery injection uses improperly validated data that is passed to XQuery commands. The application unsafely incorporates user data into an XQuery or XPath pattern, which can change the logic of the query. 

With the XQuery injection attack, queries execute commands on behalf of the attacker that the XQuery routines have access to. XQuery injection can be used to enumerate elements on the victim's environment, inject commands to the local host, or execute queries to remote files and data sources. Like SQL injection attacks, the attacker tunnels through the application entry point to target the resource access layer.

## How to Test

As in a common SQL Injection attack, with XQuery injection, the first step is to insert a single quote in the field to be tested, introducing a syntax error in the query, and to check whether the application returns an error message.

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://vulncat.fortify.com/en/detail?id=desc.dataflow.java.xquery_injection#PHP