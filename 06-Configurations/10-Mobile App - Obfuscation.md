# Mobile App - Obfuscation

|ID          |
|------------|
|GTRT-CONF-10|

## Summary

Obfuscation is the process of transforming code and data to make it more difficult to comprehend. It is an integral part of every software protection scheme. Programs can be made incomprehensible, in whole or in part, in many ways and to different degrees.

## How to Test

Attempt to decompile the byte-code, disassemble any included library files, and perform static analysis. A common tool for decompiling Android APKs is [jadx](https://github.com/skylot/jadx).

At the very least, the app's core functionality (i.e., the functionality meant to be obfuscated) shouldn't be easily discerned. Verify that:

* Meaningful identifiers, such as class names, method names, and variable names, have been discarded,
* String resources and strings in binaries are encrypted,
* Code and data related to the protected functionality is encrypted, packed, or otherwise concealed.

## References

Application Development Security 1.1/S2 C1 (d) Obfuscate applications’ resources and information. 

[Testing Obfuscation (MSTG-RESILIENCE-9)](https://github.com/OWASP/owasp-mstg/blob/1.1.3/Document/0x05j-Testing-Resiliency-Against-Reverse-Engineering.md#testing-obfuscation-mstg-resilience-9)
