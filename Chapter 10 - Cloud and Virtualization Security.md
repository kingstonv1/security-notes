---
title: Chapter 10 - Cloud and Virtualization Security
tags:
  - "#project/comptia"
  - "#notes"
start: 04/19/2025
---
## Vocabulary

- **Cloud Computing:** A setup in which a cloud service provider allows other organizations to use their computing services over the internet
- **Oversubscription:** The idea that cloud providers can grant permissions to customers to provision more resources than the provider actually has, because not everyone will always use all of their resources. The idea is similar to airlines overbooking plane tickets
- **Multitenancy:** The idea that multiple organizations can utilize the same shared pool of resources
- **Cloud Service Provider:** A firm that offers cloud computing services to customers
- **Cloud Consumer:** An organization or individual who purchases cloud services from a CSP
- **Cloud Partner:** An organization that offers ancillary products or services that support or integrate with the offerings of a CSP
- **Cloud Auditor:** An independent organization that provides assessments of cloud services and operations
- **Cloud Carrier:** The intermediaries that provide the connectivity that allows the delivery of cloud services
- **Infrastructure as a Service (IaaS):** A cloud setup in which processing, storage, or network resources are provided to build on top of
- **Platform as a Service (PaaS):** A cloud setup in which infrastructure and extras, such as deployment environment or tooling, are offered by the cloud provider
- **Software as a Service (SaaS):** A cloud setup in which an app or service is offered to the consumer with limited configuration options, typically on a subscription model
- **Function as a Service (FaaS):** A type of PaaS setup in which consumers can upload code functions to be executed on a timer or based on conditions. Also called serverless computing
- **Managed Service Provider (MSP):** An organization which serves remote IT management to organizations. Also called an MSSP when security is part of the agreement
- **Public Cloud:** A multitenant cloud model in which anyone can purchase and use a pool of cloud resources
- **Private Cloud:** Cloud infrastructure provisioned for a single customer
- **Community Cloud:** A multitenant cloud model provisioned for use by an exclusive group of customers
- **Hybrid Cloud:** A cloud setup that deploys public, private, or community cloud offerings together in some way, with mechanisms to bridge between them
- **Bursting:** Utilizing private cloud offerings in most cases and scaling up past max capacity using public cloud resources
- **AWS Outpost:** A type of hybrid offering in which customers request hardware that they install in their own datacenters. The rack is maintained by AWS but provisioned in the same way as typical private AWS resources
- **Shared Responsibility Model:** A model in which multiple cybersecurity teams or organizations are responsible for the safety of data
- **Cloud Security Alliance (CSA):** An industry organization focused on developing and promoting best practices in cloud security
- **Cloud Controls Matrix (CCM):** A spreadsheet created by the CSA which documents cloud security controls and their appropriate uses
- **Edge Computing:** The use of some processing power in distant IoT devices to pre-process data in places where it may be impractical to send back to the cloud
- **Fog Computing:** The use of IoT gateway devices physically near sensors to do edge preprocessing
- **Type-I Hypervisor:** Also known as a bare-metal hypervisor, a hypervisor OS that operates directly on the hardware
- **Type-II Hypervisor:** Hypervisors which run atop an existing operating system
- **Containers:** Units of virtualization that operate at the application level
- **Block Storage:** The allocation of large amounts of storage in a cloud setup which is then formatted as a virtual disk and accessed like a regular disk
- **Amazon Elastic Block Storage (EBS):** Amazon's block storage offering
- **Object Storage:** The placement of individual files in "buckets" which the user can access through an API without knowing the underlying storage details
- **Amazon Simple Storage Service (S3):** Amazon's object storage offering
- **Software-Defined Networking (SDN):** A setup which allows engineers to interact with and modify cloud resources through their APIs
- **Software-Defined Visibility (SDV):** A setup which allows engineers to interact with cloud logging and traffic information through their APIs
- **Security Group:** A control which allows a cloud consumer to define appropriate network and resource usage activity (like a cloud firewall)
- **Virtual Private Cloud (VPC):** The cloud substitute for a VLAN, which allows systems to be grouped into virtual clouds with rules that dictate allowed network traffic applied on a per-VPC basis
- **VPC Endpoints:** APIs which allow VPCs to communicate with one another
- **Cloud Transit Gateway:** A setup which allows cloud VPCs to integrate with on-premise VLANs
- **Infrastructure as Code (IaC):** The use of code to provision and deprovision a cloud provider's infrastructure resources
- **Data Sovereignty:** The idea that data is subjected to the legal restrictions of any country it is stored or used in
- **Virtual Machine Escape:** A type of exploit that allows a user of a VM to access resources dedicated to other VMs on that hypervisor
- **Virtual Machine Sprawl:** A problem that occurs when IaaS users create virtual machines that they do not use or forget about, leaving them to accrue costs and accumulate security issues
- **Resource Reuse:** When cloud providers re-assign resources from one customer to another without properly cleaning up first
- **API Inspection:** A control typically configured with WAF solutions that inspects API requests and endpoints for security issues
- **Secure Web Gateway (SWG):** A control that monitors web requests made by *internal users* and compares them to a security policy, blocking requests
- **Cloud Access Security Broker (CASB):** A software tool that serves as an intermediary between CSUs and CSPs to monitor user activity and enforce policy requirements
- **Inline CASB Solution:** A CASB solution which sits physically or logically in between the user and service. Inline CASBs can catch requests before they make it to the cloud provider
- **API-Based CASB Solution:** A CASB solution which does not interact with the user, but indirectly through the CSP's API
- **Resource Policy:** A piece of code that allows an organization to control the resources or actions that their users can request from a CSP

## Cloud Basics

Cloud computing is a movement that utilizes huge amounts of centralized computing resources controlled by companies known as Cloud Service Providers. Cloud Consumers can then provision those resources for use through the Internet, allowing organizations to access nearly limitless computing resources, only paying for what they need. This can be done by applications without the direct interaction of any human beings, allowing organizations to spin up and shut down resources to achieve elasticity. Cloud computing is controlled primarily by three big industry players - Amazon through Amazon Web Services, Microsoft through Azure, and Google through Google Cloud Platform. 

Cloud offerings typically are described as "{X}aaS". XaaS in itself is a term that describes this category of computing - it means "everything as a service". The most common "as a service" architectures offered by cloud providers are Infrastructure as a Service, Platform as a Service, Software as a Service, and Function as a Service. Infrastructure includes the hardware and facility resources that an organization may need to run its services - memory, computing resources, storage, and physical space. Platform as a Service goes one step further and also provides the operating system and tooling oriented to the purpose the consumer requires. Software as a Service does not provide any of those things - instead, it prevents a complete, managed application for the user to interface and use with their own data. Finally, Function as a Service allows developers to give cloud providers code functions that run under specific conditions or intervals. FaaS is sometimes referred to as "serverless computing" because the user does not have to interface with the server whatsoever, but there is (obviously) still a server running that code.

Cloud deployments are described with privacy models. Cloud offerings are described as public, private, community, or hybrid, depending on who is allowed to provision the cloud resources and in what way. In a public setup, anyone or any organization can pay to provision resources from the cloud provider. This means that multiple different organizations will use the same physical hardware - for some organizations, this prevents too much risk. Therefore, a private cloud setup can be created. A private cloud setup generally can be provisioned through the same methods as public setups, but they are reserved for one customer. A community cloud setup is simply a private cloud setup that is privately reserved for a specific group of customers. A hybrid setup is a catch-all term for cloud systems that fall into multiple of these categories - for example, AWS's Outposts allow users to set up their own AWS racks on-site that they can still manage using AWS APIs and gateways.

##### Cloud Computing Components

The most important underlying technology for cloud computing is *virtualization*. Virtualization allows individual servers or computers to be split into multiple operating units with less computing power or resources. The software that handles this resource allocation is called a *hypervisor*, and there are two types.
- A **type-I hypervisor** runs directly on the bare metal of the operating system in place of a typical OS and creates virtual machines with usable OSes on top of itself.
- A **type-II hypervisor** runs on an existing OS and creates virtual machines with usable OSes on top of itself.

While VMs which run an entire OS are popular, there is another virtualization model called *containerization*. In a containerization model, an OS is created from a "recipe" to fit the requirements of a specific application. This newly created OS is called a "container", and a typical container only runs one application or service. Containerization does not require extensive customization of an entire operating system every time a container is spun up, and allows organizations to build applications that scale horizontally by spinning up more containers.

When requesting storage resources from a cloud service provider, it's typical to be able to request *block storage* or *object storage*. Block storage is a section of a physical drive that is allocated to your organization and formatted as a virtual disk. Amazon's implementation of block storage is called EBS, Elastic Block Storage. Object storage is a setup in which an organization requests individual files or folders to be stored on the cloud provider's servers - so long as the organization can later go back and retrieve those files, they do not care how the files are stored. Object storage is typically preferred over block storage because it is significantly cheaper on average than block storage. AWS Simple Storage Service, also called S3, is Amazon's implementation of object storage.

## Cloud Networking and Security

Cloud networking is handled slightly different from on-premise networking, because it typically involves organizations defining how the CSP should handle their systems' networking through code. This setup is called Software-Defined Networking (SDN), and the logging and monitoring portion of this setup is called Software-Defined Visibility (SDV).

One example of Software-Defined Networking is Security Groups, which are essentially firewall rule lists defined through code to define allowed and disallowed traffic to virtualized containers and resources. Another example is the concept of a Virtual Private Cloud, or a segmented network of containers that can communicate with each other. VPCs are similar to VLANs in that they can have their own dedicated sets of firewall rules (security groups) and endpoints that allow them to communicate to other networks. Finally, there is an offering called a Cloud Transit Gateway which allows VPCs to communicate with on-site organization VLANs.

Infrastructure as Code is the process of provisioning and deprovisioning cloud infrastructure resources autonomously using applications or scripts. IaC allows for great amounts of elasticity in applications. Amazon's IaC provisioning service is called CloudFormation and it allows engineers to specify the infrastructure they need in JSON or YAML.

##### Attacks against Cloud Platforms

While the security set up by major cloud providers is generally very good, there are potential implementation flaws to be aware of, as well as unique risks that cloud computing architecture introduces. 

Firstly, while it may seem like availability is something cloud computing systems should be guaranteed to excel at, this isn't necessarily true. Often times, vendors offer more expensive high-availability systems for organizations that consider it a high priority. Cloud providers experience many of the same availability issues that standard on-premise organizations might, though this is helped by the fact that cloud systems are often well-distributed.

 A unique legal/compliance issue brought about by cloud computing is known as *data sovereignty*. The idea is that an organization is subjected to the data privacy regulations in any country where the data is transferred or processed - and in cloud computing setups, it's common for data to be passed through foreign nations for delivery or computing purposes. Therefore, organizations should pay close attention to where their data goes and how they can control it, so they don't have to worry about the legal compliance standard for every country ever.

Virtual machines prevent additional attack vectors and exploits to consider.
- **VM Escape Vulnerabilities** allow attackers to escape the VM they were granted use of and access resources the hypervisor has dedicated to other VMs. This is dangerous because it allows an attacker to access the private data of other cloud consumers on the machine. Hypervisors are meant to prevent this type of escape.
- **Virtual Machine Sprawl** can run up costs and vulnerabilities when old machines are left to stagnate.
- **Resource Reuse** is a mistake on the part of the cloud provider that allows one consumer to access another consumer's data in a less controlled manner than VM escaping.

##### Securing Cloud Platforms

There are on-site and virtual ways to promote secure use of cloud technologies. The most important of those for security+ are:
- **Secure Web Gateways (SWGs)**, which sit on the virtual network and inspect requests for resources. In a similar way to a WAF, the SWG is primarily intended to protect important resources by inspecting and/or blocking incoming resource requests.
- **API Inspection**, the process of inspecting an API and its incoming requests and outgoing data to determine if there are present security vulnerabilities
- **Cloud Access Security Brokers**, which inspect the resource requests and work done on a VPC done by an organization's users. CASBs can be either inline or API-based. Inline CASBs do their work similarly to a firewall, sitting between the user and the cloud provider and intercepting requests to determine if they follow policy or need to be blocked. API-based CASBs are "read-only" CASBs which do not block requests but use the cloud provider's APIs to determine if security policy has been violated.
- **Resource Policies**, which are specifications (typically in markup language) that are sent directly to the cloud provider that describe how the users in an organization should be able to request and use cloud resources.