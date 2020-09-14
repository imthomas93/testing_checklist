# Sensitive information stored in cookie in cleartext

|ID          |
|------------|
|GTRT-INFO-09|

## Summary

Attackers can use widely-available tools to view the cookie and read the sensitive information. Even if the information is encoded in a way that is not human-readable, certain techniques could determine which encoding is being used, then decode the information.

## How to Test

The following examples help to illustrate the nature of this weakness and describe methods or techniques which can be used to mitigate the risk.

Note that the examples here are by no means exhaustive and any given weakness may have many subtle varieties, each of which may require different detection methods or runtime controls.

```
response.addCookie( new Cookie("userAccountID", acctID);
```

Because the account ID is in plaintext, the user's account information is exposed if their computer is compromised by an attacker.

## References

Application Development Security 1.1/S1(f) Manage secrets securely

https://www.martellosecurity.com/kb/mitre/cwe/315/
