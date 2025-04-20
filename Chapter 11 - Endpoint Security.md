---
title: Chapter 11 - Endpoint Security
tags:
  - "#project/comptia"
  - "#notes"
start: 04/19/2025
---
## Vocabulary

- **Firmware:** The embedded software that allows devices to function
- **Endpoint:** The device at the end of a network - typically a PC, mobile device, or server
- **Unified Extensible Firmware Interface (UEFI):** A standard for interactable device firmware
- **Basic Input/Output System (BIOS):** The traditional way to interact with device firmware
- **Original Equipment Manufacturer (OEM):** The manufacturer of a piece of equipment
- **Secure Boot:** A setup which attempts to ensure that a device only boots with firmware/software approved by the OEM
- **Trusted Platform Module (TPM):** A dedicated chip to apply security features
- **Measured Boot:** A setup which attempts to prevent boot-level malware by measuring aspects of the boot process and storing/validating them on a TPM
- **Hardware Root of Trust:** The central authority that hardware trusts to store and validate keys, often a TPM
- **Secure Enclave:** Apple's hardware security solution, built into their System-on-Chip (SoC) modules
- **Hardware Security Module (HSM):** A physical device which holds and manages cryptographic keys for multiple systems
- **Key Management System:** A system which stores and manages keys and certificates centrally
- **Endpoint Detection and Response (EDR):** Endpoint logging and monitoring tools that analyze data about the host system to detect suspicious activity or data
- **Indicators of Compromise (IoCs):** Signs left behind on a system that a compromise has occurred
- **Extended Detection and Response (XDR):** Systems which consider endpoint and network and tech stack data when looking for suspicious activity
- **Data Loss Prevention (DLP):** Tools that track and prevent sensitive data from being exfiltrated from the network or endpoint
- **Host-Based Firewall:** Simple firewalls built into many OSes that allow or deny traffic based on application, port, or protocol
- **Host-Based Intrusion Prevention System (HIPS):** A system which analyzes network traffic before services or applications on the host can process it to take action on the traffic
- **Host-Based Intrusion Detection System (HIDS):** A system which analyzes network traffic before services or applications on the host can process it but *cannot* take action on the traffic
- **System Hardening:** Changing the default configuration of an endpoint to decrease its attack surface
- **Group Policy Objects (GPOs):** A windows feature which allows system administrators to create pre-built configuration baselines to be deployed via Active Directory
- **Security Compliance Toolkit:** A windows feature which allows comparison and auditing of GPOs based on secure baseline configurations
- **Security Enhanced Linux (SELinux):** A kernel-based security model that runs atop Linux to add many security features, such as a Mandatory Access Control setup
- **Configuration Management:** A tool which helps to enforce and manage the configuration of endpoint system settings
- **Configuration Enforcement:** The process by which configuration management tools ensure that endpoint configurations are not changed through continual monitoring
- **Full-Disk Encryption (FDE):** A setup in which the full contents of a disk are encrypted and the bootloader or TPM provides a key at boot time
- **Transparent / On-The-Fly / Real-Time Encryption:** An implementation of FDE which decrypts data as it's used
- **Volume / Filesystem Encryption:** Encrypts different volumes of the drive separately, allowing for configurable setups per-volume
- **Self-Encrypting Drive (SED):** A drive which implements encryption at the hardware and firmware level, often requiring an external key to boot
- **Embedded Systems:** Computer systems build into other devices
- **Real-Time Operating System:** An OS that prioritizes quickly handling incoming data over all else, often used in embedded systems
- **Industrial Controls System (ICS):** A broad term for industrial automation
- **Supervisory Control and Data Acquisition (SCADA):** Large systems which run industrial infrastructure, often overlapping as a term with ICS
- **Internet of Things (IoT):** A broad term used to describe network connected devices that are used for a variety of tasks
- **Decommissioning:** Removing a device or system from service, removing it from inventory, and making sure no sensitive data remains on the device
- **Certification:** A process that documents and asserts that a device or asset was properly decommissioned

## Device Protection

Endpoint devices are the most plentiful in nearly every organization, and so a great deal of attention should be paid to making sure that they are kept secure. The first point of concern in an endpoint device is its *firmware* - the low level, integrated software that allows the hardware to do its job. Firmware attacks can occur through a variety of paths, from applications on the OS, to physical access, to the surrounding networks. Firmware attacks are particularly dangerous because they bypass the operating system and filesystem of a device - meaning re-imaging won't get rid of any persistent threats after compromise. For this reason, firmware validation techniques are very important.

*Firmware validation* is often done at boot-time. This validation can be performed in two different ways.
- **Secure Boot** attempts to ensure that the firmware running on the device is identical to the firmware that the OEM shipped (or another trusted version) using verified signatures checked against keys shipped with the device. These keys are often stored in a secure module on the device, such as a TPM.
- **Measured Boot** attempts to ensure that the firmware running on the device operates in a reasonable manner that would indicate it is not malicious. It does so by taking various points of data about the boot process and comparing them against a baseline. Typically this processing is also done on a chip such as a TPM. This method allows logging so that remote servers can also analyze the boot process on their own.

Both systems require a *hardware root of trust* which the device inherently trusts to hold keys and validate information. The TPM chips that usually act as hardware roots of trust have three key features:
- **Remote Attestation**, which means the TPM is allowed to determine whether configurations are valid or secure
- **Binding**, which means the TPM can perform encryption on data
- **Sealing**, which means the TPM can decide whether it's appropriate to decrypt data based on the state of itself and surrounding hardware

Other devices that can be used as hardware roots of trust include unmodifiable serial numbers and physically unclonable functions (PUFs).

## Endpoint Security Tools

After boot, the operating system and applications running on an endpoint present limitless security issues. Of course, custom software can now be installed to counteract these issues.

**Endpoint Detection and Response** tools are a rapidly growing field of tools which sit on an endpoint device and collect data/logs, then analyze that data to determine if data or actions taken on the device are indicative of an attack. EDR systems look for these indicators of compromise in a variety of ways, including using engines driven by AI/Machine Learning which seek to determine which behaviors are suspicious and nonsuspicious. EDR systems' usefulness to large organizations lies in its ability to make the massive amount of data collected accessible and useful when necessary, instead of having people manually comb through everything.

**Extended Detection and Response** tools are similar to EDR systems, except they also take into account the technology surrounding the endpoint - they are more embedded on the network and consider networking equipment, other endpoints, cloud services, etc.

**Data Loss Prevention** systems also serve an important purpose by allowing an organization to classify and track data belonging to them, as well as tracking and enforcing how the data is handled on endpoint devices. DLP systems often reside on both endpoint and network to provide greater security. Some DLP systems have extra functionality to encrypt or tokenize data when it is sent out of "safe zones" or wipe data altogether if it appears to be at risk.

##### OS Hardening

The default configurations that ship with many OSes, even enterprise packages, tend to be unnecessarily open. This allows attackers more ways to get into the endpoint system - also called having a larger attack surface. For this reason, strong configuration and modification of default OS settings, also called hardening, is an important part of endpoint security.

Enterprise-level demands have created solutions for the most commonly used OSes that allow system administrators to deploy and maintain configurations across a network. In Windows, this is most typically done using Group Policy. Sysadmins can create Group Policy Objects, which are sets of configurations to be applied to a Windows machine. They do this by first starting with a sensible baseline, often taken from an organization like the Center for Internet Security, and then tweaking the object based on their organization's needs. Different GPOs may be configured for different users or different roles. Once a GPO is created, it can be remotely applied to a computer within the network using AD. Microsoft supplies a toolkit to work with and audit Group Policy Objects called the Security Compliance Toolkit. 

However, native Windows tools aren't the only tools available to configure, deploy, and maintain configuration policy. Configuration management tools like Jamf Pro for Mac or CFEngine help with this process. It's important to understand the three-step process for configuration management:
- *Establishing* a baseline configuration, typically by using an existing standard and then making modifications based on your organization's needs
- *Deploying* that configuration to the applicable machines on your network
- *Maintaining* that configuration to ensure that the configuration is not changed maliciously or accidentally, typically by implementing periodic monitoring of systems over the network

## Securing Embedded and Specialized Systems

Embedded systems are everywhere, providing computing resources to devices in places you may not expect them. While some embedded systems may run low-power hardware with low capabilities, some embedded systems may run powerful hardware with fully fledged OSes that users can interface with normally. If your organization makes use of embedded systems, it's important to understand their security requirements and the types of controls that you can apply to them.

Embedded systems suffer from many of the same vulnerabilities that typical endpoints do - they are often deployed with poor default configurations, unpatched software, or user setup mistakes. For this reason, some of the controls deployed on some embedded devices may be similar to those deployed on typical endpoints. However, where securing embedded may become difficult is when computing power on the device is very limited. In these cases, the system will often run a customized RTOS to ensure quick processing of data. This can leave someone looking to secure the device with a lack of processing power to implement security controls like authentication or encryption.

SCADA and ICS systems are particularly vulnerable, as they utilize a mix of embedded and typical endpoints in a way that is often not designed to be secure. Despite this lack of focus on security, SCADA/ICS systems are often critically important to the functioning of organizations that they are used by. Typically, each device in a SCADA/ICS setup should be considered individually - typical endpoints can be secured using typical methods like authentication, encryption, patching, firewalls, etc, while more advanced or tailored controls may need to be implemented for RTUs or IoT devices. When controls can't be implemented properly on devices in an ICS, it should be isolated from access by external networks and unauthorized personnel as much as possible. While sometimes preventing a device from connecting to the internet is useful as a security control, sometimes it is unable to be connected to the internet and therefore unable to send logs or interface with central security services. A final consideration is the cost of replacing embedded systems - it's often impossible to just replace the computer, instead requiring an organization to replace the whole associated unit.

Finally, alternate methods of communication between IoT and other devices should be considered. Not every device is Wi-Fi capable, nor is it practical to connect every capable device to Wi-Fi. For this reason, IoT devices often rely on other methods of communication, with their own benefits and drawbacks.

Cellular connectivity is a popular choice for this scenario, but it comes with its own security concerns. Ensuring traffic is not intercepted using encryption is an important consideration. Securing the Subscriber Identity Module (SIM) card built into the device is also important - if the data on the SIM is exposed, an attacker can perform a SIM redirection attack to send and receive data as if it were the device in question.

Radio frequency protocols like Zigbee are another choice for communication here, especially in devices that don't require high fidelity connection or added features provided by Bluetooth. These devices typically don't have strong security modules or security support.