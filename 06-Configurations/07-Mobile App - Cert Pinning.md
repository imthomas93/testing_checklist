# Mobile App - Cert Pinning

|ID          |
|------------|
|GTRT-CONF-07|

## Summary

Certificate pinning is the process of associating the backend server with a particular X.509 certificate or public key instead of accepting any certificate signed by a trusted certificate authority. After storing ("pinning") the server certificate or public key, the mobile app will subsequently connect to the known server only. Withdrawing trust from external certificate authorities reduces the attack surface (after all, there are many cases of certificate authorities that have been compromised or tricked into issuing certificates to impostors).

The certificate can be pinned and hardcoded into the app or retrieved at the time the app first connects to the backend. In the latter case, the certificate is associated with ("pinned" to) the host when the host is seen for the first time. This alternative is less secure because attackers intercepting the initial connection can inject their own certificates.

## How to Test

* Launch a MITM attack with an interception proxy. An example tool is Burp Suite
* Monitor the traffic between the client (mobile application) and backend server
* If the proxy is unable to intecept the HTTP requests and responses, the SSL pinning has been implemented correctly. 
    * In Burp Suite, the 'Alerts' tab would indicate that the client has failed to negotiate connection

## References

Application Development Security 1.1/S2 C1 (a) Implement certificate pinning to mitigate man-in-the-middle attack

[Testing Custom Certificate Stores and Certificate Pinning (MSTG-NETWORK-4) [Android]](https://github.com/OWASP/owasp-mstg/blob/1.1.3/Document/0x05g-Testing-Network-Communication.md#testing-custom-certificate-stores-and-certificate-pinning-mstg-network-4)

[Testing Custom Certificate Stores and Certificate Pinning (MSTG-NETWORK-3 and MSTG-NETWORK-4) [iOS]](https://github.com/OWASP/owasp-mstg/blob/1.1.3/Document/0x06g-Testing-Network-Communication.md#testing-custom-certificate-stores-and-certificate-pinning-mstg-network-3-and-mstg-network-4)
