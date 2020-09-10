# XXE Injection

|ID          |
|------------|
|GTRT-INPV-06|

## Summary

XML external entity injection (also known as XXE) is a web security vulnerability that allows an attacker to interfere with an application's processing of XML data. It often allows an attacker to view files on the application server filesystem, and to interact with any back-end or external systems that the application itself can access.

In some situations, an attacker can escalate an XXE attack to compromise the underlying server or other back-end infrastructure, by leveraging the XXE vulnerability to perform server-side request forgery (SSRF) attacks.

There are various types of XXE attacks:

- Exploiting XXE to retrieve files - where an external entity is defined containing the contents of a file, and returned in the application's response.
- Exploiting XXE to perform SSRF attacks - where an external entity is defined based on a URL to a back-end system.
- Exploiting blind XXE exfiltrate data out-of-band - where sensitive data is transmitted from the application server to a system that the attacker controls.
- Exploiting blind XXE to retrieve data via error messages - where the attacker can trigger a parsing error message containing sensitive data.

## How to Test

Manually testing for XXE vulnerabilities generally involves:

- Testing for file retrieval by defining an external entity based on a well-known operating system file and using that entity in data that is returned in the application's response.
- Testing for blind XXE vulnerabilities by defining an external entity based on a URL to a system that you control, and monitoring for interactions with that system. 
- Testing for vulnerable inclusion of user-supplied non-XML data within a server-side XML document by using an XInclude attack to try to retrieve a well-known operating system file.

### Source Code Review

The following Java API may be vulnerable to XXE if they are not configured properly.

- javax.xml.parsers.DocumentBuilder
- javax.xml.parsers.DocumentBuildFactory
- org.xml.sax.EntityResolver
- org.dom4j.*
- javax.xml.parsers.SAXParser
- javax.xml.parsers.SAXParserFactory
- TransformerFactory
- SAXReader
- DocumentHelper
- SAXBuilder
- SAXParserFactory
- XMLReaderFactory
- XMLInputFactory
- SchemaFactory
- DocumentBuilderFactoryImpl
- SAXTransformerFactory
- DocumentBuilderFactoryImpl
- XMLReader
- Xerces: DOMParser, DOMParserImpl, SAXParser, XMLParser

In addition, the Java POI office reader may be vulnerable to XXE if the version is under 3.10.1.

The version of POI library can be identified from the filename of the JAR. For example,

- poi-3.8.jar
- poi-ooxml-3.8.jar

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://portswigger.net/web-security/xxe