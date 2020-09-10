# CSV injection

|ID          |
|------------|
|GTRT-INPV-11|

## Summary

Popular spreadsheet processors such as Apache OpenOffice Calc and Microsoft Office Excel support powerful formula operations that might enable attackers in control of the spreadsheet to run arbitrary commands on the underlying system or leak sensitive information on the spreadsheet.

## How to Test

The meta-characters for Microsoft Excel that signal the start of a formula are: **=, +, -. or @**, and their appearance at the start of a CSV cell value can be used to detect the injection of malicious content.

Inject the following payload as part of a CSV field: `=cmd|'/C calc.exe'!Z0`. If the user who opens the spreadsheet trusts the origin of the document, they might accept all the security prompts presented by the spreadsheet processor and let the payload run on their system, resulting in calculator.exe being opened as specified by the payload.

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://vulncat.fortify.com/en/detail?id=desc.dataflow.java.formula_injection