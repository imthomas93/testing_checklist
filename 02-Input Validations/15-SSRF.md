# SSRF

|ID          |
|------------|
|GTRT-INPV-15|

## Summary

In a Server-Side Request Forgery (SSRF) attack, the attacker can abuse functionality on the server to read or update internal resources. The attacker can supply or a modify a request which the code running on the server will process. By carefully selecting the details, the attacker may be able to read server configuration such as AWS metadata, connect to internal services like HTTP enabled databases, or perform POST requests towards internal services which are not intended to be exposed.

## How to Test

### Case I: Endpoints Which Fetch External/Internal Resources

With GET request:

- `http://example.com/index.php?page=about.php`
- `http://example.com/index.php?page=https://attackersite.com`
- `http://example.com/index.php?page=file:///etc/passwd`

With POST request:

```
POST /test/ssrf_form.php HTTP/1.1
Host: example.com

url=https://hacker.com/as&name2=value2
```

### Case II: PDF Generators

There are some cases where server converts uploaded file to a pdf. Try injecting `<iframe>`, `<img>`, `<base>` or `<script>` elements or CSS url() functions pointing to internal services.

### Tools

- [Burpsuite](https://portswigger.net/burp)
- [ZAP](https://www.zaproxy.org/)

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/e715058efb0179e0787fcd27f2a244a797d16500/Testing_for_Server-Side_Request_Forgery.md