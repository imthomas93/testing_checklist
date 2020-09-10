# Cross-Frame Scripting (XFS)

|ID          |
|------------|
|GTRT-INPV-17|

## Summary

Cross-Frame Scripting (XFS) is an attack that combines malicious JavaScript with an iframe that loads a legitimate page in an effort to steal data from an unsuspecting user. This attack is usually only successful when combined with social engineering. An example would consist of an attacker convincing the user to navigate to a web page the attacker controls. The attacker’s page then loads malicious JavaScript and an HTML iframe pointing to a legitimate site. Once the user enters credentials into the legitimate site within the iframe, the malicious JavaScript steals the keystrokes.

## How to Test

1. Create an HTML file with the following content: <html><body><iframe src=”http://example.com” height=”200″ width=”300″></iframe>
2. Insert the application URL in the src parameter.
3. Open the file in a browser.
4. If the application loads into the frame, it is likely vulnerable.

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

http://applicationsecurity.io/appsec-findings-database/cross-frame-scripting/