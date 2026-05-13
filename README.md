# IT Support Lab Series  


## Contact & Connect  
The best way to contact me is via [LinkedIn](https://www.linkedin.com/in/patrickbobbitt/). For technical inquiries regarding my labs, feel free to open an issue.

<p align="left">
  <a href="https://linkedin.com/in/patrickbobbitt"><img src="https://img.shields.io/badge/LinkedIn-Patrick%20Bobbitt-0072b1?style=for-the-badge&logo=linkedin&logoColor=white" /></a>&nbsp;<a href="mailto:pbobbitt176@gmail.com"><img src="https://img.shields.io/badge/Email-Contact%20Me-red?style=for-the-badge&logo=gmail&logoColor=white" /></a>
</p>

## Education & Certifications
<div>
</a> <img src="https://img.shields.io/badge/Education-WGU%20BS%20Cloud%20%26%20Network%20Engineering%20Student-00ADEE?style=for-the-badge&logo=google-scholar&logoColor=white" /> <a href="https://www.credly.com/badges/119032c2-bae6-45e2-a3ad-a97ca4ec8c70/public_url"><img src="https://img.shields.io/badge/Certification-CompTIA%20Network%2B-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a> <a href="https://www.credly.com/badges/e7bb1b0e-1245-4fab-8b98-c8c061e3ee33/public_url"><img src="https://img.shields.io/badge/Certification-CompTIA%20A%2B-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a> <img src="https://img.shields.io/badge/In%20Progress-CompTIA%20Security%2B-6c757d?style=for-the-badge&logo=comptia&logoColor=white" /> <a href="https://www.credly.com/badges/9c442bc0-ff46-42e8-9d56-0f50adf6d797/public_url"><img src="https://img.shields.io/badge/Certification-CompTIA%20IT%20Operations%20Specialist%20(CIOS)-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a> <a href="https://www.peoplecert.org/public-profile?ed=XCHu3ZqUTNJZsRD7ohFrrJDXq3BRolCm"> <img src="https://img.shields.io/badge/Certification-ITIL%C2%AE%204%20Foundation-6F42C1?style=for-the-badge&logoColor=white" /> </a> <img src="https://img.shields.io/badge/In%20Progress-LPI%20Linux%20Essentials-6c757d?style=for-the-badge&logo=linux&logoColor=white" />
</div>

## Lab Series Technical Stack  
<p align="left">
  <img src="https://img.shields.io/badge/Server-Windows%20Server%202025-0078D4?style=for-the-badge&logo=windowsserver&logoColor=white" />
  <img src="https://img.shields.io/badge/Client-Windows%2011-0078D4?style=for-the-badge&logo=windows11&logoColor=white" />
  <img src="https://img.shields.io/badge/Identity & Access Management-Active%20Directory-FF5733?style=for-the-badge&logo=microsoft-active-directory&logoColor=white" />
  <img src="https://img.shields.io/badge/Operations-Ticketing%20Lab-2ea44f?style=for-the-badge&logo=helpdesk&logoColor=white" />
  <img src="https://img.shields.io/badge/Hypervisor-VirtualBox-894ba9?style=for-the-badge&logo=virtualbox&logoColor=white" />
  <img src="https://img.shields.io/badge/Scripting-PowerShell-1E8449?style=for-the-badge&logo=powershell&logoColor=white" />
  <img src="https://img.shields.io/badge/Identity-Microsoft%20Entra%20ID-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white" />
  <img src="https://img.shields.io/badge/Cloud-Microsoft%20365-E33E2B?style=for-the-badge&logo=microsoft-365&logoColor=white" />
  <img src="https://img.shields.io/badge/MDM-Microsoft%20Intune-0078D4?style=for-the-badge&logo=microsoft&logoColor=white" />
</p>


## Project Overview
This repository contains a comprehensive, three-part technical lab series simulating a real-world enterprise IT environment. The project moves from raw infrastructure deployment to advanced Identity and Access Management (IAM), concluding with a hands-on Help Desk ticketing simulation.

**The Goal:** To build, secure, and manage a corporate network from the ground up, demonstrating proficiency in systems administration, network security, and technical support workflows.


## Core Tech Stack & Competencies
*   **Operating Systems:** Windows Server 2025 (Datacenter), Windows 11 Enterprise
*   **Directory Services:** Active Directory Domain Services (AD DS)
*   **Networking:** DNS, DHCP, Static IPv4 Addressing, NAT Networking
*   **Security & Policy:** Group Policy Objects (GPO), RBAC (Role-Based Access Control), Least Privilege, Account Lockout Policies
*   **Virtualization:** Oracle VirtualBox (Type-2 Hypervisor)
*   **IT Operations:** Disaster Recovery (Snapshots), Documentation, Troubleshooting
*   **Scripting:** PowerShell


## Project Structure

### [Part 1: Windows Server & Infrastructure Build](./part-1-infrastructure/)
**Focus: The Foundation.** 
*   Architected an isolated virtual network environment.
*   Deployed **Windows Server 2025** as a Primary Domain Controller.
*   Provisioned a Windows 11 managed endpoint.
*   **Key Outcome:** A fully functional, stable environment with verified internal/external connectivity and disaster recovery fail-safes.

<img src="screenshots/W11%20Has%20Joined%20Domain.png" alt="ADUC showing W11-CL01 in the Computers Container" width="49%">&nbsp;<img src="screenshots/W11-CL01%20VM%20Ping%20Test.png" alt="Successful Ping tests" width="49%">

### [Part 2: Identity & Access Management (Active Directory/GPO)](./part-2-active-directory/)
**Focus: Security & Governance.**
*   Designed a scalable **Organizational Unit (OU)** hierarchy.
*   Implemented **Role-Based Access Control (RBAC)** for HR, Finance, and IT departments.
*   Deployed **Group Policy Objects (GPOs)** to harden endpoints (restricting CMD/Control Panel) and enforce corporate compliance.
*   Automated **User Provisioning at Scale**: Built a PowerShell-driven onboarding process to create and assign 100 user accounts from a CSV file.
*   Validated **Security & System Integrity**: Conducted end-to-end testing (permissions, GPOs, resource limits), ensuring policies work as intended.
*   **Key Outcome:** A fully automated and policy-driven domain where user access, security controls, and resource provisioning are consistently enforced, reducing manual IT workload and significantly reducing the attack surface, and ensuring every employee is set up correctly from day one.

<img src="screenshots/Scaling%20PowerShell%20.png" alt="Users added with powershell" width="49%">&nbsp;<img src="screenshots/Scaled%20AD%20Users.png" alt=" All Users in AD " width="49%">&nbsp;<img src="screenshots/S%20Drive%20and%20Printer%20Accessible.png" alt="W11 File Explorer showing mapped S: Drive and Printer" width="49%">&nbsp;<img src="screenshots/GPOs.png" alt="Users In Active Directory" width="49%">

### [Part 3: Hybrid Cloud Integration & Endpoint Management (MDM)](./part-3-hybrid-cloud-integration/)
**Focus: Cloud Identity & Mobility.**
*   Established a **Hybrid Identity** infrastructure by deploying Microsoft Entra Connect Sync, bridging the on-premises Active Directory to a Microsoft 365 Enterprise environment.
*   Engineered **Single Sign-On (SSO)** capabilities by resolving non-routable `.local` domain constraints and implementing alternative UPN suffixes for over 100 users.
*   Configured **Hybrid Microsoft Entra Join** via GPO and enrolled client endpoints into **Microsoft Intune** for over-the-air Mobile Device Management (MDM).
*   Modernized policy enforcement by translating local Group Policies into **Intune Configuration Profiles**, pushing customized browser settings and security policies via the cloud.
*   Conducted advanced **troubleshooting and root cause analysis**, resolving critical host-machine storage failures (`VERR_DISK_FULL`), licensing attribute errors, and GPO conflicts during MDM enrollment.
*   **Key Outcome:** A fully synchronized, cloud-integrated environment that extends local infrastructure to the web. Users benefit from seamless SSO, while IT can securely provision licenses, enforce compliance, and push software to remote devices over the internet, enabling a secure "work-from-anywhere" infrastructure.

<img src="screenshots/Hybrid%20Users%20Synced.png" alt="Microsoft Entra admin center showing the list of synchronized users" width="49%">&nbsp;<img src="screenshots/Internet%20startup%20in%20action.gif" alt="Animated GIF showing the web browser automatically opening to the IT support page based on the cloud policy" width="49%">

### [Part 4: Help Desk Operations & Ticketing](./part-4-helpdesk-tickets/) *(In Progress)*
**Focus: The User Experience.**
*   Simulating real-world L1/L2 support scenarios.
*   Resolving common issues: Password resets, software deployment, and policy troubleshooting.
*   Utilizing ticketing workflows to document and track "Break/Fix" incidents.
*   **Key Outcome:** Demonstrating the ability to translate technical knowledge into professional end-user support.

## Key Technical Highlights

### Cloud Integration & Hybrid Identity
* **Hybrid Directory Synchronization:** Deployed **Microsoft Entra Connect Sync** to bridge the on-premises Windows Server 2025 environment with Microsoft 365, successfully synchronizing 100+ Active Directory users and security groups to the cloud.
* **Seamless Single Sign-On (SSO):** Resolved non-routable domain (`lab.local`) limitations by configuring alternative UPN suffixes (`@pbitsupport.onmicrosoft.com`) across all local accounts, establishing a unified login for local file shares, Entra ID, and M365 email.

### Modern Endpoint Management (MDM)
* **Intune Device Enrollment:** Configured **Hybrid Microsoft Entra Join** via Group Policy and Entra Connect, successfully enrolling Windows 11 client devices into Microsoft Intune for cloud-based Mobile Device Management.
* **Cloud Policy Deployment:** Transitioned local GPOs to Intune Configuration Profiles (Settings Catalog), deploying targeted web browser configurations based on synced Entra ID security groups (Finance vs. HR).
* **Enterprise License Management:** Managed M365 E5 Developer licenses within the Microsoft 365 Admin Center, strategically provisioning access and managing "Usage Location" attributes to maintain regional compliance.

### Enterprise-Scale Automation
* **Bulk User Provisioning:** Automated the creation and security group assignment of 100+ user accounts using a custom PowerShell script, reducing a multi-hour onboarding task to just minutes and eliminating manual errors.

### Security Hardening
* **Access Control:** Deployed automated security policies to enforce **Principle of Least Privilege (PoLP)**, ensuring that standard users cannot access system-level tools, while "IT Support" users maintain the access needed to perform their duties.

### Automated Resource Provisioning
* **Zero-Touch Setup:** Deployed Group Policies to automatically map departmental network drives (S:) and deploy shared printers, providing employees with instant access to essential tools upon login.

### Efficient Storage Management
* **Data Governance:** Implemented FSRM to enforce storage quotas and block unauthorized file types (e.g., audio/video), preventing waste and ensuring critical disk space remains available for business operations.

### Troubleshooting & Resilience
Throughout this lab series, I resolved critical conflicts, including:
* **Proactive Vulnerability Management:** Researched Server 2025 DirSync known issues prior to cloud migration, confirming KB5068861 was installed to prevent directory synchronization failures.
* **Identity & Routing Resolution:** Solved Entra Sync errors caused by a private local domain by bulk-mapping accounts to a public UPN suffix, ensuring cloud-authentication functionality.
* **Licensing & Compliance Errors:** Rectified an "Invalid Usage Location" error during M365 license assignment by updating regional compliance data for synced cloud profiles.
* **Policy Conflict Resolution:** Bypassed a local "Disable Settings" GPO that blocked MDM enrollment by utilizing an IT Support admin account, proving the effectiveness of previously established Least Privilege architectures.
* **Hypervisor Optimization:** Solved "Black Screen" boot errors by managing Hyper-V/Core Isolation conflicts, and resolved a critical VirtualBox `VERR_DISK_FULL` crash during a cumulative OS update by performing host-level storage remediation.
* **Permission Misconfiguration:** Identified and corrected inherited NTFS/share permission conflicts that unintentionally granted Finance access to all departments.
* **GPO & Print Deployment Failure:** Troubleshot a failed network printer deployment caused by incorrect GPO pathing and client security restrictions; rebuilt the printer using a compatible driver and corrected the FQDN to restore functionality.
* **Network Logic:** Rectified authentication errors caused by VM mismatches, proving a methodical approach to the OSI model.
  
### Documentation & Governance
Each phase of this project includes a detailed **Implementation Log**. I treat these logs as professional internal documentation, ensuring that every configuration change is auditable and repeatable, a vital skill in any enterprise IT team.

## Disclaimer & AI Disclosure
While 100% of the technical implementation and verification within this environment was conducted by the author, Generative AI was employed to assist in structuring the final report and ensuring professional terminology standards were met throughout the documentation.
