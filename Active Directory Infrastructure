## Project Overview
  Build an Active Directory environment using Windows Server 2022 and VirtualBox. Include a domain controller, Windows 10 client, DNS, Group Policy, departmental file shares, AGDLP permissions, and automatic drive mapping. 

## Project Goals
  * Gain Practical Windows Server and Active Directroy experinece
  * Practice domain adminstration
  * Implement role based file permissions
  * Establish the foundation for a future hybrid Microsoft environment

## Lab Architecture
  Host: Microsoft Surface Laptop
  Hypervisor: Oracle VirtualBox

  DC01: 
  - Windows Server 2022
  - Domain Controller
  - DNS Server
  - File Server
  - IP: 192.168.50.10

CLIENT01:
  - Windows 10 Pro
  - Domain joined workstation
  - IP: 192.168.50.10

Domain: tracey.lab
VirtualBox Network:  
  - LabNet-NAT
  - 192.168.50.0/24
  - Gateway: 192.168.50.1

## Tools and Technologies
  * Oracle VirtualBox
  * Windows Server 2022
  * Windows 10 Pro
  * Active Directroy Domain Services
  * DNS
  * Group Policy Management
  * PowerShell
  * SMB file sharing
  * NTFS permissions
  * AGDLP

## Active Directory Deployment
  * Forest and domain created as tracey.lab
  * NetBIOS name: TRACEYLAB
  * DC01 is the domain controller
  * DNS and Global Catalog enabled
  * CLIENT01 is joined to the domain

## User and Group Management
  * 15+ users
  * Departmnet assignments
  * Job titles
  * Managers and direct reports
  * Global role groups beginning with GG
  * Domain Local permissions groups beginning with DL

## Group Policy Configuration
  * Computer security basleine
  * User security baseline 
  * Interactive logon notice
  * Inactivity and screen lock 
  * Department drive mappings 
  * Item level targeting using security groups 

## Testing and Validation
  * Domain user login
  * DNS resolution
  * Group Policy applicaiton
  * Authorized and unauthroized file access
  * Account disabling and password resets
  * Group membership changes 

## Problems Encountered and Resolutions
  * Virtualization initally disabeld 
  * VirtualBox ISO donwload problems 
  * Duplicate or ghost network adapters 
  * DNS forwarder connectivity confusion
  * Incorrect group scope
  * PowerShell syntax errors 
  * Drive mappings requireiring group policy update and re sign in

## Project Limitations
  The main liitation was hosting the file services on DC01 becuase the Surface I was using to host the lab only has 8GB of RAM. In a real production envionment, the file server would normally be sepreate from the domain controller. 
