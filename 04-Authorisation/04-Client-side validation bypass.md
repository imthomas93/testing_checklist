# Client-side validation bypass

|ID          |
|------------|
|GTRT-ATHZ-04|

## Summary

Input validation must always be done on the server-side for security. While client side validation can be useful for both functional and some security purposes it can often be easily bypassed.

It is common to see customized client-side input validation implemented within scripts. Client-side controls of this kind are usually easy to circumvent; it is possible to enter a benign value into the input field in the browser, intercept the validated submission with your proxy, and modify the data to your desired value.

## How to Test

First, identify a webpage that has input validation implemented.

Next, capture a benign HTTP/HTTPS request with an intercepting web proxy, such as Burp Suite. For HTTPS requests, you will first need to install [Burp's Certificate Authority](https://portswigger.net/burp/documentation/desktop/tools/proxy/options/installing-ca-certificate).

After intercepting the benign request, modify the data such that the modified data would trigger the input validation if submitted normally. If the request is succesful, the server should respond with a HTTP status 200, indicated that client-side validation has been bypassed.

## References

Application Development Security 1.1/S1(a) Manage logon session and access controls securely

https://owasp.org/www-project-proactive-controls/v3/en/c5-validate-inputs

https://portswigger.net/support/using-burp-to-bypass-client-side-javascript-validation

https://portswigger.net/burp/documentation/desktop/tools/proxy/options/installing-ca-certificate
