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
- Windows Surface Pro 6
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

DC01 was configured with a static IP address and used as the internal DNS server for the domain. CLIEN01 was configured to use DC01 for DNS so that it could locate the domain controller and access domain resources. 
DNS testing confirmed that DC01 could resolve both internal domain records and external domain names through configured DNS forwarders. 

## Organizational Unit Design

Organizational units were created to separate users, computers, administrative accounts, groups, servers, and disabled objects. 
Departmental OUs included:
- Finance
- Human Resources
- Information Technology
- Operations
- General Staff

This structure allowed Group Policy and administrative tasks to be applied to the appropriate users and computers. 

## Group Policy Configuration

Group Policy Objects were cereted to centrally manage user and computer settings.
Configured policies included: 
- Computer security baseline
- User security baseline
- Interactive logon notice
- Inactivity timeout
- Password protected screen locking
- Automatic department drive mappings

The drive mapping policy used Group Policy Preferences and item level targeting. Security group membership determined which drives appeared for each user. 

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


## Problems Encountered and Resolutions

Problem: Hardware virtualization unavailable
Resolution: Verified and enabled virtualization support before creating the virtual machines

Problem: Duplicate or ghost network adapter
Resolution: Reviewed the active adapters and corrected the static network configuration

Problem: DNS forwarding unsuccessful
Resolution: Verified internal DNS first, then tested eternal name resolution through DC01

Problem: Windows installation media issues
Resolution: Created the virtual machine instance first, and then uploaded the ISO file after the VM was created. 

## Project Limitations

Because the host system only had 8GB of RAM, DC01 also hosted the departmental file shares. In a production environment, file services would normally be on their own separate server, rather than sharing the domain controller. 

The environment also only used one domain controller. A production environment would normally have additionally domain controllers to support redundancy, replication, and fault tolerance. 

This lab was isolated within VirtualBox and was not configured as an internet facing environment. 
