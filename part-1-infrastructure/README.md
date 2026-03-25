# Part 1: Infrastructure Setup

## Objective
Establish a centrally managed Windows domain environment to simulate real-world corporate IT operations and security protocols.

## Environment
- **Windows Server 2025** (Domain Controller)
- **Windows 11 Education** (Client Workstation)
- **Oracle VirtualBox** (Type-2 Hypervisor)

## Key Tasks
- **Infrastructure Build:**
  - Provisioned virtual hardware for server and client environments.
- **Network Configuration:**
  - Set up a private virtual network (`192.168.0.0/24`) for secure VM communication.
- **Active Directory Setup:**
  - Installed **AD DS** and promoted the server to a **Domain Controller** (`lab.local`).
- **DNS Configuration:**
  - Configured DNS and static IPv4 addressing to ensure reliable name resolution.
- **System Integration:**
  - Successfully joined the Windows 11 workstation (**W11-CL01**) to the domain.
- **Validation:**
  - Verified the computer object and connectivity within **Active Directory Users and Computers (ADUC)**.
- **Recovery Planning:**
  - Created system snapshots to ensure environment stability and rapid rollback capability.

## Outcome
Successfully deployed a functional Active Directory environment capable of **centralized authentication**, user management, and policy enforcement mirroring a professional enterprise IT setup.

## Screenshots
- **Network & IP Config:** `NatNetwork_Lab.png`, `IPV4 Settings.png`
- **Server Roles:** `VM AD DS.png`
- **Domain Verification:** `W11 Has Joined Domain.png`
- **System Snapshots:** `Lab Snapshots Final.png`

## Key Takeaways (Skills Demonstrated)
- **Active Directory Administration:**
  - Understanding domain architecture and centralized management.
- **Network Infrastructure:**
  - Implementing **DNS** and static addressing in a virtualized environment.
- **System Troubleshooting:**
  - Resolving hardware virtualization conflicts (Hyper-V/Core Isolation) to ensure peak performance.
- **Disaster Recovery:**
  - Utilizing snapshots for configuration baselining and risk mitigation.
