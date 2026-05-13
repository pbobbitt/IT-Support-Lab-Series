# Part 3: Microsoft 365 Hybrid Identity & Intune Endpoint Management


## Contact & Connect  
The best way to contact me is via [LinkedIn](https://www.linkedin.com/in/patrickbobbitt/). For technical inquiries regarding my labs, feel free to open an issue.

<p align="left">
  <a href="https://linkedin.com/in/patrickbobbitt"><img src="https://img.shields.io/badge/LinkedIn-Patrick%20Bobbitt-0072b1?style=for-the-badge&logo=linkedin&logoColor=white" /></a>&nbsp;<a href="mailto:pbobbitt176@gmail.com"><img src="https://img.shields.io/badge/Email-Contact%20Me-red?style=for-the-badge&logo=gmail&logoColor=white" /></a>
</p>

## Education & Certifications
<div>
</a> <img src="https://img.shields.io/badge/Education-WGU%20BS%20Cloud%20%26%20Network%20Engineering%20Student-00ADEE?style=for-the-badge&logo=google-scholar&logoColor=white" /> <a href="https://www.credly.com/badges/119032c2-bae6-45e2-a3ad-a97ca4ec8c70/public_url"><img src="https://img.shields.io/badge/Certification-CompTIA%20Network%2B-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a> <a href="https://www.credly.com/badges/e7bb1b0e-1245-4fab-8b98-c8c061e3ee33/public_url"><img src="https://img.shields.io/badge/Certification-CompTIA%20A%2B-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a> <img src="https://img.shields.io/badge/In%20Progress-CompTIA%20Security%2B-6c757d?style=for-the-badge&logo=comptia&logoColor=white" /> <a href="https://www.credly.com/badges/9c442bc0-ff46-42e8-9d56-0f50adf6d797/public_url"><img src="https://img.shields.io/badge/Certification-CompTIA%20IT%20Operations%20Specialist%20(CIOS)-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a> <a href="https://www.peoplecert.org/public-profile?ed=XCHu3ZqUTNJZsRD7ohFrrJDXq3BRolCm"> <img src="https://img.shields.io/badge/Certification-ITIL%C2%AE%204%20Foundation-6F42C1?style=for-the-badge&logoColor=white" /> </a> <img src="https://img.shields.io/badge/In%20Progress-LPI%20Linux%20Essentials-6c757d?style=for-the-badge&logo=linux&logoColor=white" />
</div>

**Lab Series Technical Stack**  
<p align="left">
  <img src="https://img.shields.io/badge/Server-Windows%20Server%202025-0078D4?style=for-the-badge&logo=windowsserver&logoColor=white" />
  <img src="https://img.shields.io/badge/Client-Windows%2011-0078D4?style=for-the-badge&logo=windows11&logoColor=white" />
  <img src="https://img.shields.io/badge/Identity-Microsoft%20Entra%20ID-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white" />
  <img src="https://img.shields.io/badge/Cloud-Microsoft%20365-E33E2B?style=for-the-badge&logo=microsoft-365&logoColor=white" />
  <img src="https://img.shields.io/badge/MDM-Microsoft%20Intune-0078D4?style=for-the-badge&logo=microsoft&logoColor=white" />
  <img src="https://img.shields.io/badge/Hypervisor-VirtualBox-894ba9?style=for-the-badge&logo=virtualbox&logoColor=white" />
</p>

# Project Overview
The primary objective of this phase was to seamlessly connect a local Windows Server 2025 network to Microsoft's cloud infrastructure. By establishing a "Hybrid Identity" environment, 100 local user accounts were successfully synchronized to Microsoft Entra ID, and a remote workstation was enrolled into Microsoft Intune for centralized, over-the-air device management.

## Tech Stack & Skills
*   **Systems:** Windows Server 2025, Windows 11, Microsoft 365 Admin Center, Microsoft Entra ID (formerly Azure AD), Microsoft Intune.
*   **Networking/Security:** Entra Connect Sync, Hybrid Entra Join, Mobile Device Management (MDM), Single Sign-On (SSO), Configuration Profiles.
*   **Core Skills:** Cloud Migration, Identity & Access Management (IAM), UPN Suffix Routing, Endpoint Device Setup, IT Troubleshooting.

## Key Accomplishments

###   **Hybrid Identity Deployment & Directory Synchronization:**
  * Integrated on-premises Active Directory with Microsoft Entra ID using the Entra Connect tool. Successfully migrated 100 users and 3 departmental security groups to the cloud, enabling employees to use a Single Sign-On (SSO) login for both local and cloud services.
###   **Enterprise Cloud Provisioning & Domain Routing:**
  * Provisioned a Microsoft 365 Enterprise environment and resolved non-routable private domain limitations (`lab.local`). Mapped all user accounts to a valid, public UPN suffix (`@pbitsupport.onmicrosoft.com`) to allow secure internet-based authentication.
###   **Zero-Touch Remote Device Management (MDM):**
  * Configured Microsoft Intune to manage company hardware over the internet. Deployed automated Configuration Profiles that instantly push corporate web settings and security baselines to specific departments (HR, Finance) upon user login.
###   **Advanced Infrastructure Troubleshooting:**
  * Diagnosed and resolved critical service interruptions, including host-level storage depletion (`VERR_DISK_FULL`), regional compliance blocks on software licenses (Usage Location Null errors), and local Group Policy (GPO) lockouts preventing cloud enrollment.

## Final Validation & Project Completion
**The hybrid cloud environment is fully operational, proving the ability to securely sync local network accounts to Microsoft Entra ID and automatically push software configurations to remote employee devices using Intune.**

> **Full Technical Deep Dive** 
> For the specific CLI commands, granular configuration steps, and a detailed implementation log, please see: **[Implementation Log (Detailed Version)](https://github.com/pbobbitt/IT-Support-Lab-Series/edit/main/part-3-hybrid-cloud-integration/ImplementationLog.md)**

## Visual Proof

### Cloud Identity Migration & User Sync
*   **Action:** Synchronized 100 local Active Directory users to the Microsoft cloud.
*   **Context:** Ensuring all existing employees can use a single, secure set of credentials to access cloud applications like Outlook, Teams, and SharePoint without needing duplicate accounts.
*   **Validation:** Microsoft Entra Admin Center confirms the successful population of the local users and their assigned departments.
<img src="Screenshots/Hybrid%20Users%20Synced.png" alt="Microsoft Entra admin center showing the list of synchronized users" width="70%">

### Remote Device Management (Intune)
*   **Action:** Enrolled a workstation into Microsoft Intune and applied a targeted Configuration Profile.
*   **Context:** Automating the setup of employee devices so they securely receive company apps and standard configurations without an IT technician needing to physically touch the machine.
*   **Validation:** Verified the remote rule instantly forced the workstation's web browsers to automatically open the internal IT Support page upon launch.
<img src="Screenshots/Internet%20startup%20in%20action.gif" alt="Animated GIF showing the web browser automatically opening to the IT support page based on the cloud policy" width="70%">

## Professional Key Takeaways
*   **Modern Cloud Administration:** I learned how to successfully bridge the gap between traditional on-site servers and modern cloud services, demonstrating the exact skills needed to manage a remote or hybrid workforce.
*   **Proactive Device Management:** By utilizing Microsoft Intune to push policies based on department groups, I demonstrated the ability to secure and configure company assets remotely, drastically reducing IT helpdesk tickets for manual software setups.
*   **Analytical Problem Solving:** I successfully navigated strict Microsoft licensing constraints and complex routing issues (UPN suffixes) by diagnosing the root causes and applying enterprise-standard administrative fixes.

## Disclaimer & AI Disclosure
While 100% of the technical implementation and verification within this environment was conducted by the author, Generative AI was employed to assist in structuring the final report and ensuring professional terminology standards were met throughout the documentation.
