# Security headers (e.g., HSTS, CSP, X-Frame-Options)

|ID          |
|------------|
|GTRT-CONF-01|

## Summary

The HTTP Strict Transport Security (HSTS) header is a mechanism that web sites have to communicate to the web browsers that all traffic exchanged with a given domain must always be sent over https, this will help protect the information from being passed over unencrypted requests.

Considering the importance of this security measure it is prudent to verify that the web site is using this HTTP header in order to ensure that all the data travels encrypted from the web browser to the server.

The HTTP Strict Transport Security (HSTS) feature lets a web application inform the browser through the use of a special response header that it should never establish a connection to the the specified domain servers using HTTP. Instead it should automatically establish all connection requests to access the site through HTTPS.

The increase in XSS and clickjacking vulnerabilities demands a more defense in depth security approach. CSP comes in place to enforce the loading of resources (scripts, images, etc.) from restricted locations that are trusted by the server, as well as enforcing HTTPS usage transparently. 

## How to Test

Testing for the presence of HSTS header can be done by checking for the existence of the HSTS header in the server's response in an interception proxy, or by using curl.

### Tools

- [CSP Evaluator](https://csp-evaluator.withgoogle.com/)

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/07-Test_HTTP_Strict_Transport_Security.md

https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Content_Security_Policy_Cheat_Sheet.md