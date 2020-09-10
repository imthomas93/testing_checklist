# OS injection

|ID          |
|------------|
|GTRT-INPV-12|

## Summary

OS command injection is a technique used via a web interface in order to execute OS commands on a web server. The user supplies operating system commands through a web interface in order to execute OS commands. Any web interface that is not properly sanitized is subject to this exploit. With the ability to execute OS commands, the user can upload malicious programs or even obtain passwords. OS command injection is preventable when security is emphasized during the design and development of applications.

## How to Test

When viewing a file in a web application, the filename is often shown in the URL. Perl allows piping data from a process into an open statement. The user can simply append the Pipe symbol `|` onto the end of the filename.

### Special Characters for Comand Injection

The following special character can be used for command injection:

-  `|` 
- `;`
-  `&`
-  `$`
-  `>`
-  `<`
-  `'`
-  `!`

### Code Review Dangerous API

Uses of following API as it may introduce the command injection risks:

1. Java
   - `Runtime.exec()`
2. C/C++
   - `system`
   - `exec`
   - `ShellExecute`
3. Python
   - `exec`
   - `eval`
   - `os.system`
   - `os.popen`
   - `subprocess.popen`
   - `subprocess.call`
4. PHP
   - `system`
   - `shell_exec`
   - `exec`
   - `proc_open`
   - `eval`

### Tools

- [OWASP WebGoat](https://owasp.org/www-project-webgoat/)
- [Commix](https://github.com/commixproject/commix)

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/12-Testing_for_Command_Injection.md