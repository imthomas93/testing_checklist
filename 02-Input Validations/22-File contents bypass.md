# File contents bypass

|ID          |
|------------|
|GTRT-INPV-22|

## Summary

Many application’s business processes allow for the upload and manipulation of data that is submitted via files. But the business process must check the files and only allow certain “approved” file types. Deciding what files are “approved” is determined by the business logic and is application/system specific. The risk in that by allowing users to upload files, attackers may submit an unexpected file type that that could be executed and adversely impact the application or system through attacks that may deface the web site, perform remote commands, browse the system files, browse the local resources, attack other servers, or exploit the local vulnerabilities, just to name a few.

Vulnerabilities related to the upload of unexpected file types is unique in that the upload should quickly reject a file if it does not have a specific extension. Additionally, this is different from uploading malicious files in that in most cases an incorrect file format may not by it self be inherently “malicious” but may be detrimental to the saved data. For example if an application accepts Windows Excel files, if an similar database file is uploaded it may be read but data extracted my be moved to incorrect locations.

The application may be expecting only certain file types to be uploaded for processing, such as .CSV, .txt files. The application may not validate the uploaded file by extension (for low assurance file validation) or content (high assurance file validation). This may result in unexpected system or database results within the application/system or give attackers additional methods to exploit the application/system.


## How to Test

### Generic Testing Method

- Review the project documentation and perform some exploratory testing looking for file types that should be “unsupported” by the application/system.
- Try to upload these “unsupported” files an verify that it are properly rejected.
- If multiple files can be uploaded at once, there must be tests in place to verify that each file is properly evaluated.

### Specific Testing Method

- Study the applications logical requirements.
- Prepare a library of files that are “not approved” for upload that may contain files such as: jsp, exe, or HTML files containing script.
- In the application navigate to the file submission or upload mechanism.
- Submit the “not approved” file for upload and verify that they are properly prevented from uploading
- Check if the website only do file type check in client-side JavaScript
- Check if the website only check the file type by “Content-Type” in HTTP request.
- Check if the website only check by the file extension.
- Check if other uploaded files can be accessed directly by specified URL.
- Check if the uploaded file can include code or script injection.
- Check if there is any file path checking for uploaded files. Especially, hackers may compress files with specified path in ZIP so that the unzip files can be uploaded to intended path after uploading and unzip.

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/10-Business_Logic_Testing/08-Test_Upload_of_Unexpected_File_Types.md