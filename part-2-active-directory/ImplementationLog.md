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


# Milestone 5: Resource Management (FSRM & Print Services)

**Focus:** Provisioning critical business resources by establishing a centralized file server and automated print services.

### Implement a Centralized File Share with NTFS and Share Permissions

*   **Objective:** Create a centralized location for file storage with granular access control.
*   **Key Actions:**
    *   Establish a shared folder on a designated server.
    *   Configure NTFS permissions to define user and group access rights at the file and folder level.
    *   Set up Share Permissions to control network access to the shared folder.

### Configure a Network Drive Mapping via Group Policy (GPO)

*   **Objective:** Automatically map the centralized file share as a network drive for users upon login.
*   **Key Actions:**
    *   Create a new Group Policy Object (GPO) linked to the appropriate organizational unit (OU).
    *   Navigate to `User Configuration > Preferences > Windows Settings > Drive Maps`.
    *   Configure a new mapped drive, specifying the drive letter, location (path to the file share), and other relevant settings.

### Deploy a Network Printer to Managed Workstations

*   **Objective:** Automate the installation of network printers on client machines.
*   **Key Actions:**
    *   Install and share the printer on a print server.
    *   Utilize Group Policy to deploy the printer to specific users or computers.
    *   Navigate to `User Configuration` or `Computer Configuration > Policies > Windows Settings > Deployed Printers`.

### Establish Storage Quotas and File Screens using File Server Resource Manager (FSRM)

*   **Objective:** Manage storage utilization and control the types of files stored on the server.
*   **Key Actions:**
    *   Install the File Server Resource Manager (FSRM) role on the file server.
    *   **Quotas:** Define storage limits for specific volumes or folders to prevent excessive disk space consumption.
    *   **File Screens:** Create rules to block certain file types (e.g., .mp3, .exe) from being saved to the file share.


# Milestone 6: Validation & L1 Support Testing

**Focus:** Verifying that your administrative changes are active on the endpoint.

### Perform a "Force Update" of policies on the Client Machine

*   **Objective:** Immediately apply any new or updated Group Policy settings without waiting for the default refresh interval.
*   **Key Actions:**
    *   Open a Command Prompt on the client machine.
    *   Execute the command: `gpupdate /force`.

### Log in as a Standard User and verify successful authentication

*   **Objective:** Confirm that a non-administrative user can successfully log in and access their environment.
*   **Key Actions:**
    *   Log off from any administrative accounts on the client machine.
    *   Log in using the credentials of a standard user account within the domain.

### Test the GPO restrictions (e.g., attempt to open a prohibited setting)

*   **Objective:** Ensure that the configured Group Policy restrictions are being correctly enforced.
*   **Key Actions:**
    *   As the standard user, attempt to access a feature or setting that was restricted via GPO (e.g., Control Panel, specific settings pages).
    *   Verify that access is denied as expected.

### Generate a formal GP Result report on the client to confirm policy application

*   **Objective:** Create a detailed report to verify which Group Policy Objects are being applied to the user and computer.
*   **Key Actions:**
    *   Open a Command Prompt on the client machine.
    *   Execute the command: `gpresult /h C:\temp\gpresult.html` (or another accessible path).
    *   Open the generated HTML file to review the applied GPOs and troubleshoot any issues.


| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| After adding users, I was unable to log in with any of the user accounts | Tested all the users, double-checked the settings, and then saw I was trying to sign into the WS2025 Domain Controller VM| swapped to the correct W11 VM client and was able to log in |
