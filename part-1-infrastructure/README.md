# Part 1: Infrastructure Setup

## Objective
Set up a fully functional Windows domain environment with a domain controller and client machine to simulate a professional corporate network.

## Environment
- Windows Server 2025 (Domain Controller)
- Windows 11 Education (Client)
- Oracle VirtualBox 7.x
- Virtual Network (NAT Network: 192.168.0.0/24)

## Key Tasks
- **Hardware & Resource Planning**
  - Performed a system audit using `msinfo32` to ensure hardware could support multiple virtual machines, allocating 12GB RAM and 6 CPU cores to the project.
- **Virtual Network Configuration**
  - Created a dedicated isolated network (`NatNetwork_Lab`) with DHCP enabled to allow secure communication between the server and the workstation.
- **Domain Controller Deployment (Active Directory)**
  - Installed Windows Server 2025 and promoted it to a Domain Controller for the `lab.local` forest, establishing the foundation for centralized identity management.
- **Network Services Setup (DNS & IPv4)**
  - Configured static IPv4 addressing and DNS roles to ensure the client machine could reliably locate and communicate with the server.
- **Client Integration & Domain Join**
  - Provisioned a Windows 11 workstation and successfully joined it to the `lab.local` domain, verifying the connection through Active Directory Users and Computers (ADUC).
- **Proactive Troubleshooting & Optimization**
  - Resolved virtualization conflicts (Hyper-V interference) and implemented a Snapshot strategy to ensure environment stability and quick recovery.

## Outcome
A working domain environment capable of centralized authentication and management, mimicking a real-world enterprise IT infrastructure.

## Screenshots
- [System info - Hardware Verification](Images/System%20info.png)
- [Network Settings - Virtual Lab Network](Images/NatNetwork_Lab.png)
- [WS2025-DC01 - Active Directory & DNS Confirmation](Images/VM%20AD%20DS.png)
- [W11-CL01 - Domain Join Success](Images/W11%20Has%20Joined%20Domain.png)
- [Lab Snapshots - System Recovery Points](Images/Lab%20Snapshots%20Final.png)

## Key Takeaways
- **Centralized Administration**
  - Learned how to manage users and computers from a single point using **Active Directory**, a critical skill for L1 support.
- **Networking Foundations**
  - Gained hands-on experience with **IPv4, DNS, and Gateway configurations**, ensuring seamless connectivity between enterprise devices.
- **Critical Problem Solving**
  - Successfully diagnosed and fixed system-level errors (Hyper-V/Core Isolation) to ensure software compatibility and performance.
- **Disaster Recovery Basics**
  - Utilized **Snapshots** to create "restore points," demonstrating an understanding of system backups and minimizing downtime.
