# Mobile App - Anti-tampering

|ID          |
|------------|
|GTRT-CONF-03|

## Summary

Reverse engineers use a lot of tools, frameworks, and apps. The presence of such tools on the device may indicate that a user is attempting to reverse engineer the app. 

Such tools can be used to make unwanted changes to the application, such as changes to binary code, byte-code, function pointer tables, and important data structures, as well as rogue code loaded into process memory.

Some tools commonly use include:
* Substrate for Android
* Xposed
* Frida
* Drozer
* RootCloak
* Android SSL Trust Killer

## How to Test

Launch the app with various apps and frameworks installed. The app should respond in some way to the presence of each of those tools with any of the following methods:
1. The application closes immediately, without any notification.
2. A pop-up window indicates that the application won't run on the device.

In the case of Frida, the frida-server tool should be started on the device prior to launching the application



## References

Application Development Security 1.1/S2 C1 (c) Implement anti-tampering measures and disable the use of applications when tampering attempts are detected; and 

[Testing Reverse Engineering Tools Detection (MSTG-RESILIENCE-4)](https://github.com/OWASP/owasp-mstg/blob/1.1.3/Document/0x05j-Testing-Resiliency-Against-Reverse-Engineering.md#testing-reverse-engineering-tools-detection-mstg-resilience-4)

[Testing Run Time Integrity Checks (MSTG-RESILIENCE-6)](https://github.com/OWASP/owasp-mstg/blob/1.1.3/Document/0x05j-Testing-Resiliency-Against-Reverse-Engineering.md#testing-run-time-integrity-checks-mstg-resilience-6)