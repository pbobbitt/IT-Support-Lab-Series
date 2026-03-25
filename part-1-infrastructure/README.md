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
| DC01 (Windows Server 2025) | Domain Controller (AD DS, DNS) | 192.168.0.10 |
| CL01 (Windows 11) | Domain-Joined Client | 192.168.0.100 |
| Network | VirtualBox NAT Network | 192.168.0.0/24 |

📸 **VM Overview / Environment Setup**  
[View Screenshot](#)



## What I Learned
* How Active Directory environments are structured and managed
* The importance of DNS in domain functionality
* How to configure and troubleshoot domain join issues
* How virtualization impacts networking and system performance
* How to diagnose low-level system conflicts (e.g., Hyper-V vs VirtualBox)


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

##Proof of Work

* Domain controller configured with AD DS + DNS
* Client machine successfully joined the domain
* Device visible in Active Directory Users and Computers
* Successful network communication between machines

(Screenshots available in repository)
