# Uploaded path bypass

|ID          |
|------------|
|GTRT-INPV-23|

## Summary

Many application’s business processes allow users to upload data to them. Although input validation is widely understood for text-based input fields, it is more complicated to implement when files are accepted. Although many sites implement simple restrictions based on a list of permitted (or blocked) extensions, this is not sufficient to prevent attackers from uploading legitimate file types that have malicious contents.

Vulnerabilities related to the uploading of malicious files is unique in that these "malicious" files can easily be rejected through including business logic that will scan files during the upload process and reject those perceived as malicious. Additionally, this is different from uploading unexpected files in that while the file type may be accepted the file may still be malicious to the system.

Finally, "malicious" means different things to different systems, for example malicious files that may exploit SQL server vulnerabilities may not be considered as "malicious" in an environment using a NoSQL data store.

The application may allow the upload of malicious files that include exploits or shellcode without submitting them to malicious file scanning. Malicious files could be detected and stopped at various points of the application architecture such as: IPS/IDS, application server anti-virus software or anti-virus scanning by application as files are uploaded (perhaps offloading the scanning using SCAP).

## How to Test

### Archive Directory Traversal

If the application extracts archives (such as Zip files), then it may be possible to write to unintended locations using directory traversal. This can be exploited by uploading a malicious zip file that contains paths that traverse the file system using sequences such as `..\..\..\..\shell.php`. This technique is discussed further in the [snyk advisory](https://snyk.io/research/zip-slip-vulnerability).

### Zip Bombs

A [Zip bomb](https://en.wikipedia.org/wiki/Zip_bomb) (more generally known as a decompression bomb) is an archive file that contains a large volume of data. It's intended to cause a denial of service by exhausting the disk space or memory of the target system that tries to extract the archive. Note that although the Zip format is the most example of this, other formats are also affected, including gzip (which is frequently used to compress data in transit).

At its simplest level, a Zip bomb can be created by compressing a large file consisting of a single character.


## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/10-Business_Logic_Testing/09-Test_Upload_of_Malicious_Files.md
