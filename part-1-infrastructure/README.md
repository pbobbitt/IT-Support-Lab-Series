# Part 1: Infrastructure Setup (Windows Server 2025)

## Overview

In this lab, I built the foundational infrastructure for a simulated enterprise IT environment using Windows Server 2025 and virtualization.

This includes:
- A domain controller configured with Active Directory and DNS  
- A Windows 11 client machine joined to the domain  
- Basic network configuration to enable communication between systems  

This environment will be used in later labs to simulate real-world IT administration and help desk scenarios.



## Skills Demonstrated

* Active Directory Administration
  * Installed and configured Active Directory Domain Services (AD DS)  
  * Created a new domain (`lab.local`)
  *  Verified domain objects using Active Directory Users and Computers (ADUC)  
* Domain Management
  * Joined Windows 11 client to domain
  * Authenticated using domain credentials
  * Verified domain connectivity and object creation  
* Networking Fundamentals
  * Configured static IP addressing
  * Set up DNS for domain resolution
  * Tested connectivity using `ping`
* Virtualization
  * Created and configured multiple virtual machines
  * Allocated system resources (CPU, RAM, storage)
  * Managed virtual networking using NAT network  
* Troubleshooting
  * Resolved VM boot issues caused by Hyper-V conflicts
  *  Diagnosed and fixed network visibility issues
  *  Verified system functionality through testing  


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

- Disabled Memory Integrity in Windows Security  

**System Settings Adjustment**  
[View Screenshot](#)

**Result**  
Virtual machines booted and operated normally  



## Proof of Work

- Domain controller configured with AD DS + DNS  
- Client successfully joined to domain  
- Device visible in Active Directory Users and Computers  
- Verified network communication between systems  

**ADUC Final View**  
[View Screenshot](#)

**Client Logged in with Domain Account**  
[View Screenshot](#)



## Deep Dive / Full Technical Log (for reference)

This document provides a granular, step-by-step technical record of the project phases.

[View Detailed Implementation Log (Phase 0-8)](./ImplementationLog.md)



## Next Step

This environment will be used to simulate administrative tasks in Active Directory.

Continue to: **Part 2 – Active Directory Administration**
