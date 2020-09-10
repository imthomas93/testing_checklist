# XML Injection

|ID          |
|------------|
|GTRT-INPV-05|

## Summary

XML Injection testing is when a tester tries to inject an XML doc to the application. If the XML parser fails to contextually validate data, then the test will yield a positive result.

## How to Test

### Discovery

The first step in order to test an application for the presence of a XML Injection vulnerability consists of trying to insert XML metacharacters.

XML metacharacters are:

- Single quote - When not sanitized, this character could throw an exception during XML parsing, if the injected value is going to be part of an attribute value in a tag.
- Double quote - this character has the same meaning as single quote and it could be used if the attribute value is enclosed in double quotes.
- Angular parentheses - By adding an open or closed angular parenthesis in a user input, the application will build a new node. However, in the presence of an open '<', the resulting XML document will be invalid.
- Comment tag - This sequence of characters is interpreted as the beginning/end of a comment. 
- Ampersand - The ampersand is used in the XML syntax to represent entities. The format of an entity is `&symbol;`. An entity is mapped to a character in the Unicode character set.
- CDATA section delimiters - CDATA sections are used to escape blocks of text containing characters which would otherwise be recognized as markup. In other words, characters enclosed in a CDATA section are not parsed by an XML parser.

### Tag Injection

After discovery, the tester will have some information about the structure of the XML document. Then, it is possible to try to inject XML data and tags.

### Source Code Review

Check source code if the docType, external DTD, and external parameter entities are set as forbidden uses.

The followings source code keyword may apply to C.

- libxml2: xmlCtxtReadMemory,xmlCtxtUseOptions,xmlParseInNodeContext,xmlReadDoc,xmlReadFd,xmlReadFile ,xmlReadIO,xmlReadMemory, xmlCtxtReadDoc ,xmlCtxtReadFd,xmlCtxtReadFile,xmlCtxtReadIO
- libxerces-c: XercesDOMParser, SAXParser, SAX2XMLReader

### Tools

- [XML Injection Fuzz Strings (from wfuzz tool)](https://github.com/xmendez/wfuzz/blob/master/wordlist/Injections/XML.txt)

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/07-Testing_for_XML_Injection.md