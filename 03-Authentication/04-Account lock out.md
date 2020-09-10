# Account lock out

|ID          |
|------------|
|GTRT-ATHN-04|

## Summary

Account lockout mechanisms are used to mitigate brute force password guessing attacks. Accounts are typically locked after 3 to 5 unsuccessful login attempts and can only be unlocked after a predetermined period of time, via a self-service unlock mechanism, or intervention by an administrator. Account lockout mechanisms require a balance between protecting accounts from unauthorized access and protecting users from being denied authorized access.

Note that this test should cover all aspects of authentication where lockout mechanisms would be appropriate, e.g. when the user is presented with security questions during forgotten password mechanisms (see [Testing for Weak security question/answer](08-Testing_for_Weak_Security_Question_Answer.md)).

Without a strong lockout mechanism, the application may be susceptible to brute force attacks. After a successful brute force attack, a malicious user could have access to:

- Confidential information or data: Private sections of a web application could disclose confidential documents, users' profile data, financial information, bank details, users' relationships, etc.
- Administration panels: These sections are used by webmasters to manage (modify, delete, add) web application content, manage user provisioning, assign different privileges to the users, etc.
- Opportunities for further attacks: authenticated sections of a web application could contain vulnerabilities that are not present in the public section of the web application and could contain advanced functionality that is not available to public users.

## How to Test

Typically, to test the strength of lockout mechanisms, you will need access to an account that you are willing or can afford to lock. If you have only one account with which you can log on to the web application, perform this test at the end of you test plan to avoid that you cannot continue your testing due to a locked account.

To evaluate the account lockout mechanism's ability to mitigate brute force password guessing, attempt an invalid log in by using the incorrect password a number of times, before using the correct password to verify that the account was locked out. An example test may be as follows:

1. Attempt to log in with an incorrect password 3 times.
2. Successfully log in with the correct password, thereby showing that the lockout mechanism doesn't trigger after 3 incorrect authentication attempts.
3. Attempt to log in with an incorrect password 4 times.
4. Successfully log in with the correct password, thereby showing that the lockout mechanism doesn't trigger after 4 incorrect authentication attempts.
5. Attempt to log in with an incorrect password 5 times.
6. Attempt to log in with the correct password. The application returns “Your account is locked out.”, thereby confirming that the account is locked out after 5 incorrect authentication attempts.
7. Attempt to log in with the correct password 5 minutes later. The application returns “Your account is locked out.”, thereby showing that the lockout mechanism does not automatically unlock after 5 minutes.
8. Attempt to log in with the correct password 10 minutes later. The application returns “Your account is locked out.”, thereby showing that the lockout mechanism does not automatically unlock after 10 minutes.
9. Successfully log in with the correct password 15 minutes later, thereby showing that the lockout mechanism automatically unlocks after a 10 to 15 minute period.

## References

Application Development Security 2.2/S1 (j) Lock the system account upon 10 consecutive failed authentication attempts. 

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/04-Authentication_Testing/03-Testing_for_Weak_Lock_Out_Mechanism.md