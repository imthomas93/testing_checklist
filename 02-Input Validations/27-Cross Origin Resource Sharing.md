# Cross Origin Resource Sharing (CORS)

|ID          |
|------------|
|GTRT-INPV-27|

## Summary

Cross origin resource sharing (CORS) is a mechanism that enables a web browser to perform cross-domain requests using the XMLHttpRequest L2 API in a controlled manner. In the past, the XMLHttpRequest L1 API only allowed requests to be sent within the same origin as it was restricted by the same origin policy.

Cross-origin requests have an origin header that identifies the domain initiating the request and is always sent to the server. CORS defines the protocol to use between a web browser and a server to determine whether a cross-origin request is allowed. HTTP headers are used to accomplish this.

### Headers

#### Access-Control-Request-Method & Access-Control-Allow-Method

The Access-Control-Request-Method header is used when a browser performs a preflight OPTIONS request and let the client indicate the request method of the final request. On the other hand, the Access-Control-Allow-Method is a response header used by the server to describe the methods the clients are allowed to use.

#### Access-Control-Request-Headers & Access-Control-Allow-Headers

These two headers are used between the browser and the server to determine which headers can be used to perform a cross-origin request.

#### Access-Control-Allow-Credentials

This header as part of a preflight request indicates that the final request can include user credentials.

#### Others

There are other headers involved like Access-Control-Max-Age that determines the time a preflight request can be cached in the browser, or Access-Control-Expose-Headers that indicates which headers are safe to expose to the API of a CORS API specification, both are response headers specified in the CORS W3C document.

## How to Test

There are useful tools that enable testers to intercept HTTP headers, which can reveal how CORS is used. Testers should pay particular attention to the origin header to learn which domains are allowed. Also, manual inspection of the JavaScript is needed to determine whether the code is vulnerable to code injection due to improper handling of user supplied input.

### Tools

- [OWASP Zed Attack Proxy Project](https://www.zaproxy.org/)

## References

Application Development Security 1.1/S1(a) Manage logon session and access controls securely

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/11-Client-side_Testing/07-Testing_Cross_Origin_Resource_Sharing.md