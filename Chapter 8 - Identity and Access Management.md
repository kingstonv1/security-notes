---
title: Chapter 8 - Identity and Access Management
tags:
  - "#project/comptia"
  - "#notes"
start: 04/16/2025
---
## Vocabulary
- **Identity:** The set of claims made about a subject, often an individual
- **Token:** A physical device used to authenticate via code generation, USB connection, Bluetooth, or some other method
- **Authentication:** The process of proving that an identity belongs to the subject claiming it
- **Authorization:** The process of verifying what belongs to an identity
- **Extended Authentication Protocol (EAP):** An authentication framework commonly used for wireless networks
- **Challenge Handshake Authentication Protocol (CHAP):** An authentication protocol designed to provide security using an encrypted challenge and three-way handshake
- **802.1x:** An IEEE standard for network access control (NAC) used for authenticating devices that want to connect to a network
- **Remote Authentication Dial-In User Service (RADIUS):** A protocol used to communicate with authentication servers
- **AAA:** Authentication, Authorization, and Accounting
- **Terminal Access Controller Access Control System TACACS(+):** A system which uses TCP to provide AAA services. Full-packet encrypted
- **Kerberos:** A protocol for authenticating service requests between trusted hosts across an untrusted network
- **Single Sign-On (SSO):** A service which allows a user to log in with a single identity and then use multiple systems or services without reauthentication
- **Lightweight Directory Access Protocol (LDAP):**  A directory service commonly used to store and access identities
- **Security Assertion Markup Language (SAML):** An XML-based open standard for exchanging authentication and authorization information
- **OpenID:** An open standard for decentralized authentication
- **OAuth:** An open standard for authentication used by many websites
- **Identity Provider (IdP):** A system that manages the life cycle of digital identities from creation to retirement
- **Security Key:** A physical device used to provide cryptography, security protocols, or 2 factor authentication
- **Multifactor Authentication:** An authentication system that uses multiple authentication factors
- **One-Time Password (OTP):** A password requested at authentication which is only usable once
- **Time-based One-Time Password (TOTP):** An OTP that rotates on a timer
- **HMAC-Based One-Time Password (HOTP):** An OTP that uses a seed that the device and server share as well as an iterating counter to generate codes
- **User Account:** An account that can be used for a variety of purposes, typically assigned to a person
- **Privileged / Administrative Account:** An account with heightened access to organization systems
- **Shared and Generic Accounts / Credential:** An account meant to be used by multiple people. Often prohibited
- **Guest Account:** An account provided to temporary users which typically has limited privileges
- **Service Account:** An account reserved for an automated service or application to sign on with
- **Identity Proofing:** The process of ensuring, during account provisioning, that the person requesting the account is the same person it's being made for
- **Permission Creep:** The gradual increase without removal of permissions assigned to an identity as they need them, leaving them with too much access
- **Privileged Access Management (PAM):** A set of tools used to handle accounts, especially with elevated permissions
- **Just-in-time (JIT) Permission:** A permissions granted or revoked only when use is needed, often with a checkout mechanism
- **Password Vaulting:** A PAM tool which allows users to "check out" privileged credentials
- **Ephemeral Account:** An account which is only available for some amount of time, after which it is deprovisioned
- **Access Control Scheme:** 
- **Mandatory Access Control (MAC):** A system which relies on the operating system to enforce control set by an administrator. Relatively rare
- **Discretionary Access Control (DAC):** A system which relies on the "owner" of a resource to delegate access
- **Role-based Access Control (RBAC):** A system in which accounts are assigned permissions based on pre-defined "roles"
- **Rule-based Access Control (RBAC / RuBAC):** A system that uses rules, typically Access Control Lists, to determine access to resources
- **Attribute-based Access Control (ABAC):** A system which uses attributes assigned to users to determine access

## Authentication and Authorization

There are a broad range of authentication and authorization protocols and technologies. Each system aims to either confirm that a person or device is who they say they are, or ensure that an already established identity doesn't do something they're not supposed to. 

EAP is a commonly used framework for end user devices to communicate to wireless networking devices like routers. There are a variety of implementations of EAP through different vendors including EAP-TLS, LEAP, and EAP-TTLS. These send EAP messages through their respective protocols. CHAP is another framework to fill this role of point-to-point authentication. CHAP works in the following order:
1. The client attempts to initiate a network connection
2. The CHAP server sends an encrypted challenge to the client, requesting a username and password
3. The client sends their encrypted username and password to the server
4. The server sends an acknowledgement accepting or rejecting their response

802.1X is a standard for setting up network security that describes the following relationship:

![[802.1x-Introduction-and-general-principles-flow.png]]

The client makes contact with an access point, typically with some variation of EAP or CHAP. The access point then pass along their credentials to an authentication server, usually via RADIUS. The authentication server interfaces with an account directory system through LDAP or Kerberos to find the user's information. The response is then passed along the chain backwards until it reaches the user.

RADIUS is typically used along the path from network devices to an authentication server. It utilizes md5 password hashes that are symmetrically encrypted, meaning its password security is lacking. For this reason, RADIUS traffic is typically double-encrypted using IPsec or other technology. RADIUS works over TCP and UDP.

TACACS+ drops in where RADIUS sits to provide a more security-oriented and granular approach for network devices to communicate with the authentication server. TACACS works over TCP.


**Kerberos** authenticates trusted hosts on an untrusted network. Kerberos is typically also the protocol used between authentication servers and their user directory controllers. Kerberos users are composed of a **primary**, or the username; an **instance**, a differentiator between primaries, and **realms**, which are groups of users. Typically, different realms have different **key distribution centers**. 

Kerberos authentication happens in this order:
1. The client sends an authentication request containing their credentials
2. The server sends back a TGS session key and a ticket-granting ticket, which is encrypted using the private key of the Ticket Granting Service
3. When the client wants to use a service, they send their TGT to the Ticket Granting Service and includes the name of the resource it wants to use
4. The TGS sends the client a valid session key 
5. The client uses the session key to access the resource

SSO systems exist to make the process of authenticating with a variety of services easier. A user signs on to a single trusted authentication service, which then grants them tokens to use in other services as long as they are authenticated. A variety of technologies are used to accomplish SSO systems, including:
- **SAML**, which is used for a variety of authentication-based applications. SAML provides a standardized format to exchange information between many identity providers, web apps, and service providers.
- **OpenID**, which allows third-party sites to piggyback off of identities established with trusted services like Google. In this system, Relying Parties (RPs) direct authentication requests to Identity Providers (IdPs), who authenticate the user then send back an affirmative response.
- **OAuth** allows services to share specific information with third-party services without having to share credentials.

Outside of web environments, SSO is typically implemented using LDAP and Kerberos.

## Authentication Methods

Passwords are the most common method of authentication, but they suffer from being stealable and having no mechanism tying an individual to their password. Password managers are recommended when handling passwords.

Passwordless authentication is becoming increasingly common, and each method provides its own pros and cons. 

A common passwordless setup uses a physical security key, such as a USB key, during the authentication process. The USB or Bluetooth devices holds private FIDO2 keys, while the public keys are sent to the service meant to be authenticated to. U2F is another passwordless security protocol.

Multifactor authentication is also an extremely common setup used to reduce the risks associated with passwords. MFA utilizes two or more *factors of authentication* - which include:
- *Something you know*, like a password or PIN
- *Something you are*, like biometrics or voice prints
- *Something you have*, like a physical security key or mobile phone
- *Somewhere you are*, your physical location

Attacks against MFA aren't unheard of, but they are generally more difficult then those against single-factor authentication systems.

A common MFA implementation is called a One-Time Password, or OTP. OTPs are temporary passwords or codes that are tied to a physical device, like an HOTP generator or TOTP generator app on a phone. Once used, an OTP is no longer valid - this means that if the attacker manages to secure an OTP, it's only valid once and for a very short amount of time. The least secure form of OTP is sent over SMS or phone call,. which can each be intercepted using SIM redirection or eavesdropping. When no device is present in the system, pre-supplied static codes can also be used as OTPs.

**Biometrics** are an authentication method that relies on the physical characteristics of the person attempting to authenticate. Biometrics include:
- Fingerprints
- Retina Scanning
- Iris Recognition
- Facial Recognition
- Voice Recognition
- Vein Recognition
- Gait Analysis

Biometric technologies are classified according to a few values. They are type 1 error rate, or False Rejection Rate (FRR), type 2 error rate, or False Acceptance Rate (FRR), the Receiver Operating Characteristic (ROC) (the false rejection rate against the false acceprance rate), and the Impostor Attack Presentation Match Rate (IAPMR).


## Access Control Systems

PAM, or Privileged Access Management, systems help maintain security and the principle of least privilege by allowing granular control over important or dangerous privileges in a system. PAM systems work in a couple ways - one is by providing just-in-time permissions, where permissions are granted to users for only the time that they are necessary, often on a "checkout" system. Just-in-time permissions prevent privilege creep and provide detailed logs as to who required what privileges when, but also provide overhead for the user. Password vaulting allows users to utilize accounts or services temporarily without actually knowing them. Finally, PAMs provide the capability to create ephemeral accounts - temporary accounts created for particular timeframe or purpose.

Access control systems fall into a couple distinct categories, each providing different granularity and overhead.
- **Mandatory Access Control** is an uncommon solution that relies on the host OS to enforce security policy on the resources it holds. This exists in Linux as SELinux and Windows as Mandatory Integrity Control.
- **Discretionary Access Control** allows the owners of a resource to delegate rights to other users and groups.
- **Role-based access control** defines the permissions that users have based on the roles (typically one primary role) that they hold. This system is useful when the users of a system are easily sorted into groups. RBAC uses three primary rules - *role assignment*, which states that subjects can only use permissions matching their role, *role authorization*, which states that the subject's active role must be authorized for the subject, and *permission authorization*, which states that subjects can only use permissions their active role is allowed to use. While users can have multiple roles, they can only have one active role at a time.
- **Rule-based access control** manages access using a set of rules, also called an ACL (access control list).
- **Attribute-based access control** manages access according to complex policies dictated by the combinations of attributes that is assigned to each user. These schemes are very flexible, but are harder to maintain