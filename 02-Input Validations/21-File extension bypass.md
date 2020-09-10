# File extension bypass

|ID          |
|------------|
|GTRT-INPV-21|

## Summary

Many application’s business processes allow users to upload data to them. Although input validation is widely understood for text-based input fields, it is more complicated to implement when files are accepted. Although many sites implement simple restrictions based on a list of permitted (or blocked) extensions, this is not sufficient to prevent attackers from uploading legitimate file types that have malicious contents.

Vulnerabilities related to the uploading of malicious files is unique in that these "malicious" files can easily be rejected through including business logic that will scan files during the upload process and reject those perceived as malicious. Additionally, this is different from uploading unexpected files in that while the file type may be accepted the file may still be malicious to the system.

Finally, "malicious" means different things to different systems, for example malicious files that may exploit SQL server vulnerabilities may not be considered as "malicious" in an environment using a NoSQL data store.

The application may allow the upload of malicious files that include exploits or shellcode without submitting them to malicious file scanning. Malicious files could be detected and stopped at various points of the application architecture such as: IPS/IDS, application server anti-virus software or anti-virus scanning by application as files are uploaded (perhaps offloading the scanning using SCAP).


## How to Test

### Generic Testing Method

- Identify the file upload functionality.
- Review the project documentation to identify what file types are considered acceptable, and what types would be considered dangerous or malicious.
  - If documentation is not available then consider what would be appropriate based on the purpose of the application.
- Determine how the uploaded files are processed.
- Obtain or create a set of "malicious" files for testing.
- Try to upload the "malicious" files to the application and determine whether it is accepted and processed.

### Malicious File Types

The simplest checks that an application can do are to determine that only trusted types of files can be uploaded.

#### Web Shells

If the server is configured to execute code, then it may be possible to obtain command execution on the server by uploading a file known as a web shell, which allows you to execute arbitrary code or operating system commands. In order for this attack to be successful, the file needs to be uploaded inside the webroot, and the server must be configured to execute the code.

Uploading this kind of shell onto an Internet facing server is dangerous, because it allows anyone who knows (or guesses) the location of the shell to execute code on the server. A number of techniques can be used to protect the shell from unauthorised access, such as:

- Uploading the shell with a randomly generated name.
- Password protecting the shell.
- Implementing IP based restrictions on the shell.

**Remember to remove the shell when you are done.**

#### Filter Evasion

The first step is to determine what the filters are allowing or blocking, and where they are implemented. If the restrictions are performed on the client-side using JavaScript, then they can be trivially bypassed with an intercepting proxy.

If the filtering is performed on the server-side, then various techniques can be attempted to bypass it, including:

- Change the value of `Content-Type` as `image/jpeg` in HTTP request.
- Change the extensions to a less common extension, such as `file.php5`, `file.shtml`, `file.asa`, `file.jsp`, `file.jspx`, `file.aspx`, `file.asp`, `file.phtml`, `file.cshtml`
- Change the capitalisation of the extension, such as `file.PhP` or `file.AspX`
- If the request includes multiple file names, change them to different values.
- Using special trailing characters such as spaces, dots or null characters such as `file.asp...`, `file.php;jpg`, `file.asp%00.jpg`, `1.jpg%00.php`
- In badly configured versions of nginx, uploading a file as `test.jpg/x.php` may allow it to be executed as `x.php`.

### Malicious File Contents

Once the file type has been validated, it is important to also ensure that the contents of the file are safe. This is significantly harder to do, as the steps required will vary depending on the types of file that are permitted.

#### Malware

Applications should generally scan uploaded files with anti-malware software to ensure that they do not contain anything malicious. The easiest way to test for this is using the [EICAR test file](https://www.eicar.org/?page_id=3950), which is an safe file that is flagged as malicious by all anti-malware software.

Depending on the type of application, it may be necessary to test for other dangerous file types, such as Office documents containing malicious macros. Tools such as the [Metasploit Framework](https://github.com/rapid7/metasploit-framework) and the [Social Engineer Toolkit (SET)](https://github.com/trustedsec/social-engineer-toolkit) can be used to generate malicious files for various formats.

When this file is uploaded, it should be detected and quarantined or deleted by the application. Depending on how the application processes the file, it may not be obvious whether this has taken place.

#### Archive Directory Traversal

If the application extracts archives (such as Zip files), then it may be possible to write to unintended locations using directory traversal. This can be exploited by uploading a malicious zip file that contains paths that traverse the file system using sequences such as `..\..\..\..\shell.php`. This technique is discussed further in the [snyk advisory](https://snyk.io/research/zip-slip-vulnerability).

#### Zip Bombs

A [Zip bomb](https://en.wikipedia.org/wiki/Zip_bomb) (more generally known as a decompression bomb) is an archive file that contains a large volume of data. It's intended to cause a denial of service by exhausting the disk space or memory of the target system that tries to extract the archive. Note that although the Zip format is the most example of this, other formats are also affected, including gzip (which is frequently used to compress data in transit).

At its simplest level, a Zip bomb can be created by compressing a large file consisting of a single character.

#### XML Files

XML files have a number of potential vulnerabilities such as XML eXternal Entities (XXE) and denial of service attacks such as the [billion laughs attack](https://en.wikipedia.org/wiki/Billion_laughs_attack).

These are discussed further in the [Testing for XML Injection](../07-Input_Validation_Testing/07-Testing_for_XML_Injection.md) guide.

#### Other File Formats

Many other file formats also have specific security concerns that need to be taken into account, such as:

- CSV files may allow [CSV injection attacks](https://owasp.org/www-community/attacks/CSV_Injection).
- Office files may contain malicious macros or PowerShell code.
- PDFs may contain malicious JavaScript.

The permitted file formats should be carefully reviewed for potentially dangerous functionality, and where possible attempts should be made to exploit this during testing.

### Source Code Review

When there is file upload feature supported, the following API/methods are common to be found in the source code.

- Java: `new file`, `import`, `upload`, `getFileName`, `Download`, `getOutputString`
- C/C++: `open`, `fopen`
- PHP: `move_uploaded_file()`, `Readfile`, `file_put_contents()`, `file()`, `parse_ini_file()`, `copy()`, `fopen()`, `include()`, `require()`

## References

Application Development Security 1.1/S1(d)  Enforce the types for query parameters

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/10-Business_Logic_Testing/09-Test_Upload_of_Malicious_Files.md