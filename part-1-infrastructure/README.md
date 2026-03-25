# Part 1: Infrastructure Setup

## Objective
Build and configure a Windows domain environment to simulate real-world IT support tasks, including domain administration, network configuration, and client integration.

## Environment
- Windows Server 2025 (Domain Controller)
- Windows 11 Education (Client)
- Oracle VirtualBox
- Virtual Network (NAT Network: 192.168.0.0/24)

## Key Tasks
- **Hardware & Resource Planning**
  - Performed a system audit using `msinfo32` to ensure hardware could support multiple virtual machines, allocating 8 GB RAM and 4 CPU cores to the project.
- **Virtual Network Configuration**
  - Created a dedicated isolated network (`NatNetwork_Lab`) with DHCP enabled to allow secure communication between the domain controller and the client.
- **Domain Controller Deployment (Active Directory)**
  - Installed Windows Server 2025 and promoted it to a Domain Controller for the `lab.local` forest, establishing the foundation for centralized identity management.
- **Network Services Setup (DNS & IPv4)**
  - Configured static IPv4 addressing and DNS settings to ensure the client machine could reliably locate and communicate with the server.
- **Client Integration & Domain Join**
  - Provisioned a Windows 11 workstation and successfully joined it to the `lab.local` domain, verifying the connection through Active Directory Users and Computers (ADUC).
- **Proactive Troubleshooting & Optimization**
  - Resolved virtualization conflicts (Hyper-V interference) and implemented a Snapshot strategy to ensure environment stability and quick recovery.



## Outcome
Successfully deployed a functional Windows domain environment supporting centralized authentication, device management, and network services, replicating a real-world enterprise IT infrastructure.

## Key Takeaways
- **Centralized Administration**
  - Learned how to create virtual machine instances and set up an Active Directory server, a critical skill for L1 support.
- **Networking Foundations**
  - Gained hands-on experience with **IPv4 and DNS**, ensuring seamless connectivity between enterprise devices.
- **Critical Problem Solving**
  - Successfully diagnosed and fixed system-level errors (Hyper-V/Core Isolation) to ensure software compatibility and performance with the host device.
- **Disaster Recovery Basics**
  - Utilized **Snapshots** to create "restore points," demonstrating an understanding of system backups and minimizing downtime.
- **End-User Support Readiness**
  - Developed practical skills aligned with L1 IT support tasks, including system setup, issue resolution, and environment validation.
 
## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| On first run of [VM](screenshots/networking%20missing.png) couldn't find "network" under `Files>Tools`   | VM [preferences](screenshots/Preferences%20set%20as%20basic.png) were set to basic | Changed VM [preference](screenshots/networking%20is%20now%20listed.png) to expert and "networks" appeared under `Files>Tools>network` |
| [VM Boot Failure / Black Screen](screenshots/VM%20Black.png) | Hyper-V / Core Isolation enabled on Host (Warning is Green Turtle icon)| Disabled Hyper-V via [bcdedit](screenshots/Disabled%20Hyper-V%20bootloader.png) and toggled off [Memory Integrity](screenshots/Disabled%20Memory%20Integrity.png) to allow VirtualBox native VT-x/AMD-V access. Confirmed [VirtualBox now runs](screenshots/VM%20Working.png) |


## Screenshots

### Host System Verification
- Verified system resources using `msinfo32`
- Confirmed host meets requirements for running multiple VMs
- Validated sufficient CPU, RAM, and storage for lab environment  

<img src="screenshots/System%20info.png" alt="Host System Specs" width="70%">


### Virtual Network Configuration
- Created isolated network `NatNetwork_Lab` in VirtualBox
- Configured subnet `192.168.0.0/24` with DHCP enabled
- Verified network availability for VM communication  

<img src="screenshots/NatNetwork_Lab.png" alt="NatNetwork_Lab settings" width="70%">


### Domain Controller Setup (AD DS + DNS)
- Installed and configured Active Directory Domain Services on `WS2025-DC01`
- Promoted server to Domain Controller for `lab.local`
- Verified DNS and domain services functioning correctly  

<img src="screenshots/WS2025-DC01%20AD%20DS.png" width="70%">
<img src="screenshots/WS2025-DC01%20IPV4%20Settings.png" width="70%">


### Client Domain Join
- Joined `W11-CL01` to `lab.local` domain
- Authenticated using domain credentials
- Verified computer object appears in Active Directory (ADUC)  

<img src="screenshots/W11%20Has%20Joined%20Domain.png" width="70%">


### Snapshot & Recovery Setup
- Created VM snapshots after successful configuration
- Established restore points for domain controller and client
- Verified ability to revert environment to stable state  

<img src="screenshots/Lab%20Snapshots%20Final.png" width="70%">


## Disclaimer & AI Disclosure
While the **technical implementation** of this lab was performed entirely by the author, **Generative AI** was used as a collaborative tool to assist with structured formatting, professional terminology refinement, and the documentation of this report. 

This approach was taken to ensure the lab's technical findings are communicated with the clarity and professional standards required in a production IT environment.
