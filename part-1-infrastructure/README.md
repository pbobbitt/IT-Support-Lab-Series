# Part 1: Windows Server 2025 & Active Directory Infrastructure


**Professional & Educational Credentials**  
<p align="left">
  <a href="https://linkedin.com/in/patrick-bobbitt"><img src="https://img.shields.io/badge/LinkedIn-Patrick%20Bobbitt-0072b1?style=for-the-badge&logo=linkedin&logoColor=white" /></a> <img src="https://img.shields.io/badge/Education-WGU%20BS%20Cloud%20%26%20Network%20Engineering%20Student-00ADEE?style=for-the-badge&logo=google-scholar&logoColor=white" /> <a href="https://github.com/pbobbitt/pbobbitt/blob/main/CompTIA%20A%2B%20ce%20certificate.pdf"><img src="https://img.shields.io/badge/Certification-CompTIA%20A%2B-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a>&nbsp;<a href="mailto:pbobbitt176@gmail.com"><img src="https://img.shields.io/badge/Email-Contact%20Me-red?style=for-the-badge&logo=gmail&logoColor=white" /></a>
</p>

**Lab Series Technical Stack**  
<p align="left">
  <img src="https://img.shields.io/badge/Server-Windows%20Server%202025-0078D4?style=for-the-badge&logo=windowsserver&logoColor=white" />
  <img src="https://img.shields.io/badge/Client-Windows%2011-0078D4?style=for-the-badge&logo=windows11&logoColor=white" />
  <img src="https://img.shields.io/badge/Identity & Access Management-Active%20Directory-FF5733?style=for-the-badge&logo=microsoft-active-directory&logoColor=white" />
  <img src="https://img.shields.io/badge/Operations-Ticketing%20Lab-2ea44f?style=for-the-badge&logo=helpdesk&logoColor=white" />
  <img src="https://img.shields.io/badge/Hypervisor-VirtualBox-894ba9?style=for-the-badge&logo=virtualbox&logoColor=white" />
  <img src="https://img.shields.io/badge/Scripting-PowerShell-1E8449?style=for-the-badge&logo=powershell&logoColor=white" />
</p>

# Project Overview
The primary objective of this phase was to establish a scalable, virtualized Windows Server 2025 Active Directory environment and successfully integrate a Windows 11 Education client workstation. By leveraging Oracle VirtualBox and a custom NAT Network, the project successfully created an isolated sandbox that mimics an enterprise infrastructure.

## Tech Stack & Skills
*   **Systems:** Windows Server 2025 (Datacenter Edition), Windows 11, Oracle VirtualBox 7.x (Hypervisor)
*   **Networking & Security:** DNS (Domain Name System), DHCP, Static IP Addressing, NAT Networking, Forest/Domain Architecture
*   **Core Skills:** Active Directory Users & Computers (ADUC), Identity & Access Management (IAM), Disaster Recovery (Snapshots), System Optimization & Hardening

## Key Accomplishments

###  Centralized Identity Management & AD DS Deployment
* Deployed a Windows Server 2025 Domain Controller to establish the `lab.local` forest. This creates a single "source of truth" for identity and access management (IAM), enabling centralized control over user accounts and network-wide permissions.

###  Professional Domain Integration & Endpoint Management
* Successfully transitioned a Windows 11 Education workstation from a standalone state to a managed domain asset. This confirms that the server correctly handles authentication, DNS registration, and the application of corporate security policies.

###  Advanced Virtualization Troubleshooting (Firmware & OS Level)
* Resolved complex hardware-assisted virtualization conflicts by disabling Hyper-V and Memory Integrity (Core Isolation). This ensured VirtualBox had direct VT-x/AMD-V access, preventing system instability and "Black Screen" boot failures.

###  Isolated Infrastructure & Network Schema Design
* Engineered a custom NAT Network with a structured IPv4 addressing scheme. By implementing static IP assignments and internal DNS resolution, I ensured the server maintains a permanent, reachable "address" for all client workstations.

###  Disaster Recovery & Environment Resiliency
* Established a "Point-of-No-Return" recovery strategy using System Snapshots for all infrastructure nodes. This ensures the environment can be reverted to a clean, domain-joined state in seconds, protecting against configuration errors or botched updates.

## Final Validation & Project Completion
**The enterprise environment is fully operational, with a verified secure link between the Windows Server 2025 Domain Controller and the Windows 11 workstation, confirming that centralized management and DNS services are fully functional.**

> **Full Technical Deep Dive**
> For the specific CLI commands, granular configuration steps, and a detailed implementation log, please see: **[Implementation Log (Detailed Version)]([InsertLinkHere.md](https://github.com/pbobbitt/IT-Support-Lab-Series/blob/main/part-1-infrastructure/ImplementationLog.md))**

## Visual Proof

### Domain Integration & Centralized Management
*   **Action:** Joined the Windows 11 workstation to the `lab.local` domain.
*   **Context:** Bringing a new employee device under company control so it can receive security updates and policies.
*   **Validation:** Verified the workstation (`W11-CL01`) appears correctly within the **Active Directory Users and Computers (ADUC)** management console on the server.

<img src="screenshots/W11%20Has%20Joined%20Domain.png" alt="ADUC showing W11-CL01 in the Computers Container" width="70%">  

### End-to-End Connectivity
*   **Action:** Performed internal and external Ping tests.
*   **Context:** Ensuring the workstation can reach both the internal server for files and the external internet for updates.
*   **Validation:** Confirmed 0% packet loss to both the Domain Controller (`192.168.0.10`) and external DNS (`8.8.8.8`).
  
<img src="screenshots/W11-CL01%20VM%20Ping%20Test.png" alt="Successful Ping tests" width="70%">

## Professional Key Takeaways

###  **Systematic Approach:**
* I learned to build an IT environment methodically, starting with hardware requirements and network configuration before moving to server roles and client integration. This prevents errors and ensures a stable foundation.
  
###  **Security-First Mindset:**  
* By creating a Domain Controller, I implemented a core security principle: centralized control. Managing users from one place is fundamentally more secure and efficient than managing accounts on individual machines.  

###  **Effective Troubleshooting:**
* I demonstrated the ability to diagnose and resolve technical roadblocks, such as virtualization software conflicts (Hyper-V vs. VirtualBox), which is a critical skill for maintaining system uptime.

## Contact & Connect  
How to reach me:  
The best way to contact me is via [LinkedIn](https://www.linkedin.com/in/patrickbobbitt/). For technical inquiries regarding my labs, feel free to open an issue.

<p align="left">
  <a href="https://linkedin.com/in/patrick-bobbitt"><img src="https://img.shields.io/badge/LinkedIn-Patrick%20Bobbitt-0072b1?style=for-the-badge&logo=linkedin&logoColor=white" /></a>&nbsp;<a href="mailto:pbobbitt176@gmail.com"><img src="https://img.shields.io/badge/Email-Contact%20Me-red?style=for-the-badge&logo=gmail&logoColor=white" /></a>
</p>

## Disclaimer & AI Disclosure
While 100% of the technical implementation and verification within this environment was conducted by the author, Generative AI was employed to assist in structuring the final report and ensuring professional terminology standards were met throughout the documentation.
