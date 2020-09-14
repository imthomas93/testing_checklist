# Mobile App - Detect root / jailbroken devices

|ID          |
|------------|
|GTRT-CONF-08|

## Summary

In the context of anti-reversing, the goal of root/jailbreak detection is to make running the app on a rooted/jailbroken device a bit more difficult. This blocks some of the tools and techniques reverse engineers like to use. Like most other defenses, root/jailbreak detection is not very effective by itself, but implementing multiple checks that are scattered throughout the app can improve the effectiveness of the overall anti-tampering scheme.

For Android, we define "root detection" a bit more broadly, including custom ROMs detection, i.e., determining whether the device is a stock Android build or a custom build.

## How to Test

Start the application on a rooted/jailbroken device, and observe if the application performs any of the following:
1. The application closes immediately, without any notification.
2. A pop-up window indicates that the application won't run on the device.

## References

Application Development Security 1.1/S2 C1 (b) Disable the use of applications on rooted/jailbroken devices;

[Testing Root Detection (MSTG-RESILIENCE-1) [Android]](https://github.com/OWASP/owasp-mstg/blob/1.1.3/Document/0x05j-Testing-Resiliency-Against-Reverse-Engineering.md#testing-root-detection-mstg-resilience-1)

[Jailbreak Detection (MSTG-RESILIENCE-1) [iOS]](https://github.com/OWASP/owasp-mstg/blob/1.1.3/Document/0x06j-Testing-Resiliency-Against-Reverse-Engineering.md#jailbreak-detection-mstg-resilience-1)
