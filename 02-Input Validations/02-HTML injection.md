# HTML injection

|ID          |
|------------|
|GTRT-INPV-02|

## Summary

HTML injection is a type of injection vulnerability that occurs when a user is able to control an input point and is able to inject arbitrary HTML code into a vulnerable web page. This vulnerability can have many consequences, like disclosure of a user's session cookies that could be used to impersonate the victim, or, more generally, it can allow the attacker to modify the page content seen by the victims.

This vulnerability occurs when user input is not correctly sanitized and the output is not encoded. An injection allows the attacker to send a malicious HTML page to a victim. The targeted browser will not be able to distinguish (trust) legitimate parts from malicious parts of the page, and consequently will parse and execute the whole page in the victim's context.

There is a wide range of methods and attributes that could be used to render HTML content. If these methods are provided with an untrusted input, then there is an high risk of HTML injection vulnerability. 

## How to Test

When starting to test against possible injection attack, a tester should firstly list out all the potentially vulnerable parts of the website, mainly:

- Data input fields
- Webpage link

If the above 2 exists, then manual testing can be performed by including simple HTML code as part of the input to check if HTML attributes are displayed on the page.

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/11-Client-side_Testing/03-Testing_for_HTML_Injection.md