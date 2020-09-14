# Hardcoded plaintext credentials in files / web pages / scripts

|ID          |
|------------|
|GTRT-INFO-08|

## Summary

Embedded credentials, also often referred to as hardcoded credentials, are plain text credentials in source code. Password/credential hardcoding refers to the practice of embedding plain text (non-encrypted) credentials (account passwords, SSH Keys, DevOps secrets, etc.) into source code.

However, the practice of hardcoding credentials is increasingly discouraged as it poses formidable security risks that are routinely exploited by malware and hackers. In some cases, a threat actor (perhaps aligned with a nation-state) may insert hardcoded credentials to create a backdoor, allowing them persistent access to a device, application, or system.

## How to Test

Manufacturers and software companies commonly hardcode passwords into hardware, firmware, software, IoT and other devices, scripts, applications, and systems because it helps to simplify deployments at scale. Developers and other users may also embed credentials into code, for easy access as part of their workflow.

Proponents of hardcoding credentials also claim it provides an extra layer of assurance so that unsophisticated users cannot tamper with the code or product.

Passwords are commonly embedded in:

- Software applications, both locally installed and cloud-based
- BIOS and other firmware across computers, mobile devices, servers, printers, etc.
- Internet of Things (IoT) devices and medical devices
- DevOps tools
- Network switches, routers, and other control systems (SCADA, etc.)
- Embedded passwords are routinely used for:

Setting up new systems
- API and other system integrations
- Encryption and decryption keys
- Privileged and superuser access
- Application-to-Application (a2a) and Application-to-Database communications

## References

Application Development Security 1.1/S1(f) Manage secrets securely

https://www.beyondtrust.com/blog/entry/hardcoded-and-embedded-credentials-are-an-it-security-hazard-heres-what-you-need-to-know#:~:text=Embedded%20credentials%2C%20also%20often%20referred,into%20source%20code.
