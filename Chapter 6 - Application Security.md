---
title: Security+ Chapter 6 - Application Security
tags:
  - "#project/comptia"
  - "#notes"
---
## Vocabulary
- **Software Development Life Cycle (SDLC)**: The steps that software being developed goes through before its end of life.
- **User Acceptance Testing (UAT):** Testing on software or tools that gives the system to the end user and asks whether they are satisfied with it.
- **DevOps:** The combination of software development and IT operations with the goal of speeding up/improving the SLDC.
- **DevSecOps:** DevOps model with security considerations.
- **Continuous Integration/Deployment:** Automated toolchains which with with frequently updated codebases to test and push changes as they are implemented.
- **Static Code Analysis:** Inspection, automated or manual, done on code before it is compiled.
- **Dynamic Code Analysis:** Inspection, automated or manual, done on running code. This allows the inspector to pass input into the program and note its response.
- **Fuzzing:** Inspection of code, typically automated, done by sending large amounts of typically invalid or malformed information as input.
- **SQL Injection (SQLi):** An attack carried out on applications that do not sanitize the data they pass into SQL queries, where a user may supply SQL code in order to have the server make a request or reveal information it is not intended to.
- **Blind SQLi:** An SQLi attack in which the attacker cannot directly see the results of their attack. This can be *content-based* - where the user may know whether their query was successful or not based on the results displayed (but they do not get complete results), or *timing-based* - where the user requests a timeout and measures the time between what would have been a successful and unsuccessful request.
- **Code Injection:** A general term for injection attacks which is not limited to SQL. Code Injection includes LDAP injection, XML injection, DLL injection, and Cross Site Scripting.
- **Command Injection:** A form of injection attack that injects a command or API call for the host operating system to execute. 
- **Session Hijacking:** An attack in which an attacker steals a token or cookie that a legitimate user was given after authentication.
- **On-Path Attack:** In attack in which an attacker tricks a user into thinking they are the website the user is attempting to authenticate through. They then use the user's information to authenticate on behalf of the user.
- **Session Replay Attack:** An attack in which the attacker modifies or uses a user's authentication cookie to gain access to a web application.
- **Insecure Direct Object Reference:** A situation in which user-provided data is blindly used to access server information (such as by an index or ID).
- **Directory Traversal:** An attack in which an attacker injects a malicious path into a server in order to read or modify files that were not intended.
- **Local File Inclusion (LFI):** An attack which uses directory traversal techniques to execute code stored on the server.
- **Remote File Inclusion (RFI):** An attack which uses directory traversal techniques to execute code stored on a remote server.
- **Reflected Cross Site Scripting (XSS):** When unsanitized user input is reflected in the web page, allowing for arbitrary HTML code to be run as part of the application.
- **Stored/Persistent XSS:** When unsanitized user input is reflected in the web page and stored permanently as content, allowing other users to access the page with arbitrary HTML.
- **Cross Site Request Forgery (CSRF):** An attack that assumes a user is authenticated with a website and makes a request to the website on their behalf (through a link, code injection, etc)
- **Server Side Request Forgery (SSRF):** An attack that tricks a server into visiting a URL. This is dangerous when the server has access to URLs that the user is not intended to.
- **Parameter Pollution:** An attack which includes multiple parameters in a URL or form in hopes that validation only occurs on one.
- **Web Application Firewall (WAF):** A firewall that sits between the user and web application and intercepts bad requests or sensitive data before the request is completed.
- **Parameterized Queries:** Pre-written commands or queries that do not accept data as code.
- **Sandboxing:** Running an application in an isolated or controlled environment to prevent data leakage or make compromises less impactful.
- **Code Signing:** A way to check the authenticity of code being run on a user machine or server by cryptographically signing legitimate versions of the code.
- **Dead Code:** Code that an organization uses that is not being maintained or monitored.
- **Backdoor:** A vulnerability in which a set of credentials or a key can (intentionally or unintentionally) be used to bypass an application or system's security measures.
- **Resource Exhaustion:** A scenario in which an operating system runs out of resources (typically memory or storage space) to allocate to the program.
- **Memory Leak:** A type of resource exhaustion in which a poorly written program does not properly use or destroy memory that it needed previously, leaving that memory unusable to other processes.
- **Buffer Overflow:** When more data is placed into an area of memory than was allocated for that data.
- **Memory Injection:** When an attacker places arbitrary values into a section of memory, typically paired with a buffer overflow.
- **Race Condition:** A scenario in which the behavior of a code segment relies on the sequence of events happening on the host system.
- **Time-Of-Check (TOC):** The moment a system verifies a condition.
- **Time-Of-Use (TOU):** The moment a resource is modified or read after the condition.
- **Target Of Evaluation:** The resource being evaluated or tested by the check, and used for the use case.
- **TOCTOU Race Condition:** A race condition that occurs when the time-of-check is too far ahead of the time-of-use, and the result of the condition changes in that time.


## The Software Development Life Cycle

The *software development life cycle* is a model describes a process that an organization seeking to develop software should follow. There are different SDLC models to follow. Generally, they follow a form such as:
- **Planning.** Should we write the application? What else could we do to solve the problems the application looks to solve? Should we move forward?
- **Requirements.** Based on the customer, what should the application do? What should the application not do? What should we do to improve on current solutions?
- **Design.** What APIs and dataflows will be used? What technologies will be used during the programming, testing, and deployment processes? How does the application remain secure?
- **Coding.** What unit tests will be written? How will the program systems work? How will input be validated and used?
- **Testing.** What is the code supposed to do? Does the finished product fulfill those requirements? How easy is it for an attacker to compromise the program? Are the users happy with the system?
- **Training and Transition. (also called Acceptance, Installation, and Deployment).** Do the users understand how to use the application? Were previous applications phased out?
- **Operations and Maintenance.*** Does the software need modifications? Do the users need assistance with it?
- **Decommissioning.** Is the (now old) solution using resources or causing vulnerabilities it doesn't need to? Do users still need the application? Does the data need to be disposed of?

The order of the phases is not rigid, and often multiple are done in parallel.

##### DevSecOps

DevSecOps is often accomplished using collections of applications and systems known as toolchains. These toolchains help code, build, secure, test, release, and configure software. In a DevSecOps model, dedicated personnel are responsible for continually analyzing the threats in and around the application being developed and considering security implications in development decisions. 

Frequently, Dev(Sec)Ops pipelines include continuous integration toolchains to build, test, and deploy new changes to the codebase in an automated way. Continuous validation and continuous monitoring are required to sustain a continuous integration model in case of issues or attacks.


## Designing and Coding for Security

There are a number of ways to keep application development secure throughout all steps of the SDLC.

##### Secure Coding Practices

OWASP (the Open Worldwide Application Security Project) provides up-to-date, helpful documentation about good secure coding practices. Their top proactive coding controls are as follows:
- **Define Security Requirements.**
- **Leverage Security Frameworks and Libraries.**
- **Secure Database Access.**
- **Encode and Escape Data.**
- **Validate All Inputs.**
- **Implement Digital Identity.**
- **Enforce Access Controls.**
- **Protect Data Everywhere.**
- **Implement Security Logging and Monitoring.**
- **Handle All Errors and Exceptions.**

## Exploiting Authentication Vulnerabilities

Often, servers an applications rely on an authentication process to ensure that users are able to complete a requested action. There are a variety of ways to bypass these authentication systems and gain illegitimate access to systems and services. At a high level, these approaches include:
- session attacks, which seek to bypass authentication by piggybacking off of someone who has already authenticated - like cookie stealing and session replay attacks
- brute force attacks, which attempt to authenticate with a variety of different credentials until one set works - like hash cracking attacks and password spraying

Common vectors to conduct authentication-related attacks include lack of modification of default credentials, insecure cookie or session data handling, and insecure redirection handling.

## Code Security

Software developers can do a lot to prevent attacks on their software.

Code signing allows the end user to ensure that the code being run on their system was legitimately deployed by the correct organization, and has not been modified. Code signing uses public key cryptography and prevents malicious updates. Many systems will only accept digitally signed updates.

It's also important to be aware of when third-party code is used and reused. Libraries, SDKs, and in-house libraries can contain vulnerabilities - and any vulnerability that a library contains is likely also exploitable in your application. It's important to track the security status of all of your dependencies and keep them up to date.

Single points of failure are another point to notice when architecting code security - do multiple or all systems rely on shared binaries, libraries, programs or files? It's not always possible to prevent these singular points of failure, but doing so can create much more robust functionality and prevent availability issues.

It's best practice to store organization code in a repository and use version control to manage it. A shared code repository allows for a central source of truth when seeking information about the code, greater reusability for developers, integration with automated pipelines and toolchains, and prevent the dead code problem. Code repositories and automation also allow for code integrity checking, a process in which code files in the release are hashed and then the deployment systems check the hashes of the code being deployed to ensure they are the same.

Also, applications should be scalable - they can use additional computing resources to increase the throughput or speed of their operations - and elastic - they can spin up or turn down computing resources in order to scale to meet demand - in order to best optimize resource use and minimize waste.

Comments in code are another point to consider. Source code comments are helpful documentation for developers, but also helpful documentation for attackers looking to get insight into the inner workings of the program. When code needs to be deployed or given to user systems, the comments should be removed.

Errors should also be thoroughly handled throughout your program code. It's up to the developers to try to anticipate edge case scenarios and write error handling paths for them. However, try not to write error handling routines that are unnecessarily detailed, because that might give away details of the inner workings of the program.

Don't hard code credentials into your code. No backdoors, no API keys without .env files.