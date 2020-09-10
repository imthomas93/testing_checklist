# Reflected file download (RFD)

|ID          |
|------------|
|GTRT-INPV-24|

## Summary

Reflected File Download(RFD) is an attack technique which might enables attacker to gain complete access over a victim’s machine by virtually downloading a file from a trusted domain (like Google.com & Bing.com).This web attack technique has been discovered by Oren Hafif, a Trustwave SpiderLabs security researcher in 2014.

## How to Test

Reflected File Download (RFD) is a vulnerability that allows an attacker to craft a phishing URL or page that, when visited, initiates a download of a file containing arbitrary content appearing to have originated from a trusted domain. Because the user has trust in the given domain, he or she is likely to open the downloaded file, potentially resulting in malicious code execution.

In order for an attacker to run a successful RFD attack, the following requirements need to be met:
- The target application reflects user input without proper validation or encoding. This is used to inject a payload.
- The target application allows permissive URLs. The attacker may therefore control the downloaded file's name and extension.
- The target application has a misconfigured Content-Disposition header, allows the attacker to control the Content-Type and/or Content-Disposition headers in the HTTP response, or the target application includes a Content-Type that is not rendered by default in the browser.

For example, if the application uses a Spring Web MVC ContentNegotiationManager to dynamically produce different response formats, it meets the conditions necessary to make an RFD attack possible.

The ContentNegotiationManager is configured to decide the response format based on the request path extension and to use Java Activation Framework (JAF) to find a Content-Type that better matches the client's requested format. It also allows the client to specify the response content type through the media type that is sent in the request's Accept header.

JSON and JSONP APIs are also check points for RFD, most of the modern web applications are using this techniques.With help of tools like Burp Suite or OWASP zap you will be able to find the candidates for testing.

RFD testing can be divided into 3: Reflected, Filename & Download.

### 1. Reflected

Step 1 : Validate the response of JSON/JSONP APIs and check whether any user input is getting reflected.

Request
```
https://some.website.com/api/v1.0/get_user_profile
```

Response
```
{
“data”: {
“id”: “1239985”,
“domain”: “website.com”,
“ph”: “6456787984”,
“first_name”: “DemoTest”,
“last_name”: “LastRFD”,
“version”: “5”,
}
```
You can see that first_name, last_name and ph are getting reflected in the JSON response.

Step 2 : Now, enter the RFD payload rfd”||calc|| into first_name and last_name field. Validate the JSON/JSONP response, if its reflected back like rfd\”||calc|| then there is possibility of RFD.
To verify it completely, copy and save the response as filename.bat . Open it with cmd prompt , you can see window calc is getting popped up.

### Filename

If we are hitting the JSON/JSONP API url in IE 11 we can see that response will get downloaded as somefileName.json. Filename dependents mainly on http Content-Disposition header and URL.

To exploit this vulnerability, we should be able to change the file format to .cmd, .bat or .exe in order to get executed. How?

Ex: 
```
Content-Disposition: userprofile.json
```

File will be downloaded with same name mentioned in the Content-Disposition header. So we can’t exploit it. We need to move to next possibility like response without Content-Disposition header.
In the absence of a filename attribute returned within a Content-Disposition response header, browsers are forced to determine the name of a downloaded file based on the URL.

### Download

```
<body>
<a href=”https://some.website.com/api/v1.0/get_user_profile/setup.cmd?" download><img border=”0" src=”https://some.website.com/api/v1.0/get_user_profile/setup.cmd?" alt=”8000 Dollars” width=”104" height=”142"></a>
</body>
```
Open the html page click the link, file will be downloaded as setup.cmd.


## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

https://vulncat.fortify.com/en/detail?id=desc.config.java.reflected_file_download

https://medium.com/@Johne_Jacob/rfd-reflected-file-download-what-how-6d0e6fdbe331