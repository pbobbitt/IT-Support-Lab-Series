### Milestone 1: Structural Foundation (OU Hierarchy)
*Focus: Organizing the Active Directory environment for scalability.*

* **Created a Top-Level Organizational Unit (OU).**
  * Made Top Level OU Called `Lab_Production`
* Created Sub-OUs for
  * **Departments (Users):** `Lab_Users`
  * **Security Groups:** `Lab_Security`
  * **Managed Workstations:** `Lab_Computers`



### Milestone 2: Identity & Access Management (Users & Groups)
*Focus: Populating the directory with objects and assigning roles.*

* **Create at least three unique Domain User accounts.**
  * Added 3 users:
    * Darth Vader
    * Han Solo
    * Padme Amidala
* **Configure initial User Password settings and account properties.**
  * done used format `first.last@lab.local`
* Created Security Groups corresponding to Department OUs.
  * **Finance:** `SG_Finance`
  * **HR:** `SG_HR`
  * **IT:** `SG_IT_Support`
* **Assign Users to their respective Security Groups.**  
  * Han Solo: `SG_Finance`  
  * Darth Vader: `SG_HR`  
  * Padme Amidala: `SG_IT_Support`
* Confirmed successful domain authentication on `W11-CL01` using the whoami command.



### Milestone 3: Asset Migration (Client Integration)
*Focus: Bringing the workstation under the management of your new OUs.*


* Used Find command on `lab.local` to look for client object `*CL` to find all client workstations
  * Returned with `W11-CL01` used move command to move this computer to `Lab_Computers` OU   
* Verified the move within Active Directory Users and Computers (ADUC). by looking at `Lab_Computers`



### Milestone 4: Policy Enforcement (GPOs)
*Focus: Defining the "Business Rules" through Group Policy.*

* **Create a new Group Policy Object (GPO) for Account Security** (e.g., Lockout Policy).
* **Create a GPO for Desktop Restrictions** (e.g., Prohibiting Control Panel or CMD).
* **Create a GPO for "Quality of Life" or Branding** (e.g., Interactive Logon Banner or Wallpaper).
* **Link each GPO to the appropriate OU in the Group Policy Management Console (GPMC).**



### Milestone 5: Validation & L1 Support Testing
*Focus: Verifying that your administrative changes are active on the endpoint.*

* **Perform a "Force Update" of policies on the Client Machine.**
* **Log in as a Standard User and verify successful authentication.**
* **Test the GPO restrictions** (e.g., attempt to open a prohibited setting).
* **Generate a formal GP Result report on the client to confirm policy application.**


| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| After adding users, I was unable to log in with any of the user accounts | Tested all the users, double-checked the settings, and then saw I was trying to sign into the WS2025 Domain Controller VM| swapped to the correct W11 VM client and was able to log in |
