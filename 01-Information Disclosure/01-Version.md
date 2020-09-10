# Version (e.g., server, application, etc)

|ID          |
|------------|
|GTRT-INFO-01|

## Summary

A paramount step in testing for web application vulnerabilities is to find out which particular applications are hosted on a web server. Many applications have known vulnerabilities and known attack strategies that can be exploited in order to gain remote control or to exploit data. In addition, many applications are often misconfigured or not updated, due to the perception that they are only used “internally” and therefore no threat exists. With the proliferation of virtual web servers, the traditional 1:1-type relationship between an IP address and a web server is losing much of its original significance. It is not uncommon to have multiple web sites or applications whose symbolic names resolve to the same IP address. This scenario is not limited to hosting environments, but also applies to ordinary corporate environments as well.

Security professionals are sometimes given a set of IP addresses as a target to test. It is arguable that this scenario is more akin to a penetration test-type engagement, but in any case it is expected that such an assignment would test all web applications accessible through this target. The problem is that the given IP address hosts an HTTP service on port 80, but if a tester should access it by specifying the IP address (which is all they know) it reports “No web server configured at this address” or a similar message. But that system could “hide” a number of web applications, associated to unrelated symbolic (DNS) names. Obviously, the extent of the analysis is deeply affected by the tester tests all applications or only tests the applications that they are aware of.

Sometimes, the target specification is richer. The tester may be given a list of IP addresses and their corresponding symbolic names. Nevertheless, this list might convey partial information, i.e., it could omit some symbolic names and the client may not even being aware of that (this is more likely to happen in large organizations).

Other issues affecting the scope of the assessment are represented by web applications published at non-obvious URLs (e.g., http://www.example.com/some-strange-URL), which are not referenced elsewhere. This may happen either by error (due to misconfigurations), or intentionally (for example, unadvertised administrative interfaces).

To address these issues, it is necessary to perform web application discovery.

## How to Test

Techniques used for web server fingerprinting include banner grabbing, eliciting responses to malformed requests, and using automated tools to perform more robust scans that use a combination of tactics. The fundamental premise by which all these techniques operate is the same. They all strive to elicit some response from the web server which can then be compared to a database of known responses and behaviors, and thus matched to a known server type.

1. Banner Grabbing - 
A banner grab is performed by sending an HTTP request to the web server and examining its response header. This can be accomplished using a variety of tools, including telnet for HTTP requests, or openssl for requests over SSL.


2. Sending Malformed Requests - 
Web servers may be identified by examining their error responses, and in the cases where they have not been customized, their default error pages. One way to compel a server to present these is by sending intentionally incorrect or malformed requests.

## References

Application Development Security 1.1/S1(l) Prevent the disclosure of sensitive information or credentials in error response and logs

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/01-Information_Gathering/02-Fingerprint_Web_Server.md



