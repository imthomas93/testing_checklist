# Open Redirect

|ID          |
|------------|
|GTRT-INPV-13|

## Summary

This section describes how to check for client-side URL redirection, also known as open redirection. It is an input validation flaw that exists when an application accepts user-controlled input that specifies a link which leads to an external URL that could be malicious. This kind of vulnerability could be used to accomplish a phishing attack or redirect a victim to an infection page.

This vulnerability occurs when an application accepts untrusted input that contains a URL value and does not sanitize it. This URL value could cause the web application to redirect the user to another page, such as a malicious page controlled by the attacker.

This vulnerability may enable an attacker to successfully launch a phishing scam and steal user credentials. Since the redirection is originated by the real application, the phishing attempts may have a more trustworthy appearance.

## How to Test

When testers manually check for this type of vulnerability, they first identify if there are client-side redirections implemented in the client-side code. These redirections may be implemented, to give a JavaScript example, using the `window.location` object. This can be used to direct the browser to another page by simply assigning a string to it.

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/11-Client-side_Testing/04-Testing_for_Client-side_URL_Redirect.md