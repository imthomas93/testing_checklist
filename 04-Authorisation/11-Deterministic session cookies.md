# Deterministic session cookies

|ID          |
|------------|
|GTRT-ATHZ-11|

## Summary

Web Cookies (herein referred to as cookies) are often a key attack vector for malicious users (typically targeting other users) and the application should always take due diligence to protect cookies.

HTTP is a stateless protocol, meaning that it doesn't hold any reference to requests being sent by the same user. In order to fix this issue, sessions were created and appended to HTTP requests. Browsers, as discussed in [testing browser storage](../11-Client-side_Testing/12-Testing_Browser_Storage.md), contain a multitude of storage mechanisms. In that section of the guide, each is discussed thoroughly.

The most used session storage mechanism in browsers is cookie storage. Cookies can be set by the server, by including a [`Set-Cookie`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) header in the HTTP response or via JavaScript. Cookies can be used for a multitude of reasons, such as:

- session management
- personalization
- tracking

## How to Test

Below, a description of every prefix will be discussed. The tester should validate that they are being used properly by the application. Cookies can be reviewed by using an intercepting proxy, or by reviewing the browser's cookie jar.

### Cookie Prefixes

By design cookies do not have the capabilities to guarantee the integrity and confidentiality of the information stored in them. Those limitations make it impossible for a server to have confidence about how a given cookie's attributes were set at creation. In order to give the servers such features in a backwards-compatible way, the industry has introduced the concept of [`Cookie Name Prefixes`](https://tools.ietf.org/html/draft-ietf-httpbis-cookie-prefixes-00) to facilitate passing such details embedded as part of the cookie name.

#### Host Prefix

The [`__Host-`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Cookie_prefixes) prefix expects cookies to fulfill the following conditions:

  1. The cookie must be set with the [`Secure` attribute](#secure-attribute).
  2. The cookie must be set from a URI considered secure by the user agent.
  3. Sent only to the host who set the cookie and MUST NOT include any [`Domain` attribute](#domain-attribute).
  4. The cookie must be set with the [`Path`attribute](#path-attribute) with a value of `/` so it would be sent to every request to the host.

For this reason, the cookie `Set-Cookie: __Host-SID=12345; Secure; Path=/` would be accepted while any of the following ones would always be rejected:
`Set-Cookie: __Host-SID=12345`
`Set-Cookie: __Host-SID=12345; Secure`
`Set-Cookie: __Host-SID=12345; Domain=site.example`
`Set-Cookie: __Host-SID=12345; Domain=site.example; Path=/`
`Set-Cookie: __Host-SID=12345; Secure; Domain=site.example; Path=/`

#### Secure Prefix

The [`__Secure-`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Cookie_prefixes) prefix is less restrictive and can be introduced by adding the case-sensitive string `__Secure-` to the cookie name. Any cookie that matches the prefix `__Secure-` would be expected to fulfill the following conditions:

  1. The cookie must be set with the `Secure` attribute.
  2. The cookie must be set from a URI considered secure by the user agent.

## References

Application Development Security 1.1/S1(a) Manage logon session and access controls securely

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/06-Session_Management_Testing/02-Testing_for_Cookies_Attributes.md
