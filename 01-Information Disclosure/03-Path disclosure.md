# Path Disclosure (e.g., server, web, app)

|ID          |
|------------|
|GTRT-INFO-03|

## Summary

Before commencing security testing, understanding the structure of the application is paramount. Without a thorough understanding of the layout of the application, it is unlikely that it will be tested thoroughly.

## How to Test

In black-box testing it is extremely difficult to test the entire codebase. Not just because the tester has no view of the code paths through the application, but even if they did, to test all code paths would be very time consuming. One way to reconcile this is to document what code paths were discovered and tested.

There are several ways to approach the testing and measurement of code coverage:

- **Path** - test each of the paths through an application that includes combinatorial and boundary value analysis testing for each decision path. While this approach offers thoroughness, the number of testable paths grows exponentially with each decision branch.
- **Data Flow (or Taint Analysis)** - tests the assignment of variables via external interaction (normally users). Focuses on mapping the flow, transformation and use of data throughout an application.
- **Race** - tests multiple concurrent instances of the application manipulating the same data.

The trade off as to what method is used and to what degree each method is used should be negotiated with the application owner. Simpler approaches could also be adopted, including asking the application owner what functions or code sections they are particularly concerned about and how those code segments can be reached.

### Black-Box Testing

To demonstrate code coverage to the application owner, the tester can start with a spreadsheet and document all the links discovered by spidering the application (either manually or automatically). Then the tester can look more closely at decision points in the application and investigate how many significant code paths are discovered. These should then be documented in the spreadsheet with URLs, prose and screenshot descriptions of the paths discovered.

### Gray-Box or White-Box Testing

Ensuring sufficient code coverage for the application owner is far easier with gray-box and white-box approach to testing. Information solicited by and provided to the tester will ensure the minimum requirements for code coverage are met.

### Tools

- [Zed Attack Proxy (ZAP)](https://github.com/zaproxy/zaproxy)
- [List of spreadsheet software](https://en.wikipedia.org/wiki/List_of_spreadsheet_software)
- [Diagramming software](https://en.wikipedia.org/wiki/List_of_concept-_and_mind-mapping_software)


## References

Application Development Security 1.1/S1(l) Prevent the disclosure of sensitive information or credentials in error response and logs

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/01-Information_Gathering/07-Map_Execution_Paths_Through_Application.md