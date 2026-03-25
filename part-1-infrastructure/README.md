# Part 1: Infrastructure Setup (Windows Server 2025)

## Overview

In this lab, I built the foundational infrastructure for a simulated enterprise IT environment using Windows Server 2025 and virtualization.

This includes:
- A domain controller configured with Active Directory and DNS  
- A Windows 11 client machine joined to the domain  
- Basic network configuration to enable communication between systems  

This environment will be used in later labs to simulate real-world IT administration and help desk scenarios.



## Skills Demonstrated

- Active Directory Domain Services (AD DS) installation and configuration  
- Domain controller promotion and forest creation (`lab.local`)  
- Domain join process for client machines  
- Static IP configuration and DNS setup  
- Virtual machine provisioning and resource allocation  
- Network configuration using VirtualBox NAT network  
- Troubleshooting system and virtualization issues  



## Lab Architecture

| Component | Role | IP Address |
| - | - | - |
| WS2025-DC01 | Domain Controller (AD DS, DNS) | 192.168.0.10 |
| W11-CL01 | Domain-Joined Client | 192.168.0.100 |
| Network | VirtualBox NAT Network | 192.168.0.0/24 |

📸 **VM Overview / Environment Setup**  
[View Screenshot](#)



## Key Configuration Steps

### 1. Virtual Environment Setup
- Installed VirtualBox and Extension Pack  
- Created NAT Network (`192.168.0.0/24`)  
- Enabled DHCP for initial configuration  

**Virtual Network Configuration**  
[View Screenshot](#)



### 2. Domain Controller Setup (WS2025-DC01)
- Created Windows Server 2025 virtual machine  
- Allocated resources:
  - 4 GB RAM
  - 2 CPUs
  - 80 GB storage  
- Installed OS and verified internet connectivity  

**VM Configuration Settings**  
[View Screenshot](#)

**Server Installation Complete**  
[View Screenshot](#)



### 3. Network Configuration
- Assigned static IP address: `192.168.0.10`  
- Configured DNS settings  
- Verified connectivity using `ping`  

**IP Configuration (Server)**  
[View Screenshot](#)

**Network Connectivity Test**  
[View Screenshot](#)



### 4. Active Directory Setup
- Installed Active Directory Domain Services (AD DS)  
- Promoted server to Domain Controller  
- Created new forest: `lab.local`  
- Configured Directory Services Restore Mode (DSRM)  

**AD DS Role Installation**  
[View Screenshot](#)

**Domain Controller Promotion**  
[View Screenshot](#)

**Active Directory Domain (lab.local)**  
[View Screenshot](#)



### 5. Client Machine Setup (W11-CL01)
- Created Windows 11 virtual machine  
- Assigned static IP: `192.168.0.100`  
- Configured DNS to point to domain controller  

**Windows 11 Setup**  
[View Screenshot](#)

**Client Network Configuration**  
[View Screenshot](#)



### 6. Domain Join
- Joined client machine to `lab.local` domain  
- Authenticated using domain administrator credentials  
- Verified system appears in Active Directory  

**Domain Join Process**  
[View Screenshot](#)

**Successful Domain Join Confirmation**  
[View Screenshot](#)

**Computer Object in ADUC**  
[View Screenshot](#)



### 7. Snapshot Creation
- Created snapshots for stable recovery points:
  - Base AD DS configuration  
  - Domain-joined client state  

**Snapshot Configuration**  
[View Screenshot](#)



## Troubleshooting

### Issue: Virtual Machine Boot Failure (Black Screen)

**Error State**  
[View Screenshot](#)

**Cause:**  
Hyper-V and Windows Core Isolation conflicted with VirtualBox

**Resolution:**
- Disabled Hyper-V:
  ```bash
  bcdedit /set hypervisorlaunchtype off
