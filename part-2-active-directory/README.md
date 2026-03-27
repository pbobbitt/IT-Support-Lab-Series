# Identity & Access Management With Active Directory

## Objective
The goal was to build a centralized server environment to streamline user management and device security across an organization. This solves the problem of decentralized administration by allowing all employee permissions and security rules to be managed from a single, secure control point.

## Tech Stack & Skills
*   **Systems:** Windows Server 2025, Windows 11, Active Directory (AD DS), File Server Resource Manager (FSRM)
*   **Networking/Security:** Group Policy (GPOs), Account Lockout Policies, Least Privilege, DNS, NTFS Permissions, Storage Quotas
*   **Core Skills:** Identity & Access Management (IAM), Organizational Unit (OU) Design, System Hardening, Troubleshooting, PowerShell Scripting, Automation, Resource Management

## Key Accomplishments
*   **Scalable Infrastructure Design:** Built a logical Organizational Unit (OU) hierarchy to separate users, security groups, and hardware assets, ensuring the environment remains organized as the company grows.
*   **Role-Based Access Control (RBAC):** Provisioned departmental security groups (HR, Finance, IT) and automated resource access by mapping users to specific roles, reducing the risk of unauthorized data access.
*   **Asset Lifecycle Management:** Migrated Windows 11 workstations into the domain and organized them into managed containers to allow for centralized software deployment and monitoring.
*   **System Hardening & Security:** Deployed automated security policies to enforce "Least Privilege," successfully blocking non-admin users from accessing sensitive tools like the Command Prompt and Control Panel.
*   **Brute-Force Protection:** Configured and enforced account lockout thresholds to automatically freeze accounts after five failed login attempts, protecting the network from external password attacks.
*   **Enterprise-Scale Automation:** Automated the creation and security group assignment of 100+ user accounts using a custom PowerShell script, reducing a multi-hour onboarding task to just minutes and eliminating manual errors.
*   **Automated Resource Provisioning:** Deployed Group Policies to automatically map departmental network drives (S:) and deploy shared printers, providing employees with instant, zero-touch access to essential tools upon login.
*   **Efficient Storage Management:** Implemented FSRM to enforce storage quotas and block unauthorized file types (e.g., audio/video), preventing waste and ensuring critical disk space remains available for business operations.

## Final Validation & Project Completion
**The environment is 100% functional, with a verified link between the Server and Windows 11 workstation. All security policies are active, and standard users are successfully restricted from administrative settings.**

> **Full Technical Deep Dive**
> For the specific CLI commands, granular configuration steps, and a detailed implementation log, please see: **[Implementation Log (Detailed Version)](InsertLinkHere.md)**

## Visual Proof

### Policy Enforcement & Least Privilege
*   **Action:** Applied Restricted User GPO.
*   **Context:** Protecting system settings from non-administrative users to prevent unauthorized changes.
*   **Validation:** Logged in as a standard user (Han Solo) and verified that access to the Control Panel and CMD was strictly denied by system policy.
**[Insert Screenshot of "Access Denied" error on W11 Client]**

### Corporate Compliance Branding
*   **Action:** Configured Interactive Logon Banner.
*   **Context:** Establishing legal notice and "Authorized Use" warnings for all employees prior to login.
*   **Validation:** Verified that the custom security warning appears on the Windows 11 lock screen before any user can input credentials.
**[Insert Screenshot of Logon Banner on W11 Client]**

### Automated Resource Deployment
*   **Action:** Linked Drive Mappings and Printer Policy GPOs to user OUs.
*   **Context:** Ensuring all users automatically receive their department-specific shared drive and the office printer without IT intervention.
*   **Validation:** Logged in as a standard user and confirmed the 'S:' drive and Lab_Office_Printer were present and functional in File Explorer.
**[Insert Screenshot of W11 File Explorer showing mapped S: Drive and Printer]**

### Storage Quota Enforcement
*   **Action:** Configured a 100 MB FSRM quota on the Finance share.
*   **Context:** To control storage consumption and prevent a single department from using all available disk space.
*   **Validation:** Attempted to copy a 101 MB file into the Finance share and was blocked by the system due to the quota limit.
**[Insert Screenshot of "File too large for destination" error message]**

### Enterprise User Provisioning & Automation
*   **Action:** Automated the mass creation and categorization of 100 domain users via PowerShell.
*   **Context:** Replaced manual data entry with scalable automation to ensure rapid onboarding and 100% accuracy in departmental assignments.
*   **Validation:** Verified the successful migration of users into specific Active Directory OUs (Organizational Units) and confirmed correct Security Group memberships (Finance, HR, IT Support).
**[Insert Screenshot of PowerShell Script Execution showing "Successfully added" messages]**


## Professional Key Takeaways
*   **Automation & Scalability:** I learned how to manage 100+ users as efficiently as one user by utilizing Group Policy and Security Groups rather than manual configuration.
*   **Security-First Mindset:** I focused on the "Principle of Least Privilege," ensuring that standard employees have exactly what they need to work without the ability to accidentally compromise the network.
*   **Adaptability:** During the lab, I successfully troubleshot an authentication issue by identifying a VM mismatch, demonstrating my ability to remain calm and analytical when technical roadblocks occur.
*   **Automation & Scalability:** I learned how to manage 100+ users as efficiently as one by utilizing PowerShell, Group Policy, and Security Groups, which is essential for any growing organization.
*   **Systematic Troubleshooting:** I demonstrated a methodical approach to problem-solving by diagnosing a complex GPO printer deployment issue, isolating the root cause through a series of validation steps, and implementing a stable fix. This proves my ability to remain calm and analytical when resolving technical roadblocks.
