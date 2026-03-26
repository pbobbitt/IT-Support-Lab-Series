# Windows Server 2025 & Active Directory Deployment Lab

## Milestone 1: Environment Readiness & Resource Planning
**Focus:** Ensuring the physical hardware can support the virtual infrastructure and gathering the necessary software components.

*   **Conducted a hardware audit to ensure the host computer could handle multiple virtual machines.**
    *   Calculated the total resources needed (approximately 4 CPU cores, 12GB of RAM, and 160GB of storage) to run the Server and Windows 11 client simultaneously.
    *   Verified the host system’s specifications using the `msinfo32` command, confirming it exceeded requirements with 32GB of RAM and a 6-core (12-thread) processor, and 250GB of storage. 
*   **Prepared the Virtualization Platform.**
    *   Installed Oracle VirtualBox 7.x as the "Type-2 Hypervisor" to manage the virtual hardware.
    *   Added the VirtualBox Extension Pack to enable support for modern features like NVMe disk performance and encrypted connections.
*   **Acquired the necessary Operating System images (ISOs).**
    *   Downloaded Windows Server 2025 Datacenter Edition to serve as the Primary Domain Controller (the "brain" of the network).
    *   Downloaded Windows 11 Education to serve as the managed workstation for testing user policies and security settings.
*   **Verified storage availability for the virtual environment.**
    *   Confirmed 224GB of free disk space on the host drive to accommodate the growth of the virtual hard disks during the lab.

## Milestone 2: Virtual Network Configuration
**Focus:** Establishing an isolated network environment to allow communication between the server and future client workstations.

*   **Created a dedicated NAT Network named `NatNetwork_Lab`.**
*   **Defined the network addressing scheme.**
    *   Configured the network to use the `192.168.0.0/24` IP range, providing a professional and organized internal address space.
*   **Enabled DHCP (Dynamic Host Configuration Protocol).**
    *   This ensures that any new device added to the lab automatically receives an IP address, simplifying the connection process.

## Milestone 3: Server Provisioning & Operating System Installation
**Focus:** Deploying the virtual hardware and installing Windows Server 2025 as the foundation of the lab.

*   **Built the `WS2025-DC01` Virtual Machine.**
    *   Allocated 4GB of RAM and 2 processors to ensure the server runs efficiently.
    *   Created an 80GB "Dynamically Allocated" virtual disk, allowing the lab to grow in size only as data is actually added.
*   **Configured Virtual Hardware settings.**
    *   Attached the VM to the `NatNetwork_Lab` created in the previous phase.
    *   Mounted the Windows Server 2025 ISO to the virtual optical drive to begin the boot process.
*   **Completed the Windows Server 2025 Installation.**
    *   Initialized the setup using the "Set up for work or school" configuration to prepare for enterprise-level management.
    *   Established the primary Administrator account for the server.
*   **Verified baseline network connectivity.**
    *   Performed a successful `ping` test to 8.8.8.8 to confirm the server could communicate through the virtual network and reach the internet.

## Milestone 4: System Optimization & Network Identification
**Focus:** Enhancing the server's usability and establishing a permanent, static identity on the network.

*   **Improved the virtual machine’s performance and integration.**
    *   Installed "VirtualBox Guest Additions," which allows for better screen resolution, smoother mouse movement, and easier file sharing between the host and the server.
*   **Established a Static IP address for the server.**
    *   Configured the network settings manually to ensure the server’s address never changes—a critical step for any machine providing central services to a network.
    *   Disabled IPv6 to simplify the network environment and prevent connectivity conflicts during the lab.
*   **Standardized the server’s naming convention.**
    *   Changed the computer name from a random default string to `WS2025-DC01`. 
    *   This follows professional IT standards, identifying the machine as "Windows Server 2025 - Domain Controller 01."
*   **Verified the new configuration.**
    *   Used the `ipconfig` command to confirm the manual network settings were applied correctly and the server was properly identified on the virtual network. 

## Milestone 5: Active Directory Domain Services (AD DS) Installation
**Focus:** Transforming the standalone server into a "Domain Controller," which acts as the central command center for the entire network.

*   **Installed the Active Directory Domain Services role.**
    *   Utilized the Server Manager "Add Roles and Features" wizard to prepare the server for its new identity as a network manager.
*   **Promoted the server to a Domain Controller and established a new "Forest."**
    *   Created a new directory structure named `lab.local`, which serves as the private root for all users, computers, and security policies in this environment.
*   **Configured Domain Functional Levels and Disaster Recovery.**
    *   Set the forest and domain functional levels to "Windows Server 2025" to ensure the network can utilize the most modern security and performance features.
    *   Established a Directory Services Restore Mode (DSRM) password to ensure the database can be recovered in the event of a system failure.
*   **Captured the configuration for future automation.**
    *   Reviewed and exported the setup as a PowerShell script before finalizing the installation. This is a professional best practice that allows this entire deployment to be automated or replicated in a real-world business setting.
*   **Finalized the installation and performed a system reboot.**
    *   Completed the promotion and restarted the machine, officially initializing the `lab.local` domain and making the server ready to manage client workstations.


## Milestone 6: Client Workstation Deployment
**Focus:** Provisioning and installing a Windows 11 endpoint to serve as a managed device within the network.

*   **Created the virtual hardware for the client workstation.**
    *   Named the machine `W11-CL01` and allocated 4GB of RAM and 2 CPU processors to meet system requirements.
    *   Configured an 80GB "Dynamically Allocated" virtual disk to efficiently manage physical storage space.
*   **Prepared the installation environment.**
    *   Attached the VM to the `NatNetwork_Lab` and mounted the Windows 11 Education ISO.
*   **Performed the Windows 11 Operating System installation.**
    *   Bypassed the Microsoft Account requirement by selecting the "Domain Join Instead" option, creating a local administrative account named `LabAdmin`.
    *   Streamlined the OS performance by disabling resource-heavy privacy settings such as location tracking and diagnostic data collection.

## Milestone 7: Client Configuration & Network Identity
**Focus:** Finalizing the workstation setup and establishing a permanent, static presence on the laboratory network.

*   **Optimized the virtual machine user experience.**
    *   Installed VirtualBox Guest Additions to enable advanced features like shared clipboards, smoother mouse integration, and proper screen resolution.
*   **Standardized the workstation’s network name.**
    *   Renamed the computer to `W11-CL01` within the system settings to match the lab's naming convention, making it easily identifiable for the Domain Controller.
*   **Configured Static IPv4 Network Settings.**
    *   Manually assigned the IP address `192.168.0.100` to the workstation. 
    *   Using a static address instead of a dynamic one ensures the machine is always reachable at a predictable location during testing.
*   **Verified end-to-end network connectivity.**
    *   Performed successful "ping" tests to both the external internet (8.8.8.8) and the internal Server (192.168.0.10) to confirm the workstation was correctly communicating with the entire environment.

## Milestone 8: Domain Integration & Client Verification
**Focus:** Finalizing the connection between the workstation and the server to enable centralized security and management.

*   **Initiated the domain join process on the Windows 11 workstation.**
    *   Utilized the system properties tool (`sysdm.cpl`) to transition the machine from a standalone "Workgroup" to the professional `lab.local` domain environment.
*   **Authenticated the secure connection.**
    *   Provided the Domain Administrator credentials (`LAB\Administrator`) to authorize the workstation’s entry into the network, ensuring only approved devices can join the domain.
*   **Validated the successful integration on the Domain Controller.**
    *   Confirmed that the workstation `W11-CL01` appeared correctly within the "Computers" container of the Active Directory Users and Computers (ADUC) management console.
*   **Performed a final verification of the machine's identity.**
    *   Verified that the server now recognizes the Windows 11 client as a managed asset, allowing for future deployment of security policies and user accounts.


## Milestone 9: Environment Preservation (System Snapshots)
**Focus:** Establishing a "fail-safe" restoration point to protect the lab's progress and ensure system stability for future testing.

*   **Created a baseline snapshot for the Domain Controller (`WS2025-DC01`).**
    *   Named the snapshot `Base-ADDS-Configured` to mark the exact moment the Active Directory forest and DNS were fully operational.
*   **Created a baseline snapshot for the Windows 11 Workstation (`W11-CL01`).**
    *   Named the snapshot `Base-Domain-Joined` to preserve the state where the machine is successfully authenticated, the static IP is set, and the domain integration is verified.
*   **Established a "Rollback" strategy for the lab environment.**
    *   By capturing these snapshots, the entire network can be reverted to this clean, working state in seconds. This acts as an insurance policy, allowing for aggressive security testing or complex configuration changes without the risk of having to rebuild the virtual machines from scratch.
*   **Verified the snapshot tree within VirtualBox.**
    *   Confirmed that both machines are synchronized at the same point in time, ensuring the internal relationship between the server and the client remains intact upon restoration.

## Project Completion & Final Validation
**Focus:** Verifying the integrity of the network and ensuring all systems are communicating as intended.

*   **Verified the Health of the Domain Controller.**
    *   Confirmed that Windows Server 2025 is successfully broadcasting the `lab.local` domain and managing DNS requests for the internal network.
*   **Validated Centralized Endpoint Management.**
    *   Confirmed the Windows 11 workstation (`W11-CL01`) is a "Trustworthy" member of the domain. This was verified by locating the computer object within the Active Directory Users and Computers (ADUC) console.
*   **Confirmed End-to-End Connectivity.**
    *   Verified that both the Server and Client can communicate through the virtual switch, ensuring that future security policies (GPOs) will deploy correctly across the network.
*   **Established Environment Stability.**
    *   Finalized the lab by creating "Clean State" snapshots. This ensures the entire environment can be restored to this exact working configuration in seconds, providing a reliable foundation for future advanced security testing.
*   **Outcome:**
    *   The lab is now a fully functional, enterprise-grade directory environment. I have successfully moved from raw hardware requirements to a managed network where a single server can control, secure, and update multiple client workstations from one central location.

## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| On first run of [VM](Images/networking%20missing.png) couldn't find "network" under `Files>Tools`   | VM [preferences](Images/Preferences%20set%20as%20basic.png) were set to basic | Changed VM [preference](Images/networking%20is%20now%20listed.png) to expert and "networks" appeared under `Files>Tools>network` |
| [VM Boot Failure / Black Screen](Images/VM%20Black.png) | Hyper-V / Core Isolation enabled on Host (Warning is Green Turtle icon). were set to basic | Disabled Hyper-V via [bcdedit](https://github.com/pbobbitt/Windows-Server-2025-Virtual-Infrastructure-Deployment/blob/main/Images/Disabled%20Hyper-V%20bootloader.png) and toggled off [Memory Integrity](Images/Disabled%20Memory%20Integrity.png) to allow VirtualBox native VT-x/AMD-V access. Confirmed [VirtualBox now runs](Images/VM%20Working.png) |

---
*End of Implementation Log*


