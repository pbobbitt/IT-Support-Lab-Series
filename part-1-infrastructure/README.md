# Windows Server 2025 & Active Directory Infrastructure

## Objective
The goal was to deploy a centralized Windows Server 2025 environment to manage users, devices, and security policies from a single interface. This solves the business problem of "unmanaged hardware" by ensuring every laptop and server on the network follows company security standards and can be managed remotely.

## Tech Stack & Skills
*   **Systems:** Windows Server 2025 (Datacenter Edition), Windows 11, Oracle VirtualBox 7.x (Hypervisor)
*   **Networking & Security:** DNS (Domain Name System), DHCP, Static IP Addressing, NAT Networking, Forest/Domain Architecture
*   **Core Skills:** Active Directory Users & Computers (ADUC), Identity & Access Management (IAM), Disaster Recovery (Snapshots), System Optimization & Hardening

## Key Accomplishments
*   **Centralized Identity Management:** Deployed a **Windows Server 2025 Domain Controller** (`lab.local`) to act as the central "brain" of the network, allowing for one-click user onboarding and offboarding.
*   **Network Infrastructure Design:** Engineered an isolated **NAT Network** with custom IPv4 addressing and **Static IPs**, ensuring the server has a permanent, reliable "address" that workstations can always find.
*   **Secure Endpoint Integration:** Successfully joined a **Windows 11 Workstation** to the professional domain, moving the device from a standalone state to a managed asset that obeys corporate security rules.
*   **Disaster Recovery Preparedness:** Established **System Snapshots** (State-in-time backups) for all infrastructure. This ensures the business can recover from a system failure or a botched update in seconds rather than hours.
*   **Hardware Compatibility Troubleshooting:** Resolved complex **Hyper-V and Core Isolation conflicts** at the firmware level to ensure the virtualization environment remained stable and high-performing.

## Final Validation & Project Completion
**The enterprise environment is 100% operational, with a verified secure link between the Windows Server 2025 Domain Controller and the Windows 11 workstation, confirming that centralized management and DNS services are fully functional.**

> **[Full Technical Deep Dive]**
> For the specific CLI commands, granular configuration steps, and a detailed implementation log, please see: **[Implementation Log (Detailed Version)](InsertLinkHere.md)**

## Visual Proof

### Domain Integration & Centralized Management
*   **Action:** Joined the Windows 11 workstation to the `lab.local` domain.
*   **Context:** Bringing a new employee device under company control so it can receive security updates and policies.
*   **Validation:** Verified the workstation (`W11-CL01`) appears correctly within the **Active Directory Users and Computers (ADUC)** management console on the server.
**[Insert Screenshot of ADUC showing W11-CL01 in the Computers Container]**

### End-to-End Connectivity
*   **Action:** Performed internal and external Ping tests.
*   **Context:** Ensuring the workstation can reach both the internal server for files and the external internet for updates.
*   **Validation:** Confirmed 0% packet loss to both the Domain Controller (`192.168.0.10`) and external DNS (`8.8.8.8`).
**[Insert Screenshot of successful Ping tests]**

## Professional Key Takeaways
*   **Scalability:** I learned how to manage an entire fleet of computers as easily as managing one, using Active Directory to automate what would otherwise be manual tasks.
*   **Resource Management:** I gained experience in capacity planning, ensuring that virtualized hardware (RAM/CPU) was allocated efficiently to prevent system slowdowns.
*   **Technical Resilience:** By troubleshooting "Black Screen" boot errors related to Windows Security features, I demonstrated the ability to research and solve low-level system conflicts that stop a project in its tracks.
