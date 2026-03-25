# Part 1: Infrastructure Setup

## Objective
Set up a fully functional Windows domain environment with a domain controller and client machine.

## Environment
- Windows Server 2025 (Domain Controller)
- Windows 11 (Client)
- Oracle VirtualBox

## Key Tasks
- Configured a virtual NAT Network (`192.168.0.0/24`) to facilitate communication between VMs.
- Installed and configured Active Directory Domain Services (AD DS) on Windows Server 2025.
- Promoted the server to a Domain Controller for the new forest `lab.local`.
- Configured static IPv4 addressing and DNS settings to ensure proper name resolution.
- Joined the Windows 11 client machine (`W11-CL01`) to the `lab.local` domain and verified the connection in ADUC.

## Outcome
A working domain environment capable of centralized authentication and management, validated by a successful domain join and administrative login from the client workstation.

## Screenshots
- **System Requirements & Info:** `System info.png`, `C: Storage Space.png`
- **Network Configuration:** `NatNetwork_Lab.png`, `IPV4 Settings.png`
- **Server Deployment:** `WS2025-DC01 VM Settings.png`, `VM AD DS.png`
- **Client Deployment:** `W11-CL01 Settings.png`, `W11-CL01 VM Network Settings.png`
- **Domain Verification:** `W11 Has Joined Domain.png`
- **Infrastructure Snapshots:** `Lab Snapshots Final.png`

## Key Takeaways
- **Importance of DNS in AD environments:** Correct DNS pointing (Client pointing to DC) is mandatory for the domain-join process to succeed.
- **Resource Management:** Verifying hardware requirements (CPU cores/RAM) beforehand is essential when running multiple modern virtual machines simultaneously.
- **Host-Level Troubleshooting:** Type-2 hypervisors like VirtualBox may require disabling host features like Hyper-V or Memory Integrity to function correctly (addressing the "Green Turtle" performance issue).
- **Snapshot Strategy:** Creating "Clean State" snapshots after key milestones (AD DS config and Domain Join) provides a vital safety net for future lab experiments.
