# Hidden / undocumented directories

|ID          |
|------------|
|GTRT-CONF-06|

## Summary

There is essentially no way for a user to know which files are found in which directories on a web-server, unless the whole server has directory listing by default. However, if you go directly to the page it will be shown. So what the attacker can do is to brute force hidden files and directories. Just test a bunch of them. There are several tools for doing this. The attack is of course very noisy and will show up fast in the logs.


## How to Test

1. Dirb
2. Dirbuster
3. OWASP ZAP
4. Wfuzz
5. Gobuster

## References

Application Development Security 1.1/S1(j) Remove resources and services when they are not in used

https://chryzsh.gitbooks.io/pentestbook/content/web-scanning.html
