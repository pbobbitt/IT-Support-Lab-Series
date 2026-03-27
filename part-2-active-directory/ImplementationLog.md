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

*  **Implement a Centralized File Share with NTFS and Share Permissions.**
   * On `WS2025-DC01` Created folder on `C:` named `Company_Share`
      * Made 3 subfolders: `Finance`, `HR`, `IT`
    * Enabled share this folder on `Company_Share` to everyone with full control (Actual locking will be done with the `Security` tab; this prevents potential conflicts)
    * Subfolder permissions were set to remove `Lab_Users` on the `Security` tab and set these specific permissions for each of the following folders.
      * `Finance` = `SG_Finance`  
      * `HR` = `SG_HR`  
      * `IT` = `SG_IT_Support`
*   **Configure a Network Drive Mapping via Group Policy (GPO).**
    *  Created GPO `Drive Mappings`
    * Set drive mappings under `User Configuration>Preferences>Windows Settings>Drive Maps` then `Drive Maps>New>Mapped Drive`
    * Created a new mapped drive for each of the following with the drive letter `s` <BR><BR>
    
    | Path | Department | Securtiy Group|
    | - | - | - | 
    | \\WS2025-DC01\Company_Shares\Finance | Finance | SG_Finance |
    | \\WS2025-DC01\Company_Shares\HR | HR | SG_HR |
    | \\WS2025-DC01\Company_Shares\IT | IT | SG_IT_Support |
    
    * Assigned `Drive Mappings` to `Lab_User` and `Lab_Admins` because the IT support staff are actually in the admin OU, and we want this to apply to all users
       
* **Deploy a Network Printer to Managed Workstations.:**
  * Created Print Server Role
    * `Server Manager>Manage>Add Roles and Features>Print and Document Services.`
  * Created network printer named `Lab_Office_Printer`
    * `Tools>Print Management>Print Servers > WS2025-DC01 > Printers`
    * Port: `LPT1`
    * Driver: `Microsoft IPP Class Driver`
    * Share this printer: Enabled
  * Granted users access via GPO
    * From `Lab_Office_Printer` used `Deploy with Group Policy`
    * Created `Printer Policy` GPO
      * Assigned to `Lab_Users` and `Lab_Admins`
      * Made sure `The users that this GPO applies to (per user)` is checked
    
*   **Establish Storage Quotas and File Screens using File Server Resource Manager (FSRM).**
  * Added `File Server Resource Manager` role
    * `Server Manager>Manage>Add Roles and Features>Expand File and Storage Services>Expand File and iSCSI Services`
  * Establish Storage Quotas
    *  `Server Manager>Tools > File Server Resource Manager>Quota Management>Quotas`
    *  Added Quota for `Finance`, `HR`, and `IT`
        * 100 MB Limit
    * Established File Screens
      * `Server Manager>Tools > File Server Resource Manager>File Screens>`
      * Added File Screen for root folder `C:\Company_Shares`
        * Blocked Audio and Video Files
       
# Milestone 6: Validation & Audit Before Scaling
*Focus: Testing and documenting user access, policy enforcement, and resource restrictions to ensure the environment is secure and stable before mass-scaling the directory.*

* **Cross-Departmental Permission Audit**
  * Verified that `Finance` members can successfully access the [Finance folder](#) and can not see or access the HR or IT folders.
  * Confirmed IT members who also have Admin status are similarly restricted to only the [IT folder](#).
    >This validates that the NTFS permissions and Security Group mappings are correctly overriding the "Everyone: Full Control" share setting. 
* **GPO Enforcement & Exception Verification**
  * Restriction Test: Logged in as Han Solo (Finance) and attempted to open the Command Prompt and Control Panel; verified both were [blocked](#) by Group Policy.
  * Exception Test: Logged in as Padme Amidala (IT) and verified that CMD and Control Panel remain [accessible](#), confirming the Lab_Admins OU is correctly excluded from the restriction GPO.
  * Banner Test: Confirmed the legal warning banner appears on the W11-CL01 [login screen](#) for all users.
* **Network Resource Auto-Provisioning**  
  * Verified that the S: Drive (Mapped Drive) and the Lab_Office_Printer are automatically mapped and visible in File Explorer/Devices upon login [without manual user intervention](#).
  * Used the gpresult /r command on the client workstation to generate a report confirming all policies are being [applied to the user session](#).
* **Resource Limit Enforcement (FSRM Validation)**
  * Quota Test: Attempted to copy a 101MB file into the 100MB-limited Finance folder as Han Solo; verified the [system blocked the transfer due to insufficient space](#).
    * **1. Powershell Quota Test Script (101MB File)**
Used to verify that the 100MB limit on the Finance folder correctly blocks oversized transfers.
```powershell
$path = "$home\Desktop\TestFile.dat"
$size = 101MB
$file = [System.IO.File]::Create($path)
$file.SetLength($size)
$file.Close()
```
  * Screening Test: Attempted to save a .mp4 video file to the share; verified the File Screen blocked the write operation despite having remaining storage quota.
    * **1. Powershell File Screening Script (1MB .mp4 File)**
Used to verify that unauthorized file types are blocked even when the user has remaining storage quota.
```powershell
$path = "$home\Desktop\fake video.mp4"
$size = 1MB
$file = [System.IO.File]::Create($path)
$file.SetLength($size)
$file.Close()
```
    
## Milestone 7: Scalability & Automation
**Focus:** Demonstrating enterprise-level administration by using PowerShell to automate the mass creation and categorization of 100 domain users.

*   **Develop a CSV User Database**
    * Created a structured .csv file containing Firstname, Lastname, Username, and Department for 97 additional staff members to simulate a full-scale corporate environment.
*   **Scripted User Creation via PowerShell**
    * Developed and executed a PowerShell script to iterate through the CSV, automatically generating AD accounts with standardized User Principal Names (UPN) and secure default passwords.
*   **Automated Security Group Mapping**
    * Integrated logic into the script to automatically assign each new user to their respective departmental Security Group (SG_Finance, SG_HR, or SG_IT_Support) based on the CSV data.
*   **Bulk Account Activation and OU Placement**
    * Verified all 100 accounts were correctly provisioned within the Lab_Users OU and enabled for immediate domain authentication.
{Use as many/few steps as are needed to complete the Milestone}

## Milestone 8: Validation & L1 Support Testing
**Focus:** Verifying that your administrative changes are active on the endpoint.

*   **Step 1:** Perform a "Force Update" of policies on the Client Machine.
*   **Step 2:** Log in as a Standard User and verify successful authentication.
*   **Step 3:** Test the GPO restrictions (e.g., attempt to open a prohibited setting).
*   **Step 4:** Generate a formal GP Result report on the client to confirm policy application.

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| After adding users, I was unable to log in with any of the user accounts | Tested all the users, double-checked the settings, and then saw I was trying to sign into the WS2025 Domain Controller VM | Swapped to the correct W11 VM client and was able to log in |
| While auditing file share permissions, it was discovered `SG_Finance` users had access to all folders | When setting up file share permissions, `SG_Finance` was accidentally added to the root share and inherited down to all subfolders<br><BR>After more testing it was discovered that on the folder interface right clicking alone brings up the root folder the user needs to actually left click the file to select it and then right click to bring up the propeties for the correct sub folder. <BR><BR> It is unclear why this is happening it may be due to this system being a virtual machine but im not sure either way this problem is not in the scope of this project, so I'll just document this issue instead | Removed `SG_Finance` from root folder permissions and correctly added them to only the finance folder. Another audit was performed all folders had the correct permissions |
| **In Pre-Scale Audit, no users were able to access the `Lab_Office_Printer`** | There were several key root issues identified:<br><br>1. **Pathing Error:** The GPO was pointing at `\\WS2025-DC01` instead of the FQDN `\\WS2025-DC01.lab.local` under **Point and Print Restrictions**.<br><br>2. **GPO Block:** Running `gpupdate` as Padme (Admin) returned the error: *"Windows failed to apply the Deployed Printer Connections settings,"* suggesting the GPO was detected but the connection was being rejected by client security.<br><br>3. **Driver Staging:** Attempted a registry edit on the W11 Client (`RestrictDriverInstallationToAdministrators = 0`) at `HKLM\...\Printers\PointAndPrint` to allow driver installation, but the issue persisted.<br><br>4. **Manual Handshake Failure:** Attempted manual connection via **Win+R** to `\\WS2025-DC01.lab.local`. It failed with error code **`0x00000490`** (Element not found).<br><br>5. **Driver Architecture:** Error `0x00000490` indicated the **Microsoft IPP Class Driver** was failing to handshake. Attempted to swap to **Generic/Text Only**, but the server returned a "not supported" error, locking the configuration. | **Resolution:**<br>Successfully resolved by deleting the stubborn printer object on the server and recreating it from scratch using the **Generic / Text Only** driver. <br><br>Additionally, updated the **Point and Print Restrictions** GPO path to correctly point to the FQDN (`\\WS2025-DC01.lab.local`).<br><br>**Verification:** After a final `gpupdate /force`, the printer successfully appeared on all client devices for both [Admin](#) and Standard [User](#) accounts. |


