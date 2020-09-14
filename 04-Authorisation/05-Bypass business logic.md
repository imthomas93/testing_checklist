# Bypass business logic (e.g., interity of data, SOD, feature misuse)

|ID          |
|------------|
|GTRT-ATHZ-05|

## Summary

The application must ensure that only logically valid data can be entered at the front end as well as directly to the server-side of an application of system. Only verifying data locally may leave applications vulnerable to server injections through proxies or at handoffs with other systems. This is different from simply performing Boundary Value Analysis (BVA) in that it is more difficult and in most cases cannot be simply verified at the entry point, but usually requires checking some other system.

For example: An application may ask for your Social Security Number. In BVA the application should check formats and semantics (is the value 9 digits long, not negative and not all 0's) for the data entered, but there are logic considerations also. SSNs are grouped and categorized. Is this person on a death file? Are they from a certain part of the country?

Vulnerabilities related to business data validation is unique in that they are application specific and different from the vulnerabilities related to forging requests in that they are more concerned about logical data as opposed to simply breaking the business logic workflow.

The front end and the back end of the application should be verifying and validating that the data it has, is using and is passing along is logically valid. Even if the user provides valid data to an application the business logic may make the application behave differently depending on data or circumstances.

## How to Test

- Review the project documentation and use exploratory testing looking for data entry points or hand off points between systems or software.
- Once found try to insert logically invalid data into the application/system.
Specific Testing Method:
- Perform front-end GUI Functional Valid testing on the application to ensure that the only “valid” values are accepted.
- Using an intercepting proxy observe the HTTP POST/GET looking for places that variables such as cost and quality are passed. Specifically, look for “hand-offs” between application/systems that may be possible injection or tamper points.
- Once variables are found start interrogating the field with logically “invalid” data, such as social security numbers or unique identifiers that do not exist or that do not fit the business logic. This testing verifies that the server functions properly and does not accept logically invalid data.

### Related Test Cases

All [Input Validation](../07-Input_Validation_Testing/README.md) test cases.

- [Testing for Account Enumeration and Guessable User Account](../03-Identity_Management_Testing/04-Testing_for_Account_Enumeration_and_Guessable_User_Account.md).
- [Testing for Bypassing Session Management Schema](../06-Session_Management_Testing/01-Testing_for_Session_Management_Schema.md).
- [Testing for Exposed Session Variables](../06-Session_Management_Testing/04-Testing_for_Exposed_Session_Variables.md).

### Tools

[OWASP Zed Attack Proxy (ZAP)](https://www.zaproxy.org)

## References

Application Development Security 1.1/S1(a) Manage logon session and access controls securely

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/10-Business_Logic_Testing/01-Test_Business_Logic_Data_Validation.md
