# SSI Injection

|ID          |
|------------|
|GTRT-INPV-07|

## Summary

Web servers usually give developers the ability to add small pieces of dynamic code inside static HTML pages, without having to deal with full-fledged server-side or client-side languages. This feature is incarnated by the Server-Side Includes. In SSI injection testing, we test if it is possible to inject into the application data that will be interpreted by SSI mechanisms. A successful exploitation of this vulnerability allows an attacker to inject code into HTML pages or even perform remote code execution.

Server-Side Includes are directives that the web server parses before serving the page to the user. They represent an alternative to writing CGI programs or embedding code using server-side scripting languages, when there's only need to perform very simple tasks. Common SSI implementations provide commands to include external files, to set and print web server CGI environment variables, and to execute external CGI scripts or system commands.

As in every bad input validation situation, problems arise when the user of a web application is allowed to provide data that makes the application or the web server behave in an unforeseen manner. With regard to SSI injection, the attacker could provide input that, if inserted by the application (or maybe directly by the server) into a dynamically generated page, would be parsed as one or more SSI directives.

## How to Test

### Black-Box Testing

The first thing to do when testing in a Black Box fashion is finding if the web server actually supports SSI directives. Often, the answer is yes, as SSI support is quite common. To find out we just need to discover which kind of web server is running on our target, using classic information gathering techniques.

Whether we succeed or not in discovering this piece of information, we could guess if SSI are supported just by looking at the content of the target web site. If it contains `.shtml` files, then SSI are probably supported, as this extension is used to identify pages containing these directives. Unfortunately, the use of the `shtml` extension is not mandatory, so not having found any `shtml` files doesn't necessarily mean that the target is not prone to SSI injection attacks.

The next step consists of determining if an SSI injection attack is actually possible and, if so, what are the input points that we can use to inject our malicious code.

The testing activity required to do this is exactly the same used to test for other code injection vulnerabilities. In particular, we need to find every page where the user is allowed to submit some kind of input, and verify whether the application is correctly validating the submitted input. If sanitization is insufficient, we need to test if we can provide data that is going to be displayed unmodified (for example, in an error message or forum post). Besides common user-supplied data, input vectors that should always be considered are HTTP request headers and cookies content, since they can be easily forged.

Once we have a list of potential injection points, we can check if the input is correctly validated and then find out where the provided input is stored. We need to make sure that we can inject characters used in SSI directives:

```
< ! # = / . " - > and [a-zA-Z0-9]
```

If the application is vulnerable, the directive is injected and it would be interpreted by the server the next time the page is served, thus including the content of the Unix standard password file.

The injection can be performed also in HTTP headers, if the web application is going to use that data to build a dynamically generated page.

### Gray-Box Testing

If we have access to the application source code, we can quite easily find out:

- If SSI directives are used. If they are, then the web server is going to have SSI support enabled, making SSI injection at least a potential issue to investigate.
- Where user input, cookie content and HTTP headers are handled. The complete list of input vectors is then quickly determined.
- How the input is handled, what kind of filtering is performed, what characters the application is not letting through, and how many types of encoding are taken into account.

Performing these steps is mostly a matter of using grep to find the right keywords inside the source code (SSI directives, CGI environment variables, variables assignment involving user input, filtering functions and so on).

### Tools

- [Web Proxy Burp Suite](https://portswigger.net/)
- [OWASP ZAP](https://www.zaproxy.org/)
- [String searcher: grep](https://www.gnu.org/software/grep)

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/08-Testing_for_SSI_Injection.md