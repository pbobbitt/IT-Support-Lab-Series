# Project Overview
This lab connects an existing local network (a Windows Server 2025 containing 100 users) to Microsoft's cloud environment. By establishing this "Hybrid Identity" setup, local users are copied over to a free Microsoft 365 Enterprise workspace. Additionally, Microsoft Intune is used to automatically secure and deploy software to company computers over the internet, proving we can efficiently manage a remote workforce.


**Systems Used:** created in 
<BR>
[Part 1: Windows Server & Infrastructure Build](https://github.com/pbobbitt/IT-Support-Lab-Series/tree/main/part-1-infrastructure)
[Part 2: Identity & Access Management With Active Directory]( https://github.com/pbobbitt/IT-Support-Lab-Series/tree/main/part-2-active-directory)
<BR><BR>
Domain Controller (Main Server): `WS2025-DC01`
<BR>
Client Device (Work Computer): `W11-CL01`

## Milestone 1: Microsoft 365 Cloud Setup
**Focus:** Provisioning a free enterprise-grade cloud environment to host the synced directory.

* Enrolled in the [Microsoft 365 Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program)
  * Signed up for a free Developer account.
    * Selected `Applications for internal use> all areas> Configurable sandbox`
  * Made an account and a custom domain name for the cloud environment.
    * Domain name: `pbitsupport.onmicrosoft.com`
    * Admin account: `Admin@pbitsupport.onmicrosoft.com`

> **Evidence:** See **Microsoft 365 Admin Center Dashboard**
<img src="Screenshots/M365%20E5%20configurable%20sandbox%20account.png" alt="M365 Admin Center" width="70%">
<BR>

## Pre-Milestone 2: Troubleshooting

Before starting to install Entra Connect on the local lab environment, I looked on Microsoft Learn and saw there was a known issue with Active Directory directory synchronization when used with Entra Connect Sync, which both will be used in the next section. Here is the [Microsoft database entry for the issue](https://learn.microsoft.com/en-us/windows/release-health/resolved-issues-windows-server-2025#3692msgdesc)
  
  > "Applications that use the Active Directory directory synchronization (DirSync) control for on-premises Active Directory Domain Services (AD DS), such as when using Microsoft Entra Connect Sync, can result in incomplete synchronization."

The listed fix is the Windows `KB5068861` update. I checked my Windows Server 2025 install; luckily, it already had this specific update. I wanted to note this, as if this error were more recent, it could lead to a lot of issues with this setup. But i did see my Windows server needed a Windows update, which i attempted to install...

<img src="Screenshots/DC%20Windows%20Patch%20needed.png" alt="DC Windows Patch Needed" width="70%">

Then I ran into a Storage controller `Error (VERR_DISK_FULL)` on VirtualBox

### Root Cause Analysis
* **Problem:** VirtualBox error `VERR_DISK_FULL` appeared. 
* **Cause:** The physical host SSD (1.81 TB) reached critical capacity (only 23.9 MB remaining), preventing the VM from expanding its dynamically allocated disk.
* **Resolution (CompTIA 6-Step Methodology):**

    1. **Identify:** <br>
    Domain controller VM hit "Paused" status in VirtualBox and displayed `Error (VERR_DISK_FULL)`. 

    2. **Establish Theory:** <br>
    While downloading the cumulative updates (KB5070773) required for the Entra Connect installation, the Virtual Machine lacked the buffer space required on the host OS for the VM to write update files.

    3. **Test Theory:** <br>
    Checked the Host OS main storage drive and confirmed the Host OS was out of space.

    4. **Plan & Implement:** <br>
    The Host is my personal PC so i performed host-level cleanup, clearing ~60GB of data. Didn't make a longer write-up about this as it is not a part of this cloud migration lab.

    5. **Verification:** <br>
    Successfully resumed the VM and completed the OS patching without further issues.

<img src="Screenshots/Error%20(VERR_DISK_FULL).png" alt="Error (VERR_DISK_FULL)" width="35%"><img src="Screenshots/Host%20PC%20Storage%20Full.png" alt="Host PC Storage Full" width="60%">

> **Evidence:** See **Windows up to date"**
<img src="Screenshots/DC%20Windows%20Patch%20Updated.png" alt="DC Windows Patch Updated" width="70%">
<BR>
  
## Milestone 2: Entra Connect Installation
**Focus:** Installing the tool that securely bridges our local network server to the new Microsoft cloud environment.

* Downloaded Entra Connect from the [Microsoft Download Center](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted)
  * Read and followed the current best practices listed by [Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-roadmap#install-azure-ad-connect)
  * Used Connect Sync as it covers the scope of the lab environment  
* Running Connect Sync showed my `lab.local` domain was not routable via the internet, and that I would need to register with a domain registrar. This is out of scope of this lab so instead i added `pbitsupport.onmicrosoft.com` as an alternative UPN suffix.
  * Added `pbitsupport.onmicrosoft.com` by going to
    * `Active Directory Domains and Trusts > on top folder Right click - Properties > added alternative UPN suffix.`
  * On `Active Directory Users and Computers`, updated all users under both Lab_Admins and Lab_Users to now use `pbitsupport.onmicrosoft.com` as the UPN suffix by
    * `Lab_Admins > Ctrl + A > Right click - Properties > Account > check UPN Suffix > pbitsupport.onmicrosoft.com `
   
> Notice: In a real enterprise environment, we would have had a real domain to map these users onto to maintain the `@lab.local`. Due to that being out of the scope of this lab series, I instead opted to map the existing and future accounts to use the alternate UPN of `@pbitsupport.onmicrosoft.com`. In my lab environment, I would then start a Change Management Plan to use this new domain to sign in and to change all onboarding to reflect the change. This was done to establish a seamless Single Sign-On (SSO) experience and to eliminate authentication errors. <BR><BR>
> Currently, users can use:
> * `first.last@lab.local` Works on local accounts and file shares, but should instead use the new login now
> * `first.last@pbitsupport.onmicrosoft.com` Works on local accounts, file shares, and O365, Entra, and email. This login will be the default used in this environment from now on 

* Went through the rest of the Connect Sync Express setup
  * Cloud admin account: `Admin@pbitsupport.onmicrosoft.com`
  * Local admin account: `LAB\Administrator`
  * Left everything else default
 
* After that, I re-ran the Connect sync to customize the installation after the express setup had more options to select.
  * Syncronization options changed:
    * Enabled Entra ID app and Attribute filtering
    * Password hash synchronization
    
> **Evidence:** See **Connect Sync Complete**
<img src="Screenshots/Connect%20Complete.png" alt="Connect Sync Complete" width="70%">
<BR>

## Milestone 3: Hybrid Identity Verification
**Focus:** Confirming that the 100 local Active Directory users have successfully populated into the cloud portal.

* Logged into the [Microsoft Entra Admin Center](https://azure.microsoft.com/)
  * Confirmed User profiles synced
    * `Manage > Users`
    * Verified all 100 users (31 from admin, 69 from users) synced into the Microsoft Entra environment, which shows 101 users (100 from active directory + 1 cloud admin)

   <img src="Screenshots/Users%20Synced.png" alt="Users Synced" width="70%">
<BR>

  * Confirmed security groups synced
    * `Manage > Groups`
    * This shows 12 groups, the 3 that we set up in a previous lab `SG_Finance, SG_HR, and SG_IT_Support`, and 9 base groups of Entra ID
    * Spot checked each group to ensure that the correct users ended up there
      
   <img src="Screenshots/SGs%20Synced.png" alt="security groups" width="70%">
<BR>

  * Gpos / Devices/ Configuration Profiles
    * GPOs do not sync to Entra ID, so instead we will set up Configuration Profiles on [Intune](https://intune.microsoft.com/#home)
      * On Intune admin center `Devices > Configuration > Create > New Policy`
        * Platform: Windows 10 and later, Profile type: Settings catalog
        * Made a demo policy to set the start page and new page for Chrome and Edge to [IT Support Lab Series](https://github.com/pbobbitt/IT-Support-Lab-Series)
          * `Intune > Devices > Configuration > Create`
        * Assigned to `SG_Finance and SG_HR` left `SG_IT_Support` on default browser behaivior for troubleshooting.
       
<img src="Screenshots/Internet%20startup.gif" alt="Internet Start up" width="70%">
<BR>

   * Enrolled the client machine `W11-CL01` into Intune
      * on Domain Controller: `WS2025-DC01`
        * Created new GPO `Entra Enroll` at
          * `Computer configuration > Administrative template > Windows components > Device registration`
          * Enabled "register domain joined computers as devices"
          * Applied to lab.local
          * ran CLI `gpupdate /force`
        * With Connect sync
          * set Device options to have `configure hybrid microsoft entra ID join"
          * on Windows 10 or later devices
          * SCP set `lab.local` as the forest going to `Entra ID` using Hybrid Microsoft Entra Join
      * In order to use Intune, I have to assign them licenses for this Lab i have 25 licenses I can assign but I have 101 users so i will have to assign licenses on a per need basis
        * On Microsoft 365 Admin Center
          * `Users > Active Users`
          * Assigned active licenses to 
            * Han Solo: SG_Finance
            * Darth Vader: SG_HR
            * Padme Amidala: SG_IT_Support (this is an admin group)
           

<img src="Screenshots/Limited%20Licenses%20Assigned.png" alt="Limited Licenses Assigned" width="70%">
<BR> 

   * On `W11-CL01`
        * Logged in as Padme Amidala to enroll the deivce in to the MDM,
          * `Settings > Accounts > Access work or school` Signed in with Padme Amidala's account
        * Registered this device in the MDM. Now, this device is enrolled, so it should apply to all users who use it.
        
       
<img src="Screenshots/Internet%20startup%20in%20action.gif" alt="Internet Start up in action" width="45%">
<BR>

* Verified all 100 users (31 from admin, 69 from users) Synced into the Microsoft Entra environment, which shows 101 users (100 from active directory + 1 cloud admin) 

> **Evidence:** See **Hybrid Identity Verification**
<img src="Screenshots/Hybrid%20Users%20Synced.png" alt="M365 Admin Center" width="70%">
<BR>


## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| Directory Synchronization Known Issues | Microsoft identified a [known issue](https://learn.microsoft.com/en-us/windows/release-health/resolved-issues-windows-server-2025#3692msgdesc) in Windows Server 2025 where applications using DirSync (like Entra Connect) could fail to sync fully without specific patching. | Researched documentation on Microsoft Learn and verified that `KB5068861` was already installed on the local DC. This ensured a stable baseline before proceeding with the cloud integration | 
| Virtual Machine [`VERR_DISK_FULL`](Screenshots/Error%20(VERR_DISK_FULL).png) error. | The physical host SSD ran out of [storage capacity](Screenshots/Host%20PC%20Storage%20Full.png) during the KB5070773 update, preventing the update and potentially leaving security vulnerabilities. To resolve, I cleaned files from the Host device. Verified by successfully resuming the VM and finishing the [OS update](Screenshots/DC%20Windows%20Patch%20Updated.png). |
| Entra Sync issue with [Non-Routable Domain](Screenshots/Lab.local%20non-routable.png) (lab.local) | Entra ID can only verify publicly hosted domains, so the private `@lab.local` accounts could not be used. This would prevent users from signing into cloud services with their local IDs. | Added `@pbitsupport.onmicrosoft.com` as an alternative [UPN suffix](Screenshots/UPN%20update.png) and updated all user accounts to use that new domain as the primary. Verified change went live on [Entra ID](Screenshots/Lab.local%20non-routable%20error%20fixed.png), ensuring a seamless Single Sign-On (SSO) |
| Had Issues adding devices to Intune | None of my 101 users had an active license, so they could do Entra Join, but not MDM Enrollment | I have 25 Microsoft 365 E5 Developer licenses. I [assigned 3 of them](Screenshots/Limited%20Licenses%20Assigned.png), but will need to cycle these as I have 101 users. | 
| License assignment "invalid Usage Location" | Synced users had a null 'Usage Location' attribute, blocking license assignment. | Manually updated Usage Location to 'United States' in M365 Admin Center to satisfy regional compliance. |
| GPO Lockout (Settings) | "Disable Settings" GPO prevented manual Intune sync on the client VM. | Utilized an account from the SG_IT_Support group (excluded from the GPO) to perform the initial MDM registration. |



