# Windows Server 2025 & Active Directory Deployment Lab

# Project Conclusion
This project outlines the foundational setup of a virtualized enterprise environment. Starting with bare-metal hardware, a complete, two-machine network was deployed, consisting of a Windows Server 2025 Domain Controller and a Windows 11 client workstation. The process involved meticulous hardware validation, virtual network configuration, operating system installation, and the critical integration of the client into the Active Directory domain. The result is a stable, cleanly configured baseline environment, secured with snapshots, ready for more advanced infrastructure development and testing.

## Milestone 1: Environment Preparation
**Focus:** Verifying hardware capabilities and establishing the virtual network backbone.

*   **Confirmed Host System Compatibility:** Ensured the physical machine met the necessary CPU, RAM, and storage requirements to run both virtual machines and the host operating system without performance issues.
*   **Acquired Core Software:** Downloaded all required components, including VirtualBox, the VirtualBox Extension Pack, Windows Server 2025, and Windows 11 Education ISOs.
*   **Constructed a Virtual Network:** Created an isolated VirtualBox network (`NatNetwork_Lab`) with a `192.168.0.0/24` IP range to allow the server and client to communicate.

> **Evidence:** See **Network Settings**
<img src="screenshots/NatNetwork_Lab.png" alt="A screenshot of the host computer's system information" width="70%">
<BR>

## Milestone 2: Server Deployment & Domain Creation
**Focus:** Building and promoting the primary server to a Domain Controller.

*   **Created the Server Virtual Machine:** Provisioned a new VM named `WS2025-DC01` with 4GB of RAM and 2 processors.
*   **Installed and Configured Windows Server:** Completed the installation of Windows Server 2025, set a static IP address (`192.168.0.10`), and renamed the machine.
*   **Deployed Active Directory:** Added the Active Directory Domain Services role and promoted the server to become the first domain controller in a new forest named `lab.local`.

> **Evidence:** See **Virtual Machine AD DS + DNS**
<img src="screenshots/WS2025-DC01%20AD%20DS.png" alt="Server Manager dashboard showing AD DS and DNS roles are installed" width="70%">
<BR>

## Milestone 3: Client Workstation Setup
**Focus:** Deploying a Windows 11 client machine prepared for domain integration.

*   **Created the Client Virtual Machine:** Provisioned a new VM named `W11-CL01` with specifications matching the server.
*   **Installed Windows 11 Education:** Completed the OS installation, specifically using the "Domain join instead" option to create a local account and avoid a mandatory Microsoft account.
*   **Configured Client Network Settings:** Set a static IP address (`192.168.0.100`) and pointed its DNS to the server's IP to ensure it could find the `lab.local` domain.

> **Evidence:** See **W11 Ping test**
<img src="screenshots/W11-CL01%20VM%20Ping%20Test.png" alt="A command prompt window showing a successful ping from the Windows 11 client to the server" width="70%">
<BR>

## Milestone 4: Domain Integration
**Focus:** Joining the client workstation to the Active Directory domain.

*   **Connected Client to Domain:** Used the System Properties (`sysdm.cpl`) utility on the `W11-CL01` client to officially join it to the `lab.local` domain.
*   **Verified Domain Membership:** Confirmed on the `WS2025-DC01` server that a new computer object for `W11-CL01` appeared in the "Computers" container within Active Directory Users and Computers.

> **Evidence:** See **W11-CL01 shows in ADUC on WS2025-DC01**
<img src="screenshots/W11%20Has%20Joined%20Domain.png" alt="Active Directory Users and Computers window showing the W11-CL01 computer object" width="70%">
<BR>

## Milestone 5: Environment Finalization & Stability
**Focus:** Creating a clean, revertible baseline for both machines to ensure a stable foundation for future work.

*   **Captured Server Snapshot:** Took a snapshot of the `WS2025-DC01` VM named `Base-ADDS-Configured` after Active Directory was fully installed and the server was stable.
*   **Captured Client Snapshot:** Took a snapshot of the `W11-CL01` VM named `Base-Domain-Joined` immediately after it was successfully connected to the domain.
*   **Resolved Initial Setup Hurdles:** Documented and fixed preliminary issues, such as Hyper-V conflicts that initially prevented the VMs from booting, ensuring a smooth operational state.

> **Evidence:** See **Final Snapshot Tree**
<img src="screenshots/Lab%20Snapshots%20Final.png" alt="The VirtualBox snapshot manager showing the final snapshot tree for the lab VMs" width="70%">
<BR>

## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| On first run of [VM](Images/networking%20missing.png) couldn't find "network" under `Files>Tools`   | VM [preferences](Images/Preferences%20set%20as%20basic.png) were set to basic | Changed VM [preference](Images/networking%20is%20now%20listed.png) to expert and "networks" appeared under `Files>Tools>network` |
| [VM Boot Failure / Black Screen](Images/VM%20Black.png) | Hyper-V / Core Isolation enabled on Host (Warning is Green Turtle icon). were set to basic | Disabled Hyper-V via [bcdedit](https://github.com/pbobbitt/Windows-Server-2025-Virtual-Infrastructure-Deployment/blob/main/Images/Disabled%20Hyper-V%20bootloader.png) and toggled off [Memory Integrity](Images/Disabled%20Memory%20Integrity.png) to allow VirtualBox native VT-x/AMD-V access. Confirmed [VirtualBox now runs](Images/VM%20Working.png) |

---
*End of Implementation Log*


