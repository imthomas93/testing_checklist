# Code Injection

|ID          |
|------------|
|GTRT-INPV-10|

## Summary

This section describes how a tester can check if it is possible to enter code as input on a web page and have it executed by the web server.

In Code Injection testing, a tester submits input that is processed by the web server as dynamic code or as an included file. These tests can target various server-side scripting engines, e.g ASP or PHP. Proper input validation and secure coding practices need to be employed to protect against these attacks.

## How to Test

### Black-Box Testing

1. Testing for PHP Injection Vulnerabilities - Using a query string, the tester can inject code (in this example, a malicious URL) to be processed as part of the included file.

### Gray-Box Testing

1. Testing for ASP Code Injection Vulnerabilities - Examine ASP code for user input used in execution functions. Can the user enter commands into the Data input field?

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11-Testing_for_Code_Injection.md