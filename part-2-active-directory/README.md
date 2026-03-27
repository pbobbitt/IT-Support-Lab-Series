# Identity & Access Management With Active Directory

## Objective
The goal was to build a centralized server environment to streamline user management and device security across an organization. This solves the problem of decentralized administration by allowing all employee permissions and security rules to be managed from a single, secure control point.

## Tech Stack & Skills
*   **Systems:** Windows Server 2025, Windows 11, Active Directory (AD DS), File Server Resource Manager (FSRM)
*   **Networking/Security:** Group Policy (GPOs), Account Lockout Policies, Least Privilege, DNS, NTFS Permissions, Storage Quotas
*   **Core Skills:** Identity & Access Management (IAM), Organizational Unit (OU) Design, System Hardening, Troubleshooting, PowerShell Scripting, Automation, Resource Management

## Key Accomplishments
###   **Enterprise-Scale Automation:**
*  Automated the creation and security group assignment of 100+ user accounts using a custom PowerShell script, reducing a multi-hour onboarding task to just minutes and eliminating manual errors.

###   **System Hardening & Security**
*  Deployed automated security policies to enforce "Least Privilege," successfully blocking non-admin users from accessing sensitive tools like the Command Prompt and Control Panel.

###   **Automated Resource Provisioning**
*  Deployed Group Policies to automatically map departmental network drives (S:) and deploy shared printers, providing employees with instant, zero-touch access to essential tools upon login.

###   **Role-Based Access Control (RBAC):**
*  Provisioned departmental security groups (HR, Finance, IT) and automated resource access by mapping users to specific roles, reducing the risk of unauthorized data access.

###   **Efficient Storage Management**
*  Implemented FSRM to enforce storage quotas and block unauthorized file types (e.g., audio/video), preventing waste and ensuring critical disk space remains available for business operations.


## Final Validation & Project Completion
**The environment is fully functional and scaled for 100 users. All automated security policies, resource permissions, and network services have been verified as operational, with client workstations successfully receiving all configurations as intended.**

> **Full Technical Deep Dive**
> For the specific CLI commands, granular configuration steps, and a detailed implementation log, please see: **[Implementation Log (Detailed Version)](InsertLinkHere.md)**

## Visual Proof


### Enterprise User Provisioning & Automation
*   **Action:** Automated the mass creation and categorization of 100 domain users via PowerShell.
*   **Context:** Replaced manual data entry with scalable automation to ensure rapid onboarding and 100% accuracy in departmental assignments.
*   **Validation:** Verified the successful migration of users into specific Active Directory OUs (Organizational Units) and confirmed correct Security Group memberships (Finance, HR, IT Support).  
<img src="screenshots/Scaling%20PowerShell%20.png" alt="Users added with powershell" width="49%"> <img src="screenshots/Scaled%20AD%20Users.png" alt=" All Users in AD " width="49%">  

### Policy Enforcement & Least Privilege
*   **Action:** Applied Restricted User GPO.
*   **Context:** Protecting system settings from non-administrative users to prevent unauthorized changes.
*   **Validation:** Logged in as a standard user (Han Solo) and verified that access to the Control Panel and CMD was strictly denied by system policy.  
<img src="screenshots/Finance%20member%20Cant%20use%20CMD%20or%20Control%20Panel.png" alt="Users cant access CMD or Control Panel" width="70%">

### Automated Resource Deployment
*   **Action:** Linked Drive Mappings and Printer Policy GPOs to user OUs.
*   **Context:** Ensuring all users automatically receive their department-specific shared drive and the office printer without IT intervention.
*   **Validation:** Logged in as a standard user and confirmed the 'S:' drive and Lab_Office_Printer were present and functional in File Explorer.  
<img src="screenshots/S%20Drive%20and%20Printer%20Accessible.png" alt="W11 File Explorer showing mapped S: Drive and Printer" width="70%">

### Role-Based Access Control (RBAC) & Identity Management
*   **Action:** Provisioned departmental Security Groups (SG_Finance, SG_HR, SG_IT_Support) and implemented an OU-based exclusion for IT Administrators.
*   **Context:** Establishing a scalable access model where permissions are tied to job functions (Roles) rather than individual user accounts, ensuring consistent security across the domain.
*   **Validation:** Verified that moving users from the Lab_Users OU to the Lab_Admins OU successfully triggered GPO "Filtered" status, allowing IT staff to bypass standard desktop restrictions while keeping Finance and HR restricted.
<img src="screenshots/IT%20member%20Can%20use%20CMD%20or%20Control%20Panel.png" alt="Admins Users can access CMD and Control Panel " width="49%"> <img src="screenshots/SG_IT_Support%20Users%20Correct.png" alt="Users in the Admin Group" width="49%">  

### Storage Quota Enforcement
*   **Action:** Configured a 100 MB FSRM quota on the Finance share.
*   **Context:** To control storage consumption and prevent a single department from using all available disk space.
*   **Validation:** Attempted to copy a 101 MB file into the Finance share and was blocked by the system due to the quota limit.  
<img src="screenshots/Finance%20member%20cant%20add%20101%20MB%20file%20to%20Finance%20folder.png" alt="system blocked the 101 MB transfer" width="70%">


## Professional Key Takeaways
*   **Automation & Scalability:** I learned how to manage 100+ users as efficiently as one user by utilizing Group Policy and Security Groups rather than manual configuration.
*   **Security-First Mindset:** I focused on the "Principle of Least Privilege," ensuring that standard employees have exactly what they need to work without the ability to accidentally compromise the network.
*   **Adaptability:** During the lab, I successfully troubleshot an authentication issue by identifying a VM mismatch, demonstrating my ability to remain calm and analytical when technical roadblocks occur.
*   **Automation & Scalability:** I learned how to manage 100+ users as efficiently as one by utilizing PowerShell, Group Policy, and Security Groups, which is essential for any growing organization.
*   **Systematic Troubleshooting:** I demonstrated a methodical approach to problem-solving by diagnosing a complex GPO printer deployment issue, isolating the root cause through a series of validation steps, and implementing a stable fix. This proves my ability to remain calm and analytical when resolving technical roadblocks.
