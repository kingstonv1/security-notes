---
title: Chapter 9 - Resilience and Physical Security
tags:
  - "#project/comptia"
  - "#notes"
start: 04/17/2025
---
## Vocabulary

- **Continuity of Operations:** Ensuring that operations will continue even if issues occur
- **Geographic Dispersion:** A principle that states facilities should be placed geographically apart, typically by at least 90 miles
- **Load Balancing:** A system which uses multiple systems or sets of hardware to distribute the resource usage of one service
- **Clustering:** When groups of computers are connected together to perform the same task
- **Uninterruptible Power Supply (UPS):** A system which provides battery or other power generation systems when primary power sources are out
- **Managed Power Distribution Units (PDUs):** Systems which provide intelligent and remote control of power to systems
- **Platform Diversity:** The usage of different vendors, cryptographic solutions, platforms, and controls to accomplish the same ends
- **Resilience:** A component of availability that determines what type and level of disruptions the service can handle without availability being compromised
- **Ease of Deployment:** The complexity and work required to deploy the solution, including initial and ongoing costs
- **Redundant Arrays of Inexpensive Disks (RAID):** Multiple disks which hold redundant data. Can be striped (copy is spread across disks) or mirrored (copy is on one disk)
- **Journaling:** Creating a log of changes which can be played back if an issue occurs
- **Recovery Point Objective:** The desired, reasonable amount of data that should be lost when a recovery process is utilized
- **Recovery Time Objective:** The desired, reasonable amount of time that recovery should take
- **Full Backup:** A backup which includes all the files on a filesystem
- **Image:** A backup which includes every bit on the drive
- **Snapshot:** A copy of the disk contents, not including the OS
- **Storage Area Network (SAN):** A dedicated network that connects servers to storage devices, allowing for a shared storage pool
- **Network-Attached Storage:** A storage center that allows multiple computers over a network to utilize its storage
- **Vertical Scalability:** The ability of a service to increase throughput by utilizing a higher-resource machine
- **Horizontal Scalability:** The ability of a service to increase throughput by utilizing more machines
- **Hot Sites:** Redundant sites which have all the infrastructure and data required to fulfill the needs of the organization. Very expensive but can be utilized in non-disaster scenarios
- **Warm Sites:** Redundant sites which have some or all of the systems or infrastructure needed, but not the live data
- **Cold Sites:** Redundant sites which have space, power, and/or internet but not systems, personnel, or data 
- **Capacity Planning:** Allocating resources to deal with future demands, especially during a crisis
- **Tabletop Exercises:** Detailed discussions between incident recovery personnel to validate a recovery plan
- **Simulation Exercises:** Drills or practices in which personnel simulate what they would do in an actual incident
- **Parallel Processing Exercises:** An exercise in which processing is moved to a hot site or alternate site to validate that the site works as expected
- **Failover Exercises:** An exercise in which a full failure of a site or system is tested
- **Infrared Sensors:** Sensors that rely on changes in infrared light, or heat radiation, to detect changes
- **Microwave Sensors:** Sensitive sensors that detect motion and heat signature changes in a room or space
- **Ultrasonic Sensors:** Proximity detection sensors that are set off by vibrations
- **Environmental Attack:** An attack that seeks to disrupt a physical space's environment - temperature, sprinkler systems, air quality or visibility, etc
- **Nearline Backups:** Backup storage that's not *immediately* available, but can be retrieved in a reasonable amount of time
- **S3 Glacier / Coldline Storage:** Amazon and Google's low-price, slow backup storage services

## Resilience in Security Architectures

The availability of systems is sometimes overlooked, especially when it comes to resilience - the ability to recover from incidents, manmade or otherwise, with little time and resource loss. The principle behind this is called *continuity of operations.* Organizations seek to maintain continuity of operations because system outages are often very, very expensive. 

The first major approach to establishing resilience in a system is through **redundancy** - you should have multiple sets of resources, computers/servers, or your data. That way, if one system or set is affected, there is at least one more to back it up. Redundancy can be established through geographic dispersion - a setup in which duplicate resources are placed 90+ miles away from another physically. This insulates the overall system against local issues like natural disasters, grid problems, or internet outages. Within a single location, computing resources may be separated physically and/or put on different power distribution systems. Some network topologies also allow different ways to route traffic to a destination - this prevents a single point of failure from taking down operations on that network.

There is also a concept of resilience as it relates to computing resources. Scalability concerns are a part of this, as well as concerns that one computer or server rack going down can severely harm infrastructure. There are two core ways to protect against these concerns: *load balancing*, which are important because they provide security as well as an avenue for upgrading computing resources according to demand, and *clustering*, which is hyper-resilient against individual computer outages. Platform diversity works to solve similar problems - if one service or application for a security or system solution fails, your organization should have a plan B that is implemented or can be implemented.

**Data storage resiliency** is critical in many, many systems where there is business-critical data to be processed. Redundant storage, journaling, and backups are all ways to accomplish data storage resiliency, with differing implementation details, advantages, and drawbacks.

You may want to keep your data in one place, but without the possibility of a single-drive or single-computer failure compromising the information. The solution for this is *Redundant Arrays of Inexpensive Disks*, or *RAID*. The goal of RAID is to ensure parity - or noncorrupted/lost data. Here is a table of RAID setups.

| RAID Setup                       | Description                                                                         | Advantage                                                                                          | Disadvantage                                            |
| -------------------------------- | ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| RAID 0 - Striping                | Data is spread evenly across all drives in the array                                | Best speed; all disk capacity put to use                                                           | If one drive is lost, that data is gone                 |
| RAID 1 - Mirroring               | All data is duplicated to one or more drives                                        | High read speeds; one disk failure does not lose data                                              | Uses 2x the storage                                     |
| RAID 5 - Striping w/ Parity      | Data is striped using RAID 0, then another drive stores data checksums.             | Data reads are fast, while writes are slower. Drive failures can be rebuilt with the parity drive. | Tolerates 1 drive failure at a time. Rebuilding is slow |
| RAID 10 - Mirroring and Striping | Requires 4x the storage, with drives added in pairs. Data is striped then mirrored. | High speed due to striping, and disk failures do not constitute data loss                          | Uses 4x the storage                                     |

In addition to data redundancy, journaling and backups exist to allow an organization to "roll back" after data loss. Journaling is a kind of pseudo-backup in which the changes applied to a filesystem are tracked from a given point. You can't restore from a journal without first restoring to the state the system was in when the journal was started (or somewhere after). *Replication* is also a pseudo-backup system in which data is regularly copied to a secondary system or site. Replication is distinguished from backups because it's not periodic, it's continuous - changes are replicated live as they are made.

##### Backups

Finally, backups are the most common way to achieve data security in computing systems. Backups come in a great deal of implementations and flavors, but the idea of a backup is to create a complete copy of the data in question that can be "restored" as needed later. Backups setups are distinguished by how often the backups are taken, how, and what data is contained within the backup.

- **Full Backups** back up all of the files on a filesystem, including those belonging to the OS.
- **Incremental Backups** copy only the data changed since the last backup. These save space but require a prior full backup.
- **Snapshots** capture the state of the data on a filesystem, but exclude OS files. Snapshots are typically used where the OS setup is consistent, such as VMs or cloned containers.
- **Images** capture every bit on the drive.

Backup storage is the next important consideration to make after the actual backup process. Four backup mediums to know about are:

- **Tape**, which is low-cost and easy to store. Often, organizations have "tape robots" to quickly manage, read, and write tape backups.
- **Disks**, which are more expensive than tape but often much faster. Disk backup storage is typically implemented using a NAS or SAN setup.
- **Optical Media**, like Blu-Ray disks or DVDs, are still used sometimes but do not hold large capacities of data well.
- **Flash Media**, like SD cards or USB drives, are used typically for small-scale or file-level backups, especially in a pinch.


## Capacity and Incident Planning

It's critically important to have recovery plans and resources set up for different types and severities of incidents. Capacity planning is the first consideration. You must be sure that your organization is able to meet the increased personnel, technology, and infrastructure needs that an incident may require. Capacity planning is split into three areas:
- **People**, who provide the labor and skillsets needed to recover from a disaster. It's difficult and expensive to keep personnel to perfectly handle every security incident, but you must keep enough people to respond to different levels of incident, and be sure those people can actually access the resources they need to during recovery. Organizations can use third-party help or contractors for this, or simply employ people across a geological range, some nearer their recovery sites.
- **Technology**, which are the tools that an organization uses on their systems. It's important to understand how a security incident affects your business-critical tools at an individual level, and to have plans or alternate tools in case things go wrong.
- **Infrastructure**, which are the compute and network resources required to run your organization or recover from an incident. This includes redundancy and volume of network bandwidth, storage, and computing power.

In the course of planning, you'll want to run drills to be sure your dedicated recovery systems and personnel are able to handle an actual event.
- **Tabletop Exercises** are simply discussions of plans between recovery personnel. They provide no risk to the company but also provide the least amount of assurance that the plans work in practice.
- **Simulation Exercises** simulate what would be done in an actual event. There are a variety of ways to apply simulation exercises, some more intrusive than others.
- **Parallel Processing Exercises** are exercises in which processing is moved to an alternate site so that the backup and recovery processes can be validated at the main site and the hot site can be confirmed to work properly. These exercises have potential to disrupt an organization's functioning if processing is not successfully moved.
- **Failover Exercises** test a full failure state in the main systems, but often in a way that attempts to prevent availability issues.