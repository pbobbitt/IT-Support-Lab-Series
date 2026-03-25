# Technical Implementation Log

This document provides a detailed, step-by-step technical record of the project phases. It is intended for technical review, auditing, and reproducibility.

---

## Phase 0: System Requirements Check

The goal is to run Windows Server 2025 and Windows 11 virtual machines. Hardware compatibility was verified before deployment.

**Reference Requirements:**
- [Windows Server 2025](https://learn.microsoft.com/en-us/windows-server/get-started/hardware-requirements?tabs=storage&pivots=windows-server-2025)  
- [Windows 11](https://www.microsoft.com/en-us/windows/windows-11-specifications?r=1)

| Component | Windows Server 2025 | Windows 11 (VM) | Windows 11 (Host) | Total Needed |
|----------|--------------------|-----------------|-------------------|-------------|
| CPU | 64-bit, 2 processors | 64-bit, 2 processors | 64-bit, 2 processors | 6 processors |
| RAM | 4 GB | 4 GB | 4 GB | 12 GB |
| Storage | 32 GB | 64 GB | 64 GB | 160 GB |

System verification using `msinfo32` confirmed:
- 6 cores (12 logical processors)
- 32 GB RAM
- 224 GB available storage

**Evidence:**  
[System Info](Images/System%20info.png)  
[C: Storage Space](Images/C:%20Storage%20Space.png)

---

## Phase 1: Download Systems

| Tool / OS | Version | Purpose |
|----------|--------|--------|
| [Oracle VirtualBox](https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html) | 7.x | Hypervisor for VM management |
| [VB Extension Pack](https://www.virtualbox.org/wiki/Downloads) | 7.x | Enables RDP, encryption, NVMe support |
| Windows Server 2025 | Datacenter | Domain Controller |
| Windows 11 Education | 25H2 | Client workstation |

---

## Phase 2: Virtual Network Configuration

- Created NAT network: `NatNetwork_Lab`  
- Configured IP range: `192.168.0.0/24`  
- Enabled DHCP  

**Evidence:**  
[Network Settings](Images/NatNetwork_Lab.png)

---

## Phase 3: Virtual Machine Creation (Domain Controller)

- VM Name: `WS2025-DC01`  
- Resources:
  - 4 GB RAM  
  - 2 CPUs  
  - 80 GB storage (dynamic)  
- Mounted Windows Server 2025 ISO  
- Connected to `NatNetwork_Lab`

**Evidence:**  
[VM Settings](Images/WS2025-DC01%20VM%20Settings.png)

---

## Phase 4: Windows Server Installation

- Completed OS installation  
- Configured admin account ("Work or school")  
- Verified connectivity using:

`ping 8.8.8.8`
**Evidence:**  
[Ping Test](#)

---

## Phase 5: Basic Server Configuration

- Installed Guest Additions  
- Configured static IPv4 address  
- Disabled IPv6  
- Renamed system to `WS2025-DC01`  

**Evidence:**  
[Server Settings](#)  
[ipconfig Output](#)

---

## Phase 6: Active Directory Setup

- Installed AD DS role  
- Promoted server to Domain Controller  
- Created forest: `lab.local`  
- Set DSRM password  
- Restarted system  

**Evidence:**  
[AD DS + DNS Config](#)

---

## Phase 7: Windows 11 Client Setup

### VM Creation

- VM Name: `W11-CL01`  
- Resources:
  - 4 GB RAM  
  - 2 CPUs  
  - 80 GB storage  
- Connected to `NatNetwork_Lab`  

**Evidence:**  
[VM Settings](#)

---

### OS Configuration

- Installed Windows 11 Education  
- Created local account: `LabAdmin`  
- Disabled unnecessary privacy settings  
- Verified connectivity:
  - `ping 8.8.8.8`  
  - `ping 192.168.0.10`  
- Renamed system to `W11-CL01`  

**Evidence:**  
[Ping Test](#)

---

### Final Network Configuration

- Set static IP: `192.168.0.100`  

---

## Phase 8: Domain Join

### Domain Join Process

- Opened `sysdm.cpl`  
- Joined domain: `lab.local`  
- Authenticated with `LAB\Administrator`  

### Verification

Confirmed device appears in:
- Active Directory Users and Computers  
- `lab.local > Computers`  

**Evidence:**  
[Domain Join Verification](#)

---

## Phase 9: Snapshot Configuration

Snapshots created for recovery and reproducibility:

| Milestone | Snapshot Name | Description |
|----------|-------------|------------|
| Infrastructure Base | `Base-ADDS-Configured` | AD DS + DNS configured |
| Client Integration | `Base-Domain-Joined` | Client joined to domain |

**Evidence:**  
[Snapshot Tree](#)

---

## Troubleshooting Log

| Issue | Root Cause | Resolution |
|------|-----------|-----------|
| Network settings missing | Preferences set to Basic mode | Switched to Expert mode |
| VM boot failure (black screen) | Hyper-V / Core Isolation enabled | Disabled Hyper-V and Memory Integrity |

**Evidence:**  
[Network Issue](#)  
[Preferences Fix](#)  
[Boot Error](#)  
[Fix Applied](#)  
[Working VM](#)

---

*End of Implementation Log*
