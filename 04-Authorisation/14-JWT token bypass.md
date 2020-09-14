# JWT token bypass (e.g., algorithm type, signature validation, bruteforce secret keys, KID manipulation)

|ID          |
|------------|
|GTRT-ATHZ-14|

## Summary

JSON web tokens are a type of access tokens that are widely used in commercial applications. They are based on the JSON format and includes a token signature to ensure the integrity of the token. 

When implemented correctly, JSON web tokens provide a secure way to identify the user since the data contained in the payload section cannot be tampered with. (Since the user does not have access to the secret key, the user is unable to sign the token.)

But if implemented incorrectly, there are ways that an attacker can bypass the security mechanism and forge arbitrary tokens.

## How to Test

### Change the algorithm type

One of the ways that attackers can forge their own tokens is by tampering with the alg field of the header. If the application does not restrict the algorithm type used in the JWT, an attacker can specify which algorithm to use, which could compromise the security of the token.

#### None Algorithm

JWT supports a “none” algorithm. If the alg field is set to “none”, any token would be considered valid if their signature section is set to empty. For example, the following token would be considered valid:

`eyAiYWxnIiA6ICJOb25lIiwgInR5cCIgOiAiSldUIiB9Cg.eyB1c2VyX25hbWUgOiBhZG1pbiB9Cg`

Below is the decoded version, with no signature present:

`
{
 "alg" : "none",
 "typ" : "JWT"
}
{
 "user" : "admin"
}
`

### HMAC algorithm

The two most common types of algorithms used for JWTs are HMAC and RSA. With HMAC, the token would be signed with a key, then later verified with the same key. As for RSA, the token would first be created with a private key, then verified with the corresponding public key.

For a JWT that is signed using RSA, the *alg* can be changed to used HMAC. Valid tokens can be created by signing the newly forged tokens with the RSA public key

#### Providing a non-valid signature

It is possible that the signature of a token is never verified. The security mechanism can be bypassed by simply providing an invalid signature

### Bruteforcing the value of key parameter

JWT token using HS256 algorithm for signature can be susceptible to bruteforce attack . Sometimes weak secret key is being used on server side to sign the jwt token using HS256 algorithm. This gives attacker a possibility to bruteforce a list secret keys against a given valid token.

Once the actual key has been derived the used could easily manipulate the value of payload header and generate a valid signature.

A tool that may be helpful is already present at the github https://github.com/rxall/jwt-cracker. It involves the use of pyjwt library to generate and compare signature for given list of keys.

### Manipulating the KID parameter

KID stands for “Key ID”. It is an optional header field in JWTs, and it allows developers to specify the key to be used for verifying the token.

### Directory Traversal

Since the KID is often used to retrieve a key file from the file system, if it is not sanitized before use, it can lead to a directory traversal attack. When this is the case, the attacker would be able to specify any file in the file system as the key to be used to verify the token.

For example, the attacker can force the application into using a publicly available file as the key, and sign an HMAC token using that file.

### SQL Injection

The KID could also be used to retrieve the key from a database. In this case, it might be possible to utilize SQL injection to bypass JWT signing.

If SQL injection is possible on the KID parameter, the attacker can use this injection to return any value.

`
“kid”: "aaaaaaa' UNION SELECT 'key';--"
// use the string "key" to verify the token
`

For example, this above injection will cause the application to return the string “key” (since the key named “aaaaaaa” doesn’t exist in the database). The token will then be verified with the string “key” as the secret key.

## References

Application Development Security 1.1/S1(a) Manage logon session and access controls securely

https://medium.com/swlh/hacking-json-web-tokens-jwts-9122efe91e4a

https://medium.com/@cyb3rlant3rn/jwt-token-bypass-f12a2e63622a
