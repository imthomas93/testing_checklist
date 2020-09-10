# Session expiration (e.g., session did not expire/invalidated after logout)

|ID          |
|------------|
|GTRT-ATHZ-11|

## Summary

In this phase testers check that the application automatically logs out a user when that user has been idle for a certain amount of time, ensuring that it is not possible to “reuse” the same session and that no sensitive data remains stored in the browser cache.

All applications should implement an idle or inactivity timeout for sessions. This timeout defines the amount of time a session will remain active in case there is no activity by the user, closing and invalidating the session upon the defined idle period since the last HTTP request received by the web application for a given session ID. The most appropriate timeout should be a balance between security (shorter timeout) and usability (longer timeout) and heavily depends on the sensitivity level of the data handled by the application. For example, a 60 minute log out time for a public forum can be acceptable, but such a long time would be too much in a home banking application (where a maximum timeout of 15 minutes is recommended). In any case, any application that does not enforce a timeout-based log out should be considered not secure, unless such behavior is required by a specific functional requirement.

The idle timeout limits the chances that an attacker has to guess and use a valid session ID from another user, and under certain circumstances could protect public computers from session reuse. However, if the attacker is able to hijack a given session, the idle timeout does not limit the attacker’s actions, as he can generate activity on the session periodically to keep the session active for longer periods of time.

Session timeout management and expiration must be enforced server-side. If some data under the control of the client is used to enforce the session timeout, for example using cookie values or other client parameters to track time references (e.g. number of minutes since log in time), an attacker could manipulate these to extend the session duration. So the application has to track the inactivity time server-side and, after the timeout is expired, automatically invalidate the current user's session and delete every data stored on the client.

Both actions must be implemented carefully, in order to avoid introducing weaknesses that could be exploited by an attacker to gain unauthorized access if the user forgot to log out from the application. More specifically, as for the log out function, it is important to ensure that all session tokens (e.g. cookies) are properly destroyed or made unusable, and that proper controls are enforced server-side to prevent the reuse of session tokens. If such actions are not properly carried out, an attacker could replay these session tokens in order to “resurrect” the session of a legitimate user and impersonate him/her (this attack is usually known as 'cookie replay'). Of course, a mitigating factor is that the attacker needs to be able to access those tokens (which are stored on the victim's PC), but, in a variety of cases, this may not be impossible or particularly difficult.

The most common scenario for this kind of attack is a public computer that is used to access some private information (e.g., web mail, online bank account). If the user moves away from the computer without explicitly logging out and the session timeout is not implemented on the application, then an attacker could access to the same account by simply pressing the “back” button of the browser.

## How to Test

The same approach seen in the [Testing for logout functionality](06-Testing_for_Logout_Functionality.md) section can be applied when measuring the timeout log out.
The testing methodology is very similar. First, testers have to check whether a timeout exists, for instance, by logging in and waiting for the timeout log out to be triggered. As in the log out function, after the timeout has passed, all session tokens should be destroyed or be unusable.

Then, if the timeout is configured, testers need to understand whether the timeout is enforced by the client or by the server (or both). If the session cookie is non-persistent (or, more in general, the session cookie does not store any data about the time), testers can assume that the timeout is enforced by the server. If the session cookie contains some time related data (e.g., log in time, or last access time, or expiration date for a persistent cookie), then it's possible that the client is involved in the timeout enforcing. In this case, testers could try to modify the cookie (if it's not cryptographically protected) and see what happens to the session. For instance, testers can set the cookie expiration date far in the future and see whether the session can be prolonged.

As a general rule, everything should be checked server-side and it should not be possible, by re-setting the session cookies to previous values, to access the application again.

## References

Application Development Security 1.1/S1(a) Manage logon session and access controls securely

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/06-Session_Management_Testing/07-Testing_Session_Timeout.md