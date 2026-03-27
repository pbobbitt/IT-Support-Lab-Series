# Milestone 1: Structural Foundation (OU Hierarchy)
*Focus: Organizing the Active Directory environment for scalability.*

* **Created a Top-Level Organizational Unit (OU).**
  * Made Top Level OU Called `Lab_Production`
* Created Sub-OUs for
  * **Departments (Users):** `Lab_Users`
  * **Security Groups:** `Lab_Security`
  * **Managed Workstations:** `Lab_Computers`



# Milestone 2: Identity & Access Management (Users & Groups)
*Focus: Populating the directory with objects and assigning roles.*

* **Create at least three unique Domain User accounts.**
  * Added 3 users:
    * Darth Vader
    * Han Solo
    * Padme Amidala
* **Configure initial User Password settings and account properties.**
  * Used format `first.last@lab.local`
* Created Security Groups corresponding to Department OUs.
  * **Finance:** `SG_Finance`
  * **HR:** `SG_HR`
  * **IT:** `SG_IT_Support`
* **Assign Users to their respective Security Groups.**  
  * Han Solo: `SG_Finance`  
  * Darth Vader: `SG_HR`  
  * Padme Amidala: `SG_IT_Support`
* Confirmed successful domain authentication on `W11-CL01` using the whoami command.



# Milestone 3: Asset Migration (Client Integration)
*Focus: Bringing the workstation under the management of your new OUs.*


* Used Find command on `lab.local` to look for client object `*CL` to find all client workstations
  * Returned with `W11-CL01` used the move command to move this computer to `Lab_Computers` OU   
* Verified the move within Active Directory Users and Computers (ADUC) by looking at `Lab_Computers.`



# Milestone 4: Policy Enforcement (GPOs)
*Focus: Defining the "Business Rules" through Group Policy.*

* **Create a new Group Policy Object (GPO) for Account Security** (e.g., Lockout Policy).
  * Made `Lockout Policy` GPO
    * Goal: to prevent brute force password attacks.
    * Set login attempts to a max of 5 before account lockout.
* **Create a GPO for Desktop Restrictions** (e.g., Prohibiting Control Panel or CMD).
  * Created `Prohibit Control Panel and CMD` GPO
    * Goal: implement least privilege to prevent non-admin users (Han Solo and Darth Vader) from changing system settings or running scripts.
    * Removed control panel and CMD access 
* **Create a GPO for "Quality of Life" or Branding** (e.g., Interactive Logon Banner or Wallpaper).
  * Created `Logon Banner` GPO
  * Goal: Display a legal warning before login
    * Message set to `Authorized Access Only. All activities are monitored.`
* **Link each GPO to the appropriate OU in the Group Policy Management Console (GPMC).**
  * `Lockout Policy` Linked to `lab.local` top-level domain
  * `Prohibit Control Panel and CMD` linked to `Lab_Users`
    * To keep Padme Amidala and other users in the `SG_IT_Support` ou still having access to these to do job functions, a new user OU was created called `Lab_Admins`. `Prohibit Control Panel and CMD` was not applied to this new OU
    * All membors of the `SG_IT_Support` OU were moved from `Lab_Users` to `Lab_Admins`
  * `Logon Banner` Linked to `Lab_Computers`


## Milestone 5: Resource Management (FSRM & Print Services)
**Focus:** Provisioning critical business resources by establishing a centralized file server and automated print services.

*   **Step 1:** Implement a Centralized File Share with NTFS and Share Permissions.
  * On `WS2025-DC01` Created folder on `C:` named `Company_Share`
    * Made 3 subfolders `Finance`, `HR`, `IT`
  * Enabled share this folder on `Company_Share` to everyone with full control (Actual locking will be done with the `Security` tab, this prevents potential conflicts)
  * Subfolder permissions were set to remove `Lab_Users` on the `Security` tab and set these specific permissions for each of the following folders.
    * `Finance` = `SG_Finance`  
    * `HR` = `SG_HR`  
    * `IT` = `SG_IT_Support`
*   **Step 2:** Configure a Network Drive Mapping via Group Policy (GPO).
  *  Enabled share this folder on `Company_Share` to everyone with full control (Actual locking will be done with the `Security` tab, this prevents potential conflicts)
*   **Step 3:** Deploy a Network Printer to Managed Workstations.
*   
*   **Step 4:** Establish Storage Quotas and File Screens using File Server Resource Manager (FSRM).

## Milestone 6: Validation & L1 Support Testing
**Focus:** Verifying that your administrative changes are active on the endpoint.

*   **Step 1:** Perform a "Force Update" of policies on the Client Machine.
*   **Step 2:** Log in as a Standard User and verify successful authentication.
*   **Step 3:** Test the GPO restrictions (e.g., attempt to open a prohibited setting).
*   **Step 4:** Generate a formal GP Result report on the client to confirm policy application.

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| After adding users, I was unable to log in with any of the user accounts | Tested all the users, double-checked the settings, and then saw I was trying to sign into the WS2025 Domain Controller VM | Swapped to the correct W11 VM client and was able to log in |
| While auditing file share permissions, it was discovered `SG_Finance` users had access to all folders | When setting up file share permissions, `SG_Finance` was accidentally added to the root share and inherited down to all subfolders<br><BR>After more testing it was discovered that on the folder interface right clicking alone brings up the root folder the user needs to actually left click the file to select it and then right click to bring up the propeties for the correct sub folder. <BR><BR> It is unclear why this is happening it may be due to this system being a virtual machine but im not sure either way this problem is not in the scope of this project so I'll just document this issue instead | Removed `SG_Finance` from root folder permissions and correctly added them to only the finance folder. Another audit was performed all folders had the correct permissions |
