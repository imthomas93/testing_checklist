# Captcha Bypass

|ID          |
|------------|
|GTRT-ATHN-03|

## Summary

The CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart), was originally designed to prevent bots, malware, and artificial intelligence (AI) from interacting with a web page. In the 90s, this meant preventing spam bots. These days, organizations use CAPTCHA in an attempt to prevent more sinister automated attacks like credential stuffing.

Almost as soon as CAPTCHA was introduced, however, cybercriminals developed effective methods to bypass it. The good guys responded with “hardened” CAPTCHAs but the result remains the same: the test that attempts to stop automation is circumvented with automation.

There are multiple ways CAPTCHA can be defeated. A common method is to use a CAPTCHA solving service, which utilizes low-cost human labor in developing countries to solve CAPTCHA images. Cybercriminals subscribe to a service for CAPTCHA solutions, which streamline into their automation tools via APIs, populating the answers on the target website. These shady enterprises are so ubiquitous that many can be found with a quick Google search, including:


- DeathbyCAPTCHA
- 2Captcha
- Kolotibablo
- ProTypers
- Antigate

## How to Test

A CAPTCHA may hinder brute force attacks, but they can come with their own set of weaknesses, and should not replace a lockout mechanism.

To evaluate the unlock mechanism's resistance to unauthorized account unlocking, initiate the unlock mechanism and look for weaknesses. Typical unlock mechanisms may involve secret questions or an emailed unlock link. The unlock link should be a unique one-time link, to stop an attacker from guessing or replaying the link and performing brute force attacks in batches.

### Testing for Weak Pre-generated Questions

Try to obtain a list of security questions by creating a new account or by following the “I don’t remember my password”-process. Try to generate as many questions as possible to get a good idea of the type of security questions that are asked. If any of the security questions fall in the categories described above, they are vulnerable to being attacked (guessed, brute-forced, available on social media, etc.).

### Testing for Weak Self-Generated Questions

Try to create security questions by creating a new account or by configuring your existing account’s password recovery properties. If the system allows the user to generate their own security questions, it is vulnerable to having insecure questions created. If the system uses the self-generated security questions during the forgotten password functionality and if usernames can be enumerated (see [Testing for Account Enumeration and Guessable User Account](../03-Identity_Management_Testing/04-Testing_for_Account_Enumeration_and_Guessable_User_Account.md), then it should be easy for the tester to enumerate a number of self-generated questions. It should be expected to find several weak self-generated questions using this method.

### Testing for Brute-forcible Answers

Use the methods described in [Testing for Weak lock out mechanism](03-Testing_for_Weak_Lock_Out_Mechanism.md) to determine if a number of incorrectly supplied security answers trigger a lockout mechanism.

The first thing to take into consideration when trying to exploit security questions is the number of questions that need to be answered. The majority of applications only need the user to answer a single question, whereas some critical applications may require the user to answer two or even more questions.

The next step is to assess the strength of the security questions. Could the answers be obtained by a simple Google search or with social engineering attack? As a penetration tester, here is a step-by-step walkthrough of exploiting a security question scheme:

- Does the application allow the end user to choose the question that needs to be answered? If so, focus on questions which have:

  - A “public” answer; for example, something that could be find with a simple search-engine query.
  - A factual answer such as a “first school” or other facts which can be looked up.
  - Few possible answers, such as “what model was your first car”. These questions would present the attacker with a short list of possible answers, and based on statistics the attacker could rank answers from most to least likely.

- Determine how many guesses you have if possible.
  - Does the password reset allow unlimited attempts?
  - Is there a lockout period after X incorrect answers? Keep in mind that a lockout system can be a security problem in itself, as it can be exploited by an attacker to launch a Denial of Service against legitimate users.
  - Pick the appropriate question based on analysis from the above points, and do research to determine the most likely answers.

The key to successfully exploiting and bypassing a weak security question scheme is to find a question or set of questions which give the possibility of easily finding the answers. Always look for questions which can give you the greatest statistical chance of guessing the correct answer, if you are completely unsure of any of the answers. In the end, a security question scheme is only as strong as the weakest question.

## References

Application Development Security 2.2/S5(a) Agencies shall protect internet-facing systems against brute force log-on attempts by implementing the following security measures: (a) Incorporate bot mitigation tools such as CAPTCHA

https://blog.shapesecurity.com/2017/07/12/how-cybercriminals-bypass-captcha/

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/04-Authentication_Testing/03-Testing_for_Weak_Lock_Out_Mechanism.md

https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/04-Authentication_Testing/08-Testing_for_Weak_Security_Question_Answer.md