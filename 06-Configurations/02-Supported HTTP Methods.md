# Supported HTTP Methods

|ID          |
|------------|
|GTRT-CONF-02|

## Summary

HTTP offers a number of methods that can be used to perform actions on the web server. While GET and POST are by far the most common methods that are used to access information provided by a web server, HTTP allows several other methods. Some of these can be used for nefarious purposes if the web server is misconfigured.

However, most web applications only need to respond to GET and POST requests, receiving user data in the URL query string or appended to the request respectively. JavaScript and AJAX calls may send methods other than GET and POST but should usually not need to do that. Since the other methods are so rarely used, many developers do not know, or fail to take into consideration, how the web server or application framework's implementation of these methods impact the security features of the application.

## How to Test

### Discover Supported Methods

To perform this test, the tester needs some way to figure out which HTTP methods are supported by the web server that is being examined. While the OPTIONS HTTP method provides a direct way to do that, verify the server's response by issuing requests using different methods. This can be achieved by manual testing or something like the http-methods Nmap script.

### Testing for Access Control Bypass

Find a page to visit that has a security constraint such that a GET request would normally force a 302 redirect to a log in page or force a log in directly. Issue requests using various methods such as HEAD, POST, PUT etc. as well as arbitrarily made up methods such as BILBAO, FOOBAR, CATS, etc. If the web application responds with a HTTP/1.1 200 OK that is not a log in page, it may be possible to bypass authentication or authorization.

### Testing for Cross-Site Tracing Potential

The TRACE method, intended for testing and debugging, instructs the web server to reflect the received message back to the client. This method, while apparently harmless, can be successfully leveraged in some scenarios to steal legitimate users' credentials. This attack technique was discovered by Jeremiah Grossman in 2003, in an attempt to bypass the HttpOnly attribute that aims to protect cookies from being accessed by JavaScript. However, the TRACE method can be used to bypass this protection and access the cookie even when this attribute is set.

### Testing for HTTP Method Overriding

In scenarios where restricted verbs such as PUT or DELETE return a “405 Method not allowed”, replay the same request with the addition of the alternative headers for HTTP method overriding, and observe how the system responds. The application should respond with a different status code (e.g. 200) in cases where method overriding is supported.

### Tools

- [Ncat](https://nmap.org/ncat/)
- [cURL](https://curl.haxx.se/)
- [nmap http-methods NSE scripts](https://nmap.org/nsedoc/scripts/http-methods.html)
- [w3af plugin htaccess_methods](http://w3af.org/plugins/audit/htaccess_methods)

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/06-Test_HTTP_Methods.md