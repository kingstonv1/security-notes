---
title: Security+ Chapter 5 - Security Assessment and Testing
tags:
  - "#project/comptia"
  - "#notes"
---

## Vulnerability Management

The environments that cybersecurity experts manage are very complex, and so they will inevitably contain unpatched vulnerabilities at some point in their life. To keep up with this threat landscape, vulnerability management systems allow us to keep track of and patch these vulnerabilities. They work by providing an environment to categorize and identify vulnerabilities, and by discovering them in the network through vulnerability scanning. Every organization should have a vulnerability management system in place.

There are important questions to consider when implementing a vulnerability management system, the most pressing being “what should we scan?”

What you scan depends on the answer to a handful of questions, such as:
- What is the data classification of the information stored on a system?

	If the data is highly classified, vulnerabilities in the management software could lead to a critical data leak.
	
- Is the system exposed to the Internet or semi public networks?
	If it is, you will likely want to scan the system because the number of potential attackers is higher for these exposed systems.
	
- What services are offered by the system?
	Critical systems to the organization should be scanned, since the damage caused by exploiting these is disproportionate.
	
- Is the system a production, test, or development system?
	Development and testing systems may need a lesser degree of scanning and surveillance because they have a much smaller base of cleared users.

Some organizations also use automated tools to determine the devices on their network that they will scan. A listing of systems produced by these tools or by hand is called an asset inventory. A value attached to an asset describing the importance of its functionality to the organization is called an asset criticality value.

#### Configuring Scans

Vulnerability scanning applications include automation functionality that allows the user to schedule scans over their systems to run automatically. There are multiple factors that influence how often an organization may schedule these scans for:

- What is their risk appetite?
	An organization's risk appetite is its willingness to tolerate risk in their systems. An organization with little risk tolerance is likely to run scans more often, to limit the amount of time that systems are vulnerable if an exploit exists.
    
- What are the regulatory requirements they must follow?
	Regulatory requirements, such as the PCI DSS or the FISMA (Federal Information Security Management Act) may set a floor on the frequency of vulnerability scans.
    
- What are the technical constraints the organization operates under?
	Systems may lose functionality while being scanned, the increased traffic might slow critical response times, or a scanning system may only be able to run so many scans per day, leading an organization to consider scanning less frequently.
    
- What are the business constraints limiting the organization?
	Some periods of time might be more business traffic intensive, leading the organization to limit the amount of scans at the time.
	
- What are the licensing limitations faced by the organization?
	Software licenses may limit the amount of bandwidth consumed by the scanner or the number of scans able to be conducted simultaneously.
	
  
In addition to modifying the frequency of security scans, most scanning suites provide the ability to tweak the fine details of the scans themselves. You can modify the reports and how they’re sent, change which checks are conducted, provide credentials to access services, and conduct scans from a variety of places. It’s important to run configuration reviews on these settings to ensure they’re up to date with the organization requirements. Pay close attention to scan sensitivity levels, which will determine how invasive the tests run on the target machines get.

You can create new scanning configurations by beginning with a template (found online or provided through the software suite that includes the scanner.) Then, fine-tune settings to fit your organizational needs. Finally, save your configuration as a setting template so future scanning configurations can be made from it.
#### Vulnerability Scan Types

Although simple network scans can be very helpful for getting a bird's-eye view of your systems and architecture, modern vulnerability scanners have a variety of options to help you go deeper.

**Credentialed Scans**
Scans can be supplied with credentials that let them authenticate with your services and test for vulnerabilities from a user standpoint. This can help prevent false positives by allowing the scanner to confirm that a vulnerability actually exists before reporting it in the results. Notably, these scanners don't usually make modifications to data on the server, so the accounts provided should only be given read privileges. 

**Agent Scans**
Another type of in-depth scan is an agent-based scanning approach, where there is a scan tool installed on the scan server and the target server. This provides an "inside-out" approach for scanning, which can be more comprehensive and accurate than a traditional one sided scan. However, you should be wary of deploying these types of scans on live servers, as they can cause performance issues.

**Perspective Scans**
Some vulnerability management programs have the ability to conduct scans from a variety of different network perspectives, such as on the local machine, from the external internet, from DMZ servers, etc. These scans can help identify vulnerabilities that exist after attackers bypass layers of your organization's defense.

**Maintenance**
Just like any other security control, an organization's security team should conduct regular maintenance of scanning tools to ensure that the tools themselves and the vulnerability feeds remain up to date. Often times, these tools do provide automatic updating capabilities, but they should still be manually checked on regularly.

Be wary of vulnerabilities on your scanning software itself, as no software is immune from security vulnerabilities. You should keep this software patched and as unprivileged as it can be, like you would for any other application or control.

Updating your plugins and vulnerability feeds regularly is critical, as scanners can only know what to look for with accurate, new vulnerability marker information. These tools should be configured to retrieve new vulnerability information on their own regularly, ideally on a daily basis.

#### Vulnerability Scanning Applications

When filling out your toolkit, you will want to have a network vulnerability scanner, an application scanner, and a web application scanner available to you. These applications are found in offensive and defensive security specialists' toolsets.

**Infrastructure Vulnerability Scanning**
Network vulnerability scanners work by probing individual devices connected to the network for information about what they are and what software they run. Then, they run targeted tests on each device to detect unpatched vulnerabilities. Some examples of network vulnerability scanners include:
- Tenable's Nessus, a tried-and-true scanner that's been around for a while
- Qualys's scanner, a newer, cloud SAAS based scanner that can cover your on-premises and cloud applications.
- Rapid7's Nexpose
- OpenVAS, a FOSS vulnerability scanner

It's important to use a vulnerability scanner in your security routine, and some organizations even deploy two as a DID measure.

##### Application Scanning
Application scanners work on custom developed software made by your company. They scan your application to identify common vulnerabilities created by developers. Application testing uses three techniques:
- *Static Testing* analyzes code without executing it.
- *Dynamic Testing* executes the code as part of the test, testing all user-exposed features.
- *Interactive Testing* combines both of the following, analyzing the source code while the scanner interacts with the application.

Application testing should be embedded in the development process. Many organizations require a clean, passing set of tests before new code is allowed to be released into production.

##### Web Application Scanning
Web application scanners look for vulnerabilities in web applications. They test for common attack vectors like SQLI, XSS, CSRF, etc. They use traditional network sans and detailed probing to break the application.
- Nikto is a popular web scanner tool. It's open source and feely available. It has a CLI and is somewhat difficult to use.
- Arachni is also a FOSS web application scanner.

Most organizations use commercial products that have more advanced capabilities and user-friendly interfaces. There are dedicated web scanners on the market (Acunetix), but most organizations use web scanners bundled with their existing scanner suites, such as Nessus and Qualys.

##### Scan Reports
Scan reports provide an overview of all the information discovered during the scan. They give detailed information about each identified vulnerability, if applicable.

Here is an example Nessus vulnerability report:
![[Pasted image 20250113091440.png]]

At the very top, there are two details: the name of the vulnerability, and the overall severity in the top left. Typically, this is low, medium, high, or critical.

Next, there is a detailed description of the vulnerability.

The next section describes how to remedy the vulnerability. In this case, it's an application-by-application process.

In the 'See Also' section, the scanner provides references where further details on the vulnerability can be found.

The 'output' section ahows detailed information returned by the system when probed for the vulnerability. This information can be valuable because it provides the exact output to the probing.

The 'hosts' section contains the servers, services, or ports on the server that host the vulnerability. 

The 'vulnerability' information contains misc. information about the vulnerability.

The 'risk information' section gives useful information that helps asses the severity of the vulnerability.

The last section provides details on the plugin that detected the issue. 

#### Understanding CVSS

##### Tables
---
The *Common Vulnerability Scoring System* is an industry standard for assessing the severity of security vulnerabilities. It scores a vulnerability on multpile different aspects, illuminating how to prioritize prevention and incident response.

Analysts scoring a vulnerability begin by rating it on eight different measures. The first four evaluate the exploitability, and the last 3 evaluate the impact.

**Attack Vector Metric**
The attack vector metric describes how the vulnerability would be exploited.

| Value                | Description                                                                                  | Score |
| -------------------- | -------------------------------------------------------------------------------------------- | ----- |
| Physical (P)         | The attacker must physically touch the vulnerable device.                                    | 0.20  |
| Local (L)            | The attacker must have physical or logical access to the affected system.                    | 0.55  |
| Adjacent Network (A) | The attacker must have access to the local network that the affected system is connected to. | 0.62  |
| Network (N)          | The attacker can exploit the vulnerability over a network remotely.                          | 0.85  |

**Attack Complexity Metric**
The attack complexity metric describes the difficulty of exploiting the vulnerability.

| Value    | Description                                                                                   | Score |
| -------- | --------------------------------------------------------------------------------------------- | ----- |
| High (H) | Exploiting the vulnerability requires specialized conditions that would be difficult to find. | 0.44  |
| Low (L)  | Exploiting the vulnerability does not require any specialized conditions.                     | 0.77  |

**Privileges Required Metric**
The privileges required metric describes the type of account access that an attacker would need to exploit a vulnerability.

| Value    | Description                                                         | Score                              |
| -------- | ------------------------------------------------------------------- | ---------------------------------- |
| High (H) | Attackers require administrator privileges to conduct the attack.   | 0.27 (or 0.50 if scope is changed) |
| Low (L)  | Attackers require basic user privileges to conduct the attack.      | 0.62 (or 0.68 if scope is changed) |
| None (N) | Attackers do not need to authenticate to exploit the vulnerability. | 0.85                               |

**User Interaction Metric**
The user interaction metric describes whether the attacker needs to involve another human in the attack.

| Value        | Description                                                                          | Score |
| ------------ | ------------------------------------------------------------------------------------ | ----- |
| None (N)     | Successful exploitation does not require action by any user other than the attacker. | 0.85  |
| Required (R) | Successful exploitation requires action by a user other than the attacker.           | 0.62  |

**Confidentiality Metric**
The confidentiality metric describes the type of information disclosure that might occur if an attacker exploits the vulnerability.

| Value    | Description                                                                                                          | Score |
| -------- | -------------------------------------------------------------------------------------------------------------------- | ----- |
| None (N) | There is no confidentiality impact.                                                                                  | 0.00  |
| Low (L)  | Access to some information is possible, but the attacker does not have control over what information is compromised. | 0.22  |
| High (H) | All information on the system is compromised.                                                                        | 0.56  |
**Integrity Metric**
The integrity metric describes the type of information alteration that might occur if an attacker exploits the vulnerability.

| Value    | Description                                                                                                             | Score |
| -------- | ----------------------------------------------------------------------------------------------------------------------- | ----- |
| None (N) | There is no integrity impact.                                                                                           | 0.00  |
| Low (L)  | Modification of some information is possible, but the attacker does not have control over what information is modified. | 0.22  |
| High (H) | The integrity of the system is totally compromised, and the attacker can change any information at will.                | 0.56  |

**Availability Metric**
The integrity metric describes the type of disruption that might occur if an attacker successfully exploits the vulnerability.

| Value    | Description                                | Score |
| -------- | ------------------------------------------ | ----- |
| None (N) | There is no availability impact.           | 0.00  |
| Low (L)  | The performance of the system is degraded. | 0.22  |
| High (H) | The system is completely shut down.        | 0.56  |
**Scope Metric**
The scope metric describes whether the vulnerability can affect system components beyond the scope of the vulnerability. The scope metric does not contain score information. The scope metric is reflected in the values for the privileges required metric as shown earlier.

| Value       | Description                                                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Unchanged   | The exploited vulnerability can only affect resources managed by the same security authority.                                                    |
| Changed (C) | The exploited vulnerability can affect resources beyond the scope of the security authority managing the component containing the vulnerability. |

##### Understanding CVSS

The **CVSS vector** uses a single-line format to convey the ratings of a vulnerability on all six of the metrics described in the preceding sections. For example, see this CVSS vector:

 ```CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N```

The vector contains nine components. The first section just informs the reader that the vector was composed using CVSS v3. The next eight sections correspond to each of the 8 CVSS metrics. In this case, the vulnerability received the following ratings:

- Attack Vector: Network (score: 0.85)
- Attack Complexity: Low (score: 0.77)
- Privileges Required: None (score: 0.85)
- User Interaction: None (score: 0.85)
- Scope: Unchanged
- Confidentiality: High (score: 0.56)
- Integrity: None (score: 0.00)
- Availability: None (score: 0.00)

The VCSS vector provides good detailed information on the nature of the risk posed by a vulnerability, but the complexity of the vector makes it difficult to use in prioritization exercises. For this reason, analysts can calculate the *CVSS base score*, a single number representing the scores.

The first step in calculating the base score is calculating the *impact sub-score (ISS)*. The metric summarizes the three impact metrics using this formula:
$$ISS=1-[(1-Confidentiality) * (1 - Integrity) * (1 - Availability)]$$

To calculate the overall impact score we must take the value of scope into account. If the scope metric is Unchanged, we multiply the ISS by 6.42.

If the scope metric is changed, we use a more complex formula:
$$Impact = 7.52 * (ISS - 0.029) - 3.25 * (ISS - 0.02)^{15}$$

Finally, you can calculate the exploitability score using this formula:
$$Exploitability = 8.22 * AttackVector * AttackComplexity * PrivilegesRequired * UserInteraction$$

**Calculating the Base Score**
With all this information at hand, we can now determine the CVSS base score using the following rules:
- If the impact is 0, the base score is 0.
- If the scope metric is Unchanged, calculate the base score by adding together the impact and exploitability scores.
- If the scope metric is Changed, calculate the base score by adding together the impact and exploitability scores and multiply the result by 1.08.
- The highest possible base score is 10. If the calculated value is greater than 10, set the base score to 10.

**Categorizing CVSS Base Scores**
Many scanning systems further summarize CVSS results by using risk categories rather than numeric risk ratings.

|CVSS score|Rating|
|---|---|
|0.0|None|
|0.1-3.9|Low|
|4.0-6.9|Medium|
|7.0-8.9|High|
|9.0-10.0|Critical|

##### Validating Scan Results
Analysts interpreting reports often perform their own investigation to confirm the presence and severity of vulnerabilities. These investigations may include the use of external sources that supply additional information.

**False Positives**
Cybersecurity analysts should confirm each vulnerability reported. In some cases, it could be as simple as checking a patch is missing or an OS is outdated.  In other cases, you may have to simulate the exploit. When verifying a vulnerability, analysts should draw on their own expertise as well as the expertise of others. DB administrators, system engineers, network technicians, software developers, and other experts have domain knowledge that is very helpful.

**Reconciling Scan Results with Other Data Sources**
Scans should never take place in a vacuum. Analysts interpreting the reports should turn to other sources of information to supplement the analysis, such as:
- Log reviews from servers, devices, and other sources that might contain information about attempts to exploit a vulnerability
- Security information and event management (SIEM) systems that correlate log entries from multiple sources
- Configuration management systems that provide information on the OS and applications installed on a system

Each of these sources can provide good intelligence when reviewing scan reports.

#### Security Vulnerabilities

Each vulnerability scanning system contains plugins to detect different domains of vulnerabilities. It's important for analysts to be familiar with the most commonly detected vulnerabilities and some of the general categories that many vulnerabilities.

*I'm only gonna take notes on the stuff I don't know / new information in this section*

**Patch Management**
Applying security patches to systems regularly is one of the most important security considerations, but it's one that is often neglected due to a lack of resources dedicated to preventative maintenance. "Outdated application / OS" is a very commonly detected vulnerability on scans.

Therefore, it's important to have a *patch management* program that routinely patches security issues.

**Weak Configurations**
Vulnerability scans may also highlight weak configurations on systems, such as:
- The use of default settings, such as credentials
- The presence of unsecured accounts
- Open ports and services that aren't necessary for operation
- Open permissions that violate the principle of least privilege

It's important that these options are addressed when setting up technology and when detected through a scanner.

**Error Messages**
Many applications and development platforms support *debug modes* that give developers critical information for troubleshooting applications. Debug mode provides information on the workings of the application, which can assist an attacker looking to exploit the system.

Development should occur on an isolated private network only accessible internally. To solve the issue when detected, talk to your developers and ask them to disable debug modes on public-facing systems

**Insecure Protocols**
Many old internet protocols weren't made with security in mind at all. Protocols like FTP and HTTP don't use encryption or any kind of data obfuscation. The solution when this is detected in scans is to just switch to a more secure protocol. Encrypted alternatives exist for nearly every insecure protocol.

**Weak Encryption**
Encryption is an important security control used in lots of different programs. Not all encryption algorithms are built equally, and your scanner may alert you if a program uses an exploitable or outdated encryption mechanism. The solution is to simply switch to a better or newer algorithm in your application.

##### Penetration Testing
Penetration testing is the most comprehensive and accurate way to test your organization's security, but the practice requires security specialists as knowledgeable as the attackers  you wish to defend against.

There's a significant difference between the mindsets of an attacker and a defender. While a defender seeks to protect each part of their systems from the top-down, an attacker only seeks to exploit one vulnerability. While defenders need to defend from lots of attacks, successfully deterring all of them, attackers only need to succeed once.

The main way to classify penetration tests is based on the amount of knowledge that the tester has been given by the organization to begin with.
- In a *white-box* test, the testers are given full knowledge of all the systems and security controls in their scope. This includes network diagrams, security configurations, and possibly even credentials. These tests tend to provide the most comprehensive results, though not necessarily the most accurate to an actual attacker
- In a *black-box* test, the testers are not given any information about the systems they will attack. They must go through the same processes of discovery as any attacker, slowing down the test but providing an accurate assessment of what trying to compromise the systems from 0 is like. When conducting a black-box test, the skill and quality of the penetration tester is very important.
- In a *gray-box* test, testers have some knowledge about the environment but not full knowledge. A gray-box test can help focus efforts while also providing an accurate picture of security.

A key part of any penetration test is the agreement on **rules of engagement**. Key rules include the following:
- The timeline, during which testers are allowed to attack the network.
- The locations, applications, or targets that are allowed to be targeted.
- The ways in which testers are allowed to handle data or information gathered during the course of the test.
- The defenses that will be employed against the tester during the course of their test.
- What resources (time, money, licenses) will be committed to the test.
- Legal concerns for the tester and the defender.
- When and how communications will occur.


> [!CAUTION] Permission
> Don't penetration test companies without their knowledge or consent. You stupid idiot.


Agreeing on the scope and terms of the test is incredibly important. The chosen methodology impacts the results of the test - for example, a white-box test is much more likely to detect deeply nested issues than a black-box test. Clear communications around how problems and issues are handled during the test are also important. It can't always be guaranteed that a penetration test won't result in server outages or other issues. For this reason, both sides of the test should be clear about how they will communicate, when the testers should stop, and what measures they have taken during the test.

**Reconnaissance**
Penetration tests begins with a reconnaissance phase. During this time, the testers conduct scans, pointed tests, google searches, and use other information gathering techniques to get a good picture of the systems they're attacking. These techniques are split into passive techniques, like utilizing OSINT, and active techniques, which involve directly engaging with the systems.

One such method is *war driving*, a technique in which testers drive by physical facilities in a car equipped with high-end wireless signal detection equipment to scan for any vulnerable wireless networks. This technique has been expanded to include UAVs in a technique known as *war flying*.

**Running the Test**
During the test, the testers follow the same basic process used by attackers. Here are some key points:
- Initial access occurs when an attacker exploits a vulnerability to gain a foothold in the organization's network.
- Privilege escalation uses techniques to gain additional authorization on the network.
- Pivoting, also known as lateral movement, when the attacker moves between systems to gain new perspectives.
- Persistence is established when the attackers can return to the network without exploiting the initial vulnerability.

Penetration testers make use of the same tools as real attackers. One such example are *exploitation frameworks* like metaploit that provide an easy, module approach to exploiting vulnerabilities.

**Cleaning Up**
At the end of a penetration test, the testers finish their reports, present the results to management, and clean up the traces of their work. Testers should remove persistence and exploit tools they left behind.

**Training and Exercises**
Running training exercises helps everyone involved on the security team get hands-on experience dealing with incidents and attacks in a real environment. During most cybersecurity excercises, the participants are split into three teams: red team, who conducts an attack, blue team, who must secure the systems from the attack (often with a head start), and white team, who moderates the other two teams, settling disputes and setting rules.

One example of an exercise to perform is the Capture the Flag exercise, where the blue team attempts to defend a specific system or bit of data (the flag) from the red team. The exercise is scored based on how many objectives the red team achieved.