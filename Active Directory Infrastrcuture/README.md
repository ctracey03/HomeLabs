# Windows Server Active Directory Homelab

## Project Overview

This project documents the design and deployment of an on-premises Active Directory environment using Windows Server 2022, Windows 10 Pro, and Oracle VirtualBox. The environment includes a domain controller, internal DNS, a domain joined workstation, centralized Group Policy, departmental file shares, role based permissions using the AGDLP model, Access-Based Enumeration, and automatic drive mapping. The lab was built to develop practical Windows Server administration skills and establish a foundation for a future hybrid environment. 

## Project Goals

- Gain practical experience with Windows Server and Active Directory Domain Services
- Practice common domain administration tasks
- Configure centralized user and computer policies
- Implement role based access to departmental file shares
- Apply the AGDLP permission model
- Automate department drive mappings through Group Policy
- Build an on-premises environment that can later be extended into a hybrid Microsoft lab

## Lab Architecture

### Host System
- Microsoft Surface Pro 6
- Oracle VirtualBox Hypervisor
### DC01
- Windows Server 2022
- Active Directory Domain Services
- Domain Controller
- DNS Server
- Global Catalog
- SMB File Server
- Static IPv4 address: 192.168.50.10
### CLIENT01
- Windows 10 Pro
- Domain joined workstation
- Static IPv4 address: 192.168.50.20
- DNS Server: 192.168.50.10
### Domain
- DNS domain: tracey.lab
- NetBIOS domain: TRACEYLAB
### Virtual Network
- VirtualBox NAT: LabNet-NAT
- Network: 192.168.50.0/24
- Gateway: 192.168.50.1

## Tools and Technologies

- Oracle VirtualBox
- Windows Server 2022
- Windows 10 Pro
- Active Directory Domain Services
- DNS
- Active Directory Users and Computers
- Group Policy Management
- PowerShell
- SMB File Sharing
- NTFS Permissions
- Access-Based Enumeration
- AGDLP Group Nesting

## Network and DNS Configuration 

DC01 was configured with a static IP address and used as the internal DNS server for the domain. CLIENT01 was configured to use DC01 for DNS so that it could locate the domain controller and access domain resources. 
DNS testing confirmed that DC01 could resolve both internal domain records and external domain names through configured DNS forwarders. 

<img width="405" height="455" alt="CLIENT01 Domain Joined" src="https://github.com/user-attachments/assets/4efd6bcf-2f7a-431d-b37a-563366564265" />

<img width="710" height="514" alt="DC01-Network_Config" src="https://github.com/user-attachments/assets/f38fe9fa-cc1c-4d5c-b356-5f01f07e8996" />

## Organizational Unit Design

Organizational units were created to separate users, computers, administrative accounts, groups, servers, and disabled objects. 
Departmental OUs included:
- Finance
- Human Resources
- Information Technology
- Operations
- General Staff

This structure allowed Group Policy and administrative tasks to be applied to the appropriate users and computers. 

<img width="247" height="517" alt="AD OU Structure" src="https://github.com/user-attachments/assets/92f9971d-77b7-405b-9eea-cdd887af14d0" />

## User, Group, and File Permission Design

More than 15 domain user accounts were created and organized by department, with job titles, department assignments, and manager relationships configured to simulate a small business environment. Role-based security groups were implemented using the AGDLP model. Global security groups represented user roles, while Domain Local groups represetned acceesss to specefic file resources. 
Accounts > Global Groups > Domain Local Groups > Permissions
Departmental SMB shares were created for Finance, Human Resources, Information Technology, Operations, and General Staff. NTFS permissions were assigned to the appropriate Domain Local groups, while Access-Based Enumeration prevented users from seeing folders they were unauthorized to access. Testing confirmed that users could create, modify, and delete files within authorized folders while restricted folders remained hidden and inaccessible. 

<img width="739" height="406" alt="AD-GroupNesting" src="https://github.com/user-attachments/assets/0bb17cf2-e061-4434-ad3b-d6045cb682a2" />

<img width="678" height="869" alt="Deparmtnet-NTFS-Permissions" src="https://github.com/user-attachments/assets/c8a57b5a-7ff1-4a8d-8867-6c0676754d0c" />

<img width="782" height="485" alt="GlobalSecurityGroups" src="https://github.com/user-attachments/assets/c9b988eb-0c00-4c56-98a4-219e50b58cc7" />

<img width="655" height="267" alt="SMB-AccessBased-Enumeration" src="https://github.com/user-attachments/assets/7827e3be-831e-41bd-9383-052ac23ccc23" />

## Group Policy Configuration

Group Policy Objects were created to centrally manage user and computer settings.
Configured policies included: 
- Computer security baseline
- User security baseline
- Interactive logon notice
- Inactivity timeout
- Password protected screen locking
- Automatic department drive mappings

The drive mapping policy used Group Policy Preferences and item level targeting. Security group membership determined which drives appeared for each user. 

<img width="785" height="533" alt="GPO Drive Mappings" src="https://github.com/user-attachments/assets/9647d885-2385-4057-acf3-78dac4b6c007" />

<img width="1347" height="570" alt="Client01-GPReport-Result" src="https://github.com/user-attachments/assets/ffa46553-98ca-4be9-a214-a8b75270b80f" />

## Testing and Validation

- Domain user authentication on CLIENT01
- Internal and external DNS resolution
- Domain controller discovery
- User and computer Group Policy application
- Authorized and unauthorized folder access
- Access-Based Enumeration
- Password resets
- Account disabling and re-enabling
- Group membership and permission changes
- SMB share and NTFS permission verification
- Final domain controller health checks

<img width="1115" height="231" alt="DomainController-Health" src="https://github.com/user-attachments/assets/f70efd88-7112-406c-9567-7708fa5e547d" />

## Problems Encountered and Resolutions

Problem: Hardware virtualization unavailable
Resolution: Verified and enabled virtualization support before creating the virtual machines

Problem: Duplicate or ghost network adapter
Resolution: Reviewed the active adapters and corrected the static network configuration

Problem: DNS forwarding initially appeared unsuccesful
Resolution: Verified internal DNS first, then tested external name resolution through DC01

Problem: Windows installation media issues
Resolution: Created the virtual machine instance first, and then uploaded the ISO file after the VM was created. 

Problem: Incorrect security group scope
Resolution: Identified a resource permission group that had been created with the wrong scope and corrected it to a Domain Local security group before applying NTFS permissions. 

## Project Limitations

Because the host system only had 8GB of RAM, DC01 also hosted the departmental file shares. In a production environment, file services would normally be on their own separate server, rather than sharing the domain controller. 

The environment also only used one domain controller. A production environment would normally have additional domain controllers to support redundancy, replication, and fault tolerance. 

This lab was isolated within VirtualBox and was not configured as an internet facing environment. 
