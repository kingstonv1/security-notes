---
title: Chapter 12 - Network Security
tags:
  - "#project/comptia"
  - "#notes"
start: 04/20/2025
---
## Vocabulary

- **Defense-in-Depth:** The concept that several layers of security controls should be used, so a failure in one does not necessarily allow for a breach
- **Fail-Closed:** A network security control that does not allow any traffic through in a failure state
- **Fail-Open:** A network security control that allows all traffic through in a failure state
- **Active Network Tap:** A powered network device that monitors or copies network traffic
- **Passive Network Tap:** An unpowered network tap
- **Physical Isolation / Air-Gapping:** The practice of separating network devices from other network devices to prevent connectivity
- **Logical Segmentation:** The practice of using software or settings to prevent network devices from communicating
- **Software-Defined Networking (SDN):** A setup which uses software-based network configuration tools to manage a network
- **Software-Defined Wide Area Network (SD-WAN):** A virtual WAN design that allows multiple connectivity services to interconnect (MPLS, 4G, 5G, broadband)
- **Secure Access Service Edge (SASE):** Combines VPNs, SD-WAN, and cloud tools to provide secure access for devices
- **Broadcast Domain:** A network segment in which a computer can reach another computer by sending out a broadcast to all computers on the domain
- **Screened Subnet / Demilitarized Zone (DMZ):** Network zones that contain systems that need to be exposed to less trusted areas
- **Intranet:** An internal network set up to provide information to employees or members of an organization, typically without external access
- **Extranet:** A network set up to be accessed by specific external partners
- **East-West Traffic:** Traffic between computers in the same network segment, often difficult to monitor / control
- **Zero Trust:** A defense principle that assumes no network user is trusted and every action taken in a network should be validated
- **Subject:** The system requesting access to a resource in a zero-trust model
- **Policy Engine:** A server in a zero-trust setup which makes policy decisions based on rules or external systems. The policy engine will grant, deny, or revoke access to a resource based on its algorithm
- **Policy Administrator:** A server in a zero-trust setup which will grant tokens or decide to sever connections based on the decisions made by the policy engine
- **Policy Enforcement Point:** A server (or client-gateway setup) in a zero-trust setup which actually severs connections at the order of the policy administrator
- **Zero-Trust Control Plane:** The "plane" in a zero-trust setup which contains adaptive identity, threat scope reduction, policy-driven access control, and policy administrator services
- **Adaptive Identity / Adaptive Authentication:** A zero-trust technology that considers a variety of factors such as authentication factors, geolocation, and device used to determine whether a user should be granted access to an identity
- **Threat Scope Reduction / Limited Blast Radius:** A principle that limits what any individual identity can do through PLP and identity-based network segmentation to prevent the potential impact of a breach
- **Policy-Driven Access Control:** An access control system relying on policy lists to make decisions about access and a policy administrator / PEP to enforce those decisions
- **Zero-Trust Data Plane:** The "plane" in a zero-trust setup which contains implicit trust zones, subject and system architecture, and policy enforcement points
- **Implicit Trust Zone:** A network segment which allows movement and use once a subject is authenticated with a policy engine
- **Subject / System Architecture:** A setup which defines endpoint devices that are seeking access
- **Network Access Control (NAC):** A system which allows or disallows an endpoint to connect to the network based on attributes of the endpoint
- **Port Security:** A technology that allows you to limit the number of MAC addresses that can be used on a single port
- **Spanning Tree Protocol (STP):** A routing protocol that aims to prevent network loops
- **Broadcast Storm:** An issue caused when network activity is echoed back and forth and amplified each time
- **Bridge Protocol Data Unit Guard:** A technology that protects STP by ensuring that ports that shouldn't be able to send BPDU messages can't do so
- **Dynamic Host Configuration Protocol (DHCP) Snooping:** A technology that prevents rogue DHCP servers from handing out IPs
- **IPSec VPNs:** Layer 3 VPNs that transport encrypted traffic using an IPSec client-server connection
- **SSL VPNs:** VPNs that use TLS to transport encrypted traffic
- **Jump Server:** A secured and monitored system used to provide access between zones with different security levels
- **Load Balancer:** A piece of equipment or software that provides a service a virtual IP. Traffic coming into the virtual IP is distributed between systems
- **Proxy Server:** A server that accepts and forwards requests in order to centralize traffic
- **Forward Proxy:** A proxy server placed between clients and servers which forwards requests
- **Reverse Proxy:** A proxy server planed between clients and swervers which helps with load balancing and caching
- **Web / Content Filters:** Centralized proxy devices or agent-based tools that block traffic based on content rules
- **Stateless Firewalls:** Simple firewalls that make decisions based on only the information contained in individual packets
- **Stateful Firewalls:** More advanced firewalls that consider the entire state of a network exchange, including past packets between two computers
- **Next-Generation Firewall (NGFW):** A firewall which inspects typically layer 4 traffic, but also layer 7 (application) traffic to make decisions about blocking requests. Often NGFWs come bundled with other security controls as part of the solution, similar to a UTM system
- **Unified Threat Management:** A device that includes firewalls, IDP/IPS, antivirus, URL and Email filtering, DLP systems, VPNs, and monitoring capabilities. Often, UTM solutions require less configuration than NGFWs
- **Web Application Firewall (WAF):** A firewall specifically geared towards protecting web applications from attacks - like a standard firewall combined with an IPS
- **Access Control List (ACL):** A rule that permits or denies actions in a network, typically used with a firewall
- **Honeypots:** Systems intentionally configured to appear vulnerable, but are instead safe, heavily monitored systems to collect information about attackers
- **Honeyfile:** A file set up to be alluring in a place where an attacker might look after a breach. The file is closely monitored and alarms are raised if it is touched
- **Honeytoken:** Data that is intended to be attractive to attackers but is instead used to track the attacker
- **Out-of-Band Management:** The ability to access and manage a network device even when not directly on its network
- **DNS Filtering:** A technology which implements lists of domains to reroute or block DNS requests for
- **DomainKeys Identified Mail (DKIM):** An asymmetric cryptography setup in which public keys are registered to an email server through DNS and outgoing messages are signed
- **Sender Policy Framework (SPF):** Infrastructure which allows organizations to publish a list of authorized email servers in their DNS records, up to a limit of 255 characters
- **Domain-based Message Authentication Reporting and Conformance (DMARC):** A protocol which uses DKIM and SPF to determine whether an email is authentic
- **Email Security Gateway:** A device used to filter inbound and outbound email and provide a variety of extra features
- **Ephemeral Keys:** A TLS concept in which Diffie-Hellman keys are only usable once or temporarily, so those keys being exposed do not compromise past communications
- **Simple Network Management Protocol (SNMP):** A protocol which is used to monitor and manage network devices
- **Management Information Base (MIB):** The database established by an SNMP device
- **SNMP Trap:** A message sent from a network device to an SNMP manager when the device encounters a problem
- **File Integrity Monitor:** A control which detects changes to files and filesystems that appear abnormal
- **Domain Name System Security Extensions (DNSSEC):** An extension of DNS which attempts to ensure DNS information isn't modified or malicious. DNSSEC does not provide encryption, and therefore does not provide confidentiality
- **Simple Network Management Protocol version 3 (SNMPv3):** An improvement on SNMP that provides authentication of message sources and confidentiality via encryption. The use of encryption isn't enabled by default
- **Secure Real-Time Protocol (SRTP):** A secure version of RTP, a protocol for providing audio and video streams. SRTP implements encryption and authentication
- **Secure / Multipurpose Internet Mail Extensions (S/MIME):** An extension of MIME that allows for attachments to be encrypted and requires the use of certificates signed by a CA
- **IPSec:** A suite of protocols used to protect IP traffic
- **IPSec Authentication Header (AH) Mode:** An IPSec implementation that uses hashing and a shared secret key to ensure data privacy and validate senders
- **IPSec Encapsulating Security Payload (ESP) Mode:** An IPSec implementation with two modes: tunnel and transport mode. In tunnel mode, the whole packet is encrypted and authenticated; in transport mode, only the payload of the packet is secured
- **On-Path / Man in the Middle (MitM) Attack:** An attack in which an attacker gets traffic meant for another destination to be sent to them, at which point they can monitor or modify the traffic
- **SSL Stripping:** A type of MitM attack in which TLS encryption is removed from traffic ??
- **Browser-Based On-Path Attack (MitB):** A type of MitM attack which relies on a trojan placed on the user's browser to bypass TLS encryption
- **Domain Hijacking:** An attack which changes the registration of a domain to grant the attacker control
- **DNS Poisoning:** An attack in which an attacker, through some means, places a malicious DNS record on a victim's machine
- **Credential Replay:** An attack in which an attacker captures valid network data and re-sends the data to receive the response themselves
- **UDP Floods:** A type of DDoS that can be done with limited resources by flooding the target with many UDP packets
- **ICMP Floods / Ping Floods:** A type of DDoS that can be done when the botnet has access to more bandwidth than the target utilizing ICMP ping commands
- **SYN Floods:** A type of DDoS that repeatedly sends SYN handshake initiators to the target to consume TCP resources
- **Amplified DoS Attack:** A DoS attack which takes advantage of protocols that allow a small query to return large amounts of results such as DNS
- **Reflected DoS Attack:** The use of a spoofed IP address to make it appear as though a legitimate service conducted the attack

## Secure Network Design

The foundation of a secure network doesn't lie in the controls that you use, but a well-defined and well-architected network setup that considers security from the start. An understanding of an organization's network can begin with the OSI 7-layer model, which defines separated network "layers" that each handle different types of traffic. The OSI model is split into two "groups" - the media layers, made up of 1-3, and the host layers 4-7.


| #   | Layer Name   | Data Handled                                           | Technologies                           |
| --- | ------------ | ------------------------------------------------------ | -------------------------------------- |
| 1   | Physical     | Electrical or light pulses, radio waves                | Cables, NICs                           |
| 2   | Data Link    | Data format for network, error detection, flow control | Frames, Ethernet                       |
| 3   | Network      | Physical path decisions, addressing, routing           | IP, ICMP, IPSec                        |
| 4   | Transport    | Transmission of data and error control                 | TCP, UDP                               |
| 5   | Session      | Authentication, sessions, permissions                  | OSI Protocol Suite                     |
| 6   | Presentation | Format data, handles encryption and compression        | AES, RSA                               |
| 7   | Application  | Interfaces with user                                   | Applications with UI, Bash, PowerShell |

During the physical and logical layout of network components, there are many, many considerations. Here is a brief list:
- **Attack Surface** of the component or control - does the component provide any new leverage for an attacker who is looking to get into your network? What about one who's already there?
- **Device Placement** - should the device be physically airgapped? Does it need to be in a specific place to ensure connectivity? Can an attacker utilize physical access to compromise the device? Should the device be placed in a VLAN?
- **Security Zones** - does the device fit into a grouping of other devices that may need to share permissions? Does the device need to be exposed to a greater degree of risk than other devices in order to function? It may need to be placed in a dedicated security zone.
- **Failure Modes** - when the device detects a failure state, should it allow all traffic (fail-open) or deny all traffic (fail-closed)? What can the device detect as a failure state? Is the risk of a compromise to the device more costly than potential downtime caused by setting it to fail-closed?

Extra thought should be given to network components that have to be *high availability (HA)*. These devices are critical for operation and therefore have security controls that allow them to be resilient in the face of potential compromise or issues. Typical HA setups involve being sure that the duty of the device can be offloaded to other devices or systems in the case that it fails.

Networks today are often architected using a *software-defined networking* setup, which allows network separation and configuration using software solutions or code. This provides solid control over the devices in a network - SDN opens up possibilities of configuration via asset and system classification, dynamic network tuning based on logs or data, and the isolation of potentially problematic systems as determined by monitoring software. Larger implementations of SDN are often called SD-WANs, which combine a variety of protocols that a network may use under one software-defined network in order to optimize costs and availability. Finally, SASE solutions take SD-WANs further by combining the WAN with solutions like firewalls, CASBs, and zero-trust networks.

## Network Segmentation and Zero-Trust

Network segmentation is a common and important consideration when designing a secure network. Not every device needs to communicate with one another, nor does every device require the same level of network traffic scrutiny. For this reason, devices are often placed into different network segments to organize them.

VLANs are the most common form of network segmentation. A VLAN is set at the router or switch level, and it provides an insulated broadcast network for devices to communicate with one another. Screened subnets are a specific implementation of network segmentation used when systems have to, by virtue of their jobs, be exposed to low-trust network environments. Intranets are internal organization networks meant to serve a purpose to only those within the organization and be isolated from the greater internet. Extranets are networks setup for only specific external clients.

*Network Access Control*, or NAC, systems seek to prevent unauthorized access to a network from the outside in. Their focus is on whether it's reasonable for a device requesting access to be able to authenticate into the network. One way NAC systems do this is by using a client installed on the endpoint to collect information about installed software, operating system and application configuration, user identity, and use patterns to validate whether a user should be able to connect. While this approach is more in-depth, providing more accurate data and judgements, it's also difficult to maintain. A more lightweight solution is "agentless", which means they run using something like a web browser without needing a local install. Finally, NAC systems are split into two types: preadmission or postadmission. Preadmission NAC systems will prevent a connection from ever being initiated if it's determined to be potentially dangerous, whereas a postadmission system prevents false positives from causing issues and still retains the ability to log and collect information about these logins.  

The **Zero-Trust** paradigm is a complex, rapidly-growing network architecture that presumes that no user is fully trusted and being authenticated into the network does not implicitly grant trust. In a zero-trust environment, subjects request use of resources from policy enforcement points, who then make a request to a policy decision point. The policy decision point passes along the request to a policy engine, which uses various different means, such as rule and access control lists, machine learning algorithms, or manually set conditions to determine whether the subject should be allowed to access the resource. The policy engine passes its decision onto the policy administrator, who either provides a communication path (such as connection information or a token) to the subject or requests the policy enforcement point deny them the connection. 

Important implementation details in a zero-trust framework include the complex workings of the adaptive identity system, which uses multiple factors, geolocation, system information, the particular privilege level being accessed, and more to make a decision about whether someone attempting to access a resource should be trusted. Threat scope reduction is also an important tenant of the system. It's closely related to the principle of least privilege, and asserts that a subject should be able to view and access only what's reasonable given their security level.

## Protecting Data in Transit

Switches and routers offer many security features to insulate them against intentional and accidental network-related problems. It's important to be aware of the issues that could pop up in your network even without an attacker trying to make it happen - and how you can preempt those issues.

MAC addressing is a technology designed without security in mind, and so there are a number of vulnerabilities like MAC flooding and MAC spoofing that can arise. One solution to these issues is *port security*, a feature commonly shipped with enterprise routers. Port security limits the number of MAC addresses allowed to utilize a single port - either to a cap, or from a list of acceptable MACs. Port security should be implemented as part of a defense-in-depth strategy, typically with a NAC solution, because MAC spoofing prevents port security from being a singularly reliable method to prevent unauthorized connections.

Loop prevention modules seek to prevent network traffic from being infinitely repeated, wasting bandwidth and overloading networks.  Broadcast storm prevention systems (also storm control systems) prevents network traffic that both loops and amplifies from overtaking a network. BPDU Guard protects STP by preventing ports that should not send BPDU messages from sending them. DHCP snooping prevents rogue DCHP clients from handing out IP addresses in place of the router.

##### VPNs and Tunnels

VPNs create a connection through a public network that allows a client to act as though it's inside the LAN of a network that is actually remote. Built into most VPNs are encryption and authentication technologies to prevent data from being leaked. There are two major implementations of VPN:
- **IPSec VPNs** require a client and, like most IPSec implementations, can operate in either tunnel or transport mode. Tunnel mode fully secures the IP packet with encryption, whereas transport mode leaves the header information unencrypted. IPSec VPNs are used for site-to-site connections and VPNs that need to transport a variety of different traffic types.
- **SSL VPNs** use TLS (ha ha) to provide data security through a web interface or through a client and tunnel. SSL VPNs are more accessible due to not always needing a client and server configuration, and they also provide the ability to split tunnel, which means that some traffic will be sent over the VPN while other traffic is sent through the internet connection used to establish the VPN.

Finally, VPNs are distinguished by whether they are remote access or site-to-site. Site-to-site VPNs connect two specific networks, whereas remote VPNs can connect a user to a network from anywhere.

## Network Security Tools

There's an abundance of physical and logical security controls to establish on your network that manage traffic, take and aggregate logs, detect intrusions, distribute traffic, and more. Some of these devices are purpose-built, while some are software that may run on operating systems you're already familiar with. Choose which security controls you implement carefully, considering time to acquisition, difficulty of setup, customer support, and any other restrictions your organization may face.

*Jump servers*, or jump boxes, are a way to provide access between different network security zones. They allow this access carefully, establishing a paper trail that may come in useful in investigations. 

*Load balancers* are a type of technology that maximizes availability, response time, and flexibility by distributing traffic meant for one service across multiple systems. The most common load balancing setup involves the service being given a Virtual IP (VIP), which is assigned to the load balancer, who then distributes the traffic to the machines under it according to its configuration. Active/active load balancers distribute the computing load across multiple actively powered systems. Active/passive load balancing systems spin up new systems when the main systems in charge of a certain functionality go offline or fail health checks.

**Proxy Servers** sit between the client and the server to manage network traffic by filtering, modifying, or blocking requests and responses. There are two main types of proxies: forward proxies, which run inline in the connection and forward the requests from client to server, and reverse proxies, which also sit inline but instead help with load balancing and caching.

*Web filters* are a type of proxy that specifically looks for web traffic that breaks content based rules. These tend to be used to prevent endpoints from visiting web sites which are known or suspected to be harmful, often with the assistance of reputation lists or automated scanning tools.

*Intrusion Detection Systems* and *Intrusion Prevention Systems* utilize one of two methods to determine whether network traffic is insecure. The first is signature-based detection, which uses known hashes of malicious files as an indicator of compromise. The second is anomaly-based detection, which collects data to establish a "baseline" understanding of regular internet traffic before being switched on to detect traffic that does not fit that baseline. 

## Securing Common Attack Vectors

**Out-of-band Management** refers to the ability to interface with and manage network devices without being on their network. Considering how to handle out-of-band configuration can be an important part in the disaster recovery process. Out of band management can be achieved by placing access to administrator consoles on a separate VLAN or segmented network. While physical access to the system does technically count as out-of-band management, this can make the lives of disaster recovery personnel very difficult and so should ideally be avoided as the primary method.

**DNS** is a quintessential technology for resolving internet connections. DNS was never designed with security in mind, so there exist many attacks that seek to take advantage of it. Use of DNSSEC - the security extension suite for DNS - can help lessen the attack surface of DNS in your organization. DNSSEC implements authentication first and foremost, allowing a system to be sure that a DNS response is coming from a valid DNS server. This helps to combat DNS poisoning attacks. DNS filters are another way to secure DNS - DNS filter lists simply allow DNS requests made to known malicious services to be redirected.

Email remains extremely widely used on the internet today, and the people who originally designed email also did not consider security whatsoever. A huge amount of effort has been put into various different methods of securing email, and today many mechanisms exist to ensure emails are secure in transit and sent from trusted servers. These approaches include DKIM, SPC, DMARC, and S/MIME. DKIM utilizes asymmetric encryption to ensure that they are from the domain they claim to be from (since a user can claim to send email from any server). DKIM signs the body of the message and some of the header, as well as adding a DKIM signature header, which is a signature that is checked against public keys registered with DNS. SPF allows organizations to add a list of authorized email servers to the end of their DNS records. The two come together with DMARC, which checks the DKIM signature against the list of authorized mail servers defined by SPF to determine if mail was legitimately sent. Finally, email security gateways provide an extra layer of defense and functionality, which includes reputation checking, spam filters, encryption, and more.

##### Related Network Protocols

As a side note, it's important to understand the use of *ephemeral* TLS keys. TLS is the transport layer security that powers the majority of secure protocols and encrypted traffic transmission. In order for TLS keys to be exchanged at the start of a session, a Diffie-Hellman key exchange takes place. The details of the exchange are covered in a prior chapter - the important part now is that the exchange used for TLS is known as an *ephemeral* Diffie-Hellman key exchange. These keys are only temporary, so the worst an attacker can do if they break the key exchange is listening in on traffic for that one session. Prior and future communications are not compromised.

Also, the *SNMP* is an important concept in local network management. The SNMP, as the name suggests, is a relatively simple way to monitor the state of network and endpoint devices. An SNMP manager sits on the network and maintains a Management Information Base (MIB) which contains the details of the objects in the network. If a network device has a problem, it can send a message known as an SNMP trap to the manager so that the manager can take some action.
##### Using Secure Protocols

Many, many networking protocols were not originally designed with security in mind. Most of these protocols have had "secure" versions implemented. Where possible, it's preferable to use the secure versions of protocols. Below is a table of common network protocols and their safe alternatives, if applicable.


| Protocol                    | Use                                                           | Port #    | Secured Protocol | Secured Port # |
| --------------------------- | ------------------------------------------------------------- | --------- | ---------------- | -------------- |
| Session Initiation Protocol | Media Streaming                                               | 5060/5061 | SIPS             | 5060/5061      |
| Realtime Transport Protocol | Media Streaming                                               | ~         | SRTP             | ~              |
| Network Time Protocol       | Time Syncronization                                           | 123       | NTS              | 4460           |
| HTTP                        | Sending Web data over IP                                      | 80        | HTTPS            | 443            |
| IMAP                        | Handling Email                                                | 143       | IMAPS            | 993            |
| POP                         | Handling Email                                                | 110       | POP3S            | 994            |
| FTP                         | Transferring Files                                            | 21        | SFTP (SSL)       | 22             |
|                             |                                                               |           | FTPS (TLS)       | 21/990         |
| LDAP                        | Managing User and System information in a directory structure | 389       | LDAPS            | 636            |
| Border Gateway Protocol     | Network Routing                                               | 179       | x                | x              |
| DHCP                        | Network IP Assignment                                         | 67/68     | x                | x              |
| DNS                         | Domain Name Resolution                                        | 53        | DNSSEC           | 53             |
| SNMP                        | Network Device Management                                     | 161/162   | SNMPv3           | 161/162        |

Lastly, **IPSec** provides two distinct usage modes that are important to consider. There are two that you need to know:
- **Authentication Header (AH)** mode uses hashing a symmetric encryption to ensure integrity and authentication for the entire IP payload
- **Encapsulating Security Payload (ESP)** mode operates in two ways. In tunnel mode, it does a similar job to AH mode, providing integrity and authentication checks for the whole packet; in transport mode, it only protects the data and not the headers.