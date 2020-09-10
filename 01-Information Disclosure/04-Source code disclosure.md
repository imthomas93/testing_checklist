# Source Code Disclosure

|ID          |
|------------|
|GTRT-INFO-04|

## Summary

It is very common, and even recommended, for programmers to include detailed comments and metadata on their source code. However, comments and metadata included into the HTML code might reveal internal information that should not be available to potential attackers. Comments and metadata review should be done in order to determine if any information is being leaked.

For modern web apps, the use of client-Side JavaScript for the front-end is becoming more popular. Popular front-end construction technologies use client-side JavaScript like ReactJS, AngularJS, or Vue.  Similar to the comments and metadata in HTML code, many programmers also hardcod sensitive information in JavaScript variables on the front-end. Sensitive information can include (but is not limited to): Private API Keys (*e.g.* an unrestricted Google Map API Key), internal IP addresses, sensitive routes (*e.g.* route to hidden admin pages or functionality), or even credentials. This sensitive information can be leaked from such front-end JavaScript code. A review should be done in order to determine if any sensitive information leaked which could be used by attackers for abuse.

For large web applications, performance issues are a big concern to programmers. Programmers have used different methods to optimize front-end performance, including Syntactically Awesome Style Sheets (SASS), Sassy CSS (SCSS), webpack, etc. Using these technologies, front-end code will sometimes become harder to understand and difficult to debug, and because of it, programmers often deploy source map files for debugging purposes. A “source map” is a special file that connects a minified/uglified version of an asset (CSS or JavaScript) to the original authored version. Programmers are still debating whether or not to bring source map files to the production environment. However, it is undeniable that source map files or files for debugging if released to the production environment will make their source more human-readable. It can make it easier for attackers to find vulnerabilities from the front-end or collect sensitive information from it. JavaScript code review should be done in order to determine if any debug files are exposed from the front-end. Depending on the context and sensitivity of the project, a security expert should decide whether the files should exist in the production environment or not.


## How to Test

* Review webpage comments and metadata to better understand the application and to find any information leakage.
* Identify and gather JavaScript files, review JavaScript code in an application to better understand the application and to find any information leakage.
* Identify if source map files or other front-end debug files exist.

### Review webpage comments and metadata

HTML comments are often used by the developers to include debugging information about the application. Sometimes, they forget about the comments and they leave them in production environments. Testers should look for HTML comments which start with `<!--`.

Check HTML source code for comments containing sensitive information that can help the attacker gain more insight about the application. It might be SQL code, usernames and passwords, internal IP addresses, or debugging information.

```
<!-- Query: SELECT id, name FROM app.users WHERE active='1' -->
```

Some `META` tags do not provide active attack vectors but instead allow an attacker to profile an application:

```html
<META name="Author" content="Andrew Muller">
```

A common (but not [WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/) compliant) `META` tag is [Refresh](https://en.wikipedia.org/wiki/Meta_refresh).

```html
<META http-equiv="Refresh" content="15;URL=https://www.owasp.org/index.html">
```

Although most web servers manage search engine indexing via the `robots.txt` file, it can also be managed by `META` tags. The tag below will advise robots to not index and not follow links on the HTML page containing the tag.

```html
<META name="robots" content="none">
```

### Identifying JavaScript Code and Gathering JavaScript Files

Programmers often hardcode sensitive information with JavaScript variables on the front-end. Testers should check HTML source code and look for JavaScript code between `<script>` and `</script>` tags. Testers should also identify external JavaScript files to review the code (JavaScript files have the file extension `.js` and name of the JavaScript file usually put in the `src` (source) attribute of a `<script>` tag).

Check JavaScript code for any sensitive information leaks which could be used by attackers to further abuse or manipulate the system. Look for values such as: API keys, internal IP addresses, sensitive routes, or credentials.

The tester may even find something like this:

```
var conString = "tcp://postgres:1234@localhost/postgres";
```

When an API Key is found, testers can check if the API Key restrictions are set per service or by IP, HTTP referrer, application, SDK, etc.

For example, if testers found a Google Map API Key, they can check if this API Key is restricted by IP or restricted only per the Google Map APIs. If the Google API Key is restricted only per the Google Map APIs, attackers can still use that API Key to query unrestricted Google Map APIs and the application owner must to pay for that.

```
{"GOOGLE_MAP_API_KEY":"AIzaSyDUEBnKgwiqMNpDplT6ozE4Z0XxuAbqDi4", "RECAPTCHA_KEY":"6LcPscEUiAAAAHOwwM3fGvIx9rsPYUq62uRhGjJ0"}

```

In some cases, testers may find sensitive routes from JavaScript code, such as links to internal or hidden admin pages.
```
"runtimeConfig":{"BASE_URL_VOUCHER_API":"https://staging-voucher.victim.net/api", "BASE_BACKOFFICE_API":"https://10.10.10.2/api", "ADMIN_PAGE":"/hidden_administrator"}
```

When websites load source map files, the front-end source code will become readable and easier to debug.


## References

Application Development Security 1.1/S1(l) Prevent the disclosure of sensitive information or credentials in error response and logs

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/01-Information_Gathering/05-Review_Webpage_Content_for_Information_Leakage.md