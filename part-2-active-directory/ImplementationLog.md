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

*   **Implemented a Centralized File Share with NTFS and Share Permissions.**
    *   On the server `WS2025-DC01`, created a main folder on the C: drive named `Company_Share`.
    *   Inside `Company_Share`, created three subfolders: `Finance`, `HR`, and `IT`.
    *   Configured the main `Company_Share` folder to be shared with "Everyone" having full control. This initial open setting prevents permission conflicts, as specific security will be handled at the subfolder level.
    *   Modified the security permissions for each subfolder to grant exclusive access to the correct department group:
        *   `Finance` folder access was granted to the `SG_Finance` group.
        *   `HR` folder access was granted to the `SG_HR` group.
        *   `IT` folder access was granted to the `SG_IT_Support` group.
*   **Configured a Network Drive Mapping via Group Policy (GPO).**
    *   Created a new GPO named `Drive Mappings`.
    *   Within this GPO, set up policies to automatically map the 'S:' drive for users based on their department's security group.
        *   Members of `SG_Finance` are mapped to `\\WS2025-DC01\Company_Shares\Finance`.
        *   Members of `SG_HR` are mapped to `\\WS2025-DC01\Company_Shares\HR`.
        *   Members of `SG_IT_Support` are mapped to `\\WS2025-DC01\Company_Shares\IT`.
    *   Linked the `Drive Mappings` GPO to both the `Lab_Users` and `Lab_Admins` OUs to ensure all employees, including IT staff, receive the mapped drive.
*   **Deployed a Network Printer to Managed Workstations.**
    *   Added the "Print and Document Services" role to the server.
    *   Set up a new shared network printer named `Lab_Office_Printer`.
    *   Created a new GPO called `Printer Policy` to automatically deploy this printer to users.
    *   Linked the `Printer Policy` GPO to the `Lab_Users` and `Lab_Admins` OUs so all users would have access to the printer.
*   **Established Storage Quotas and File Screens using File Server Resource Manager (FSRM).**
    *   Added the "File Server Resource Manager" role to the server.
    *   Set up storage quotas on the `Finance`, `HR`, and `IT` folders, limiting each to a maximum size of 100 MB.
    *   Created a file screen on the main `Company_Shares` folder to block users from saving audio and video file types.
       
# Milestone 6: Validation & Audit Before Scaling
**Focus:** Testing and documenting user access, policy enforcement, and resource restrictions to ensure the environment is secure and stable before mass-scaling the directory.

*   **Step 1:** Performed a cross-departmental permission audit.
    *   Verified that users in the `Finance` group can successfully access the [Finance folder](#) but are correctly blocked from seeing or accessing the HR or IT folders.
    *   Confirmed that members of the IT group are also properly restricted to their designated [IT folder](#).
    *   This test validates that the specific folder permissions (NTFS) and security group rules are correctly overriding the more general "Everyone: Full Control" setting on the main share.
*   **Step 2:** Verified Group Policy enforcement and its exceptions.
    *   **Restriction Test:** Logged in as a standard Finance user (Han Solo) and confirmed that both the Command Prompt and Control Panel were successfully [blocked](#) as intended by the policy.
    *   **Exception Test:** Logged in as an IT user (Padme Amidala) and confirmed that the Command Prompt and Control Panel remained [accessible](#), proving that the exclusion for the `Lab_Admins` OU is working correctly.
    *   **Banner Test:** Confirmed that the legal warning banner appears on the [login screen](#) of the workstation for all users.
*   **Step 3:** Confirmed automatic provisioning of network resources.
    *   Verified that both the S: Drive and the `Lab_Office_Printer` are automatically mapped and visible to the user upon login [without any manual intervention](#).
    *   Used the `gpresult /r` command on the client computer to generate a report, which confirmed that all the correct policies are being [applied to the user's session](#).
*   **Step 4:** Validated the enforcement of resource limits.
    *   **Quota Test:** As a standard user, attempted to copy a 101MB file into the Finance folder, which has a 100MB limit. Verified that the [system blocked the transfer](#) because the quota would be exceeded.
        *   **Powershell Quota Test Script (101MB File):** Used to verify that the 100MB limit on the Finance folder correctly blocks oversized transfers.
          ```powershell
          $path = "$home\Desktop\TestFile.dat"
          $size = 101MB
          $file = [System.IO.File]::Create($path)
          $file.SetLength($size)
          $file.Close()
          ```
    *   **Screening Test:** Attempted to save a video file (.mp4) to the shared folder. Verified the system blocked the action because of the file type, even though the user still had available storage space.
        *   **Powershell File Screening Script (1MB .mp4 File):** Used to verify that unauthorized file types are blocked even when the user has remaining storage quota.
          ```powershell
          $path = "$home\Desktop\fake video.mp4"
          $size = 1MB
          $file = [System.IO.File]::Create($path)
          $file.SetLength($size)
          $file.Close()
          ```
    
## Milestone 7: Scalability & Automation
**Focus:** Demonstrating enterprise-level administration by using PowerShell to automate the mass creation and categorization of 100 domain users.

*   **Step 1:** Developed a master list of users.
    *   To simulate a large-scale environment, a structured CSV file was created. This file acted as a blueprint, containing the Firstname, Lastname, Username, and Department for 97 additional staff members.
    *   The file followed the structure below. The full list can be viewed [here](#).
      ```
      Firstname,Lastname,Username,Department
      Han,Solo,han.solo,Finance
      Darth,Vader,darth.vader,HR
      Padme,Amidala,padme.amidala,IT_Support
      ```

*   **Step 2:** Automated user creation with a PowerShell script.
    *   A script was executed to read the master list and automatically create an Active Directory account for each person.
    *   This script also handled assigning each new user to their correct departmental Security Group (`SG_Finance`, `SG_HR`, or `SG_IT_Support`) based on the data in the CSV file.
      ```powershell
      # 1. Define where the user list is
      $csvPath = "C:\Users\Administrator\Documents\NewUsers.csv"

      # 2. Loop through every person in that list
      Import-Csv $csvPath | ForEach-Object {
          
          # Set a default password (For this lab they will not have to change it at first login)
          $Password = ConvertTo-SecureString "Testlab1" -AsPlainText -Force
          
          # 3. Create the User in the Lab_Users OU
          New-ADUser -Name "$($_.Firstname) $($_.Lastname)" `
                     -GivenName $_.Firstname `
                     -Surname $_.Lastname `
                     -SamAccountName $_.Username `
                     -UserPrincipalName "$($_.Username)@lab.local" `
                     -Path "OU=Lab_Users,OU=Lab_Production,DC=lab,DC=local" `
                     -AccountPassword $Password `
                     -ChangePasswordAtLogon $false `
                     -Enabled $true
                     
          # 4. Map them to their Security Group based on the CSV "Department" column
          # Note: Groups are named SG_Finance, SG_HR, SG_IT_Support
          $groupName = "SG_$($_.Department)"
          
          try {
              Add-ADGroupMember -Identity $groupName -Members $_.Username
              Write-Host "Successfully added $($_.Username) to $groupName" -ForegroundColor Green
          } catch {
              Write-Host "Failed to add $($_.Username) to $groupName. Check if group exists." -ForegroundColor Red
          }
      }
      ```

*   **Step 3:** Verified account creation and finalized placements.
    *   Confirmed that all 100 accounts were correctly created within the `Lab_Users` OU and were active for login. ![Verification Image](#)
    *   Checked the security groups to ensure all new users were placed into the correct department groups. ![Verification Image](#)
    *   Since IT staff require access to administrative tools, a second script was run to automatically find all users in the `SG_IT_Support` group and move them to the `Lab_Admins` OU. This ensures they are not impacted by policies that restrict tools for standard users.
    *   The successful move of these users was confirmed. ![Verification Image](#) ![Verification Image](#)
      ```powershell
      # 1. Get all members of the IT Support group
      $ITMembers = Get-ADGroupMember -Identity "SG_IT_Support"

      # 2. Move each member to the Lab_Admins OU
      $ITMembers | ForEach-Object {
          Move-ADObject -Identity $_.DistinguishedName -TargetPath "OU=Lab_Admins,OU=Lab_Production,DC=lab,DC=local"
          Write-Host "Moved $($_.Name) to Lab_Admins OU" -ForegroundColor Cyan
      }
      ```

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| After adding users, I was unable to log in with any of the user accounts | Tested all the users, double-checked the settings, and then saw I was trying to sign into the WS2025 Domain Controller VM | Swapped to the correct W11 VM client and was able to log in |
| While auditing file share permissions, it was discovered `SG_Finance` users had access to all folders | When setting up file share permissions, `SG_Finance` was accidentally added to the root share and inherited down to all subfolders<br><BR>After more testing it was discovered that on the folder interface right clicking alone brings up the root folder the user needs to actually left click the file to select it and then right click to bring up the propeties for the correct sub folder. <BR><BR> It is unclear why this is happening it may be due to this system being a virtual machine but im not sure either way this problem is not in the scope of this project, so I'll just document this issue instead | Removed `SG_Finance` from root folder permissions and correctly added them to only the finance folder. Another audit was performed all folders had the correct permissions |
| **In Pre-Scale Audit, no users were able to access the `Lab_Office_Printer`** | There were several key root issues identified:<br><br>1. **Pathing Error:** The GPO was pointing at `\\WS2025-DC01` instead of the FQDN `\\WS2025-DC01.lab.local` under **Point and Print Restrictions**.<br><br>2. **GPO Block:** Running `gpupdate` as Padme (Admin) returned the error: *"Windows failed to apply the Deployed Printer Connections settings,"* suggesting the GPO was detected but the connection was being rejected by client security.<br><br>3. **Driver Staging:** Attempted a registry edit on the W11 Client (`RestrictDriverInstallationToAdministrators = 0`) at `HKLM\...\Printers\PointAndPrint` to allow driver installation, but the issue persisted.<br><br>4. **Manual Handshake Failure:** Attempted manual connection via **Win+R** to `\\WS2025-DC01.lab.local`. It failed with error code **`0x00000490`** (Element not found).<br><br>5. **Driver Architecture:** Error `0x00000490` indicated the **Microsoft IPP Class Driver** was failing to handshake. Attempted to swap to **Generic/Text Only**, but the server returned a "not supported" error, locking the configuration. | **Resolution:**<br>Successfully resolved by deleting the stubborn printer object on the server and recreating it from scratch using the **Generic / Text Only** driver. <br><br>Additionally, updated the **Point and Print Restrictions** GPO path to correctly point to the FQDN (`\\WS2025-DC01.lab.local`).<br><br>**Verification:** After a final `gpupdate /force`, the printer successfully appeared on all client devices for both [Admin](#) and Standard [User](#) accounts. |


