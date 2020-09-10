# Internal IP Revealed

|ID          |
|------------|
|GTRT-INFO-02|

## Summary

This web server leaks a private IP address through its HTTP headers.

This may expose internal IP addresses that are usually hidden or masked behind a Network Address Translation (NAT) Firewall or proxy server.

There is a known issue with Microsoft IIS 4.0 doing this in its default configuration. This may also affect other web servers, web applications, web proxies, load balancers and through a variety of misconfigurations related to redirection.

## How to Test

To test this vulnerability, it is basically the same procedure as the previous one; But, this time we are sending our GET request to the root of the webserver instead of autodiscover.xml.

Connect to your exchange server using OpenSSL as below.

```openssl s_client -host host.domain.com -port 443```

Then send this GET request to the root page of the webserver.

```GET / HTTP/1.0```

Notice the response kindly lets you know the Internal IP in the Location: header.

## References

Application Development Security 1.1/S1(l) Prevent the disclosure of sensitive information or credentials in error response and logs

https://www.tenable.com/plugins/nessus/10759

https://securitytutorials.co.uk/http-header-internal-ip-disclosure/