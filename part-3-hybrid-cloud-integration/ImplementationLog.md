# Project Overview
This lab connects an existing on-premise Windows Server 2025 Active Directory, containing 100 users, to Microsoft's cloud environment. By establishing this "Hybrid Identity" setup, local users are synced to a free Microsoft 365 Enterprise environment managed by Entra ID. Additionally, Microsoft Intune is used to automatically secure and deploy software to corporate computers over the internet, proving the ability to manage a remote workforce efficiently and securely. Finally, a Jira helpdesk system is set up as a foundational step for future ticketing and troubleshooting labs.

## Milestone 1: Microsoft 365 Cloud Setup
**Focus:** Provisioning a free enterprise-grade cloud environment to host the synced directory.

* Enrolled in the [Microsoft 365 Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program)
  * Signed up for a free Developer account.
    * Selected `Applications for internal use> all areas> Configurable sandbox`
  * Made an account and a custom domain name for the cloud environment.
    * Domain name: `pbitsupport.onmicrosoft.com`

> **Evidence:** See **Microsoft 365 Admin Center**
<img src="Screenshots/M365%20E5%20configurable%20sandbox%20account.png" alt="M365 Admin Center" width="70%">
<BR>

## Pre- Milestone 2: Troubleshooting

Before starting to install Entra Connect on the local lab enviroment i looked on Microsoft Learn and saw there was a known issue for Active Directory directory synchronization when used with Entra Connect Sync, which both of those will be used in the next section. Here is the [Microsoft database entry for the issue](https://learn.microsoft.com/en-us/windows/release-health/resolved-issues-windows-server-2025#3692msgdesc)
  
  > "Applications that use the Active Directory directory synchronization (DirSync) control for on-premises Active Directory Domain Services (AD DS), such as when using Microsoft Entra Connect Sync, can result in incomplete synchronization."

The listed fix is the Windows `KB5068861` update. I checked my install, and luckily, my Windows Server 2025 install already had this specific update, but I wanted to note this, as if this error were more recent, this would possibly lead to a lot of issues with this setup. But i did see my Windows server needed a Windows update, which i attempted to install...

<img src="Screenshots/DC%20Windows%20Patch%20needed.png" alt="DC Windows Patch Needed" width="70%">

Then I ran into a Storage controller `Error (VERR_DISK_FULL)` on VirtualBox

#### Root Cause Analysis
* **Problem:** VirtualBox error `VERR_DISK_FULL` appeared. 
* **Cause:** The physical host SSD (1.81 TB) reached critical capacity (only 23.9 MB remaining), preventing the VM from expanding its dynamically allocated disk.
* **Resolution (CompTIA 6-Step Methodology):**
    1. **Identify:** Domain controller VM hit "Paused" status in VirtualBox and displayed `Error (VERR_DISK_FULL)`. Checked the Host OS main storage drive and confirmed the Host OS was out of space.
    2. **Theory:** While downloading the cumulative updates (KB5070773) required for the Entra Connect installation, the Virtual Machine lacked the buffer space required on the host OS for the VM to write update files.
    3. **Action:** Performed host-level cleanup, clearing ~60GB of data.
    4. **Verification:** Successfully resumed the VM and completed the OS patching without further issues.

<img src="Screenshots/Error%20(VERR_DISK_FULL).png" alt="Error (VERR_DISK_FULL)" width="35%"><img src="Screenshots/Host%20PC%20Storage%20Full.png" alt="Host PC Storage Full" width="60%">
  
## Milestone 2: Entra Connect Installation
**Focus:** Installing the tool that links the local Windows Server 2025 Domain Controller to the new cloud environment.

*   **Log into your Windows Server 2025 Domain Controller VM.**
  *   {Make sure the virtual machine has an active internet connection so it can reach Microsoft's servers.}
*   **Download the Microsoft Entra Connect installer.**
  *   {Search for "Download Microsoft Entra Connect" in the server's web browser and download the official tool.}
*   **Run the installer and choose "Express Settings".**
*   **Enter your cloud credentials.**
  *   {When prompted, enter the M365 Global Admin credentials you created in Milestone 1.}
*   **Enter your local credentials.**
  *   {When prompted, enter your local Enterprise/Domain Admin credentials for your Windows Server 2025 environment.}
*   **Click Install and wait for the initial synchronization to finish.**

> **Evidence:** See **{Screenshot of the "Configuration Complete" screen in the Entra Connect setup wizard}**
<img src="#" alt="{Image showing Entra Connect successfully installed on the Domain Controller}" width="70%">
<BR>

## Milestone 3: Hybrid Identity Verification
**Focus:** Confirming that the 100 local Active Directory users successfully populated into the cloud portal.

*   **Log into the Microsoft Entra Admin Center in your web browser.**
*   **Navigate to the "Users" > "All Users" panel.**
*   **Locate your lab users in the directory list.**
  *   {Search for users from your local 100-user roster, such as Han Solo or Darth Vader, to ensure they transferred over.}
*   **Verify the sync status column.**
  *   {Check the "On-premises sync enabled" column. It should say "Yes" next to your local users, proving they are linked to your home lab.}

> **Evidence:** See **{Screenshot of the Entra Admin Center showing your local users in the cloud directory}**
<img src="#" alt="{Image of the cloud user list with the 'On-premises sync enabled' column showing 'Yes'}" width="70%">
<BR>

## Milestone 4: Helpdesk Foundation (Jira Setup)
**Focus:** Establishing a basic IT Service Management ticketing system to prepare for future support simulation labs.

*   **Go to the Atlassian website and sign up for Jira Service Management.**
  *   {Select the "Free" tier.}
*   **Create a new IT Service Desk project.**
  *   {Name it something relevant to your lab, like "Lab IT Helpdesk".}
*   **Set up basic request categories.**
  *   {Create a small "Service Catalog" with placeholder categories like "New Hire Onboarding" and "Software Install". You will not make any actual tickets in this phase, just set up the blank boards.}

> **Evidence:** See **{Screenshot of your empty Jira Service Management IT dashboard}**
<img src="#" alt="{Image showing the newly created Jira helpdesk project ready for future tickets}" width="70%">
<BR>

## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| {Example: Could not log into the Microsoft 365 Developer Program / Placed on a waitlist.} | {Example: Microsoft updated their rules and flagged my personal `@outlook.com` email for manual review.} | {Example: Signed up again using my WGU `.edu` student email, which bypassed the waitlist entirely and instantly granted me the E5 tenant.} |
| {Example: Entra Connect failed to authenticate my cloud credentials during setup.} | {Example: The Windows Server 2025 VM network adapter was set to "Host-Only" in VirtualBox, meaning it could not reach the internet to verify the login.} | {Example: Changed the VM network adapter settings to "NAT", verified I could ping google.com, and restarted the Entra Connect wizard successfully.} |
| {Enter your issue here} | {Enter why it happened here} | {Enter how you fixed it and verified it here} |
