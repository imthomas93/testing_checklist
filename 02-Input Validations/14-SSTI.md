# SSTI 

|ID          |
|------------|
|GTRT-INPV-14|

## Summary

Web applications commonly use server-side templating technologies (Jinja2, Twig, FreeMaker, etc.) to generate dynamic HTML responses. Server-side Template Injection vulnerabilities (SSTI) occur when user input is embedded in a template in an unsafe manner and results in remote code execution on the server. Any features that support advanced user-supplied markup may be vulnerable to SSTI including wiki-pages, reviews, marketing applications, CMS systems etc. Some template engines employ various mechanisms (eg. sandbox, allow listing, etc.) to protect against SSTI.

## How to Test

SSTI vulnerabilities exist either in text or code context. In plaintext context users allowed to use freeform 'text' with direct HTML code. In code context the user input may also be placed within a template statement (eg. in a variable name). In both cases the testing methodology has the following steps:

1. Detect template injection vulnerability points - construct common template expressions used by various template engines as payloads and monitor server responses to identify which template expression was executed by the server.

Common template expression examples:

```
a{{bar}}b
a{{7*7}}
{var} ${var} {{var}} <%var%> [% var %]
```

1. Identify the templating engine - Based on the information obtained from the previous step, the tester now has to identify which template engine is used by supplying various template expressions. Based on the server responses, the tester deduces the template engine used.
2. Build the exploit - The main goal in this step is to identify to gain further control on the server with an RCE exploit by studying the template documentation and research. The tester can also identify what other objects, methods and properties can be exposed by focusing on the `self` object. If the `self` object is not available and the documentation does not reveal the technical details, a brute force of the variable name is recommended. Once the object is identified the next step is to loop through the object to identify all the methods, properties and attributes that are accessible through the template engine. This could lead to other kinds of security findings including privilege escalations, information disclosure about application passwords, API keys, configurations and environment variables, etc.

### Tools

1. [Tplmap](https://github.com/epinna/tplmap)
2. [Backslash Powered Scanner Burp Suite extension](https://github.com/PortSwigger/backslash-powered-scanner)
3. [Template expression test strings/payloads list](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server Side Template Injection)

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/18-Testing_for_Server-side_Template_Injection.md