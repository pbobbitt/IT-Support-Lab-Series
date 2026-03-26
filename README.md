# Enterprise IT Support & Systems Administration Lab Series  


**Professional & Educational Credentials**  
<p align="left">
  <a href="https://linkedin.com/in/patrick-bobbitt"><img src="https://img.shields.io/badge/LinkedIn-Patrick%20Bobbitt-0072b1?style=for-the-badge&logo=linkedin&logoColor=white" /></a> <img src="https://img.shields.io/badge/Education-WGU%20BS%20Cloud%20%26%20Network%20Engineering%20Student-00ADEE?style=for-the-badge&logo=google-scholar&logoColor=white" /> <a href="https://github.com/pbobbitt/pbobbitt/blob/main/CompTIA%20A%2B%20ce%20certificate.pdf"><img src="https://img.shields.io/badge/Certification-CompTIA%20A%2B-E31837?style=for-the-badge&logo=comptia&logoColor=white" /></a>
</p>

**Lab Series Technical Stack**  
<p align="left">
  <img src="https://img.shields.io/badge/Server-Windows%20Server%202025-0078D4?style=for-the-badge&logo=windowsserver&logoColor=white" />
  <img src="https://img.shields.io/badge/Client-Windows%2011-0078D4?style=for-the-badge&logo=windows11&logoColor=white" />
  <img src="https://img.shields.io/badge/Identity & Access Management-Active%20Directory-FF5733?style=for-the-badge&logo=microsoft-active-directory&logoColor=white" />
  <img src="https://img.shields.io/badge/Operations-Ticketing%20Lab-2ea44f?style=for-the-badge&logo=helpdesk&logoColor=white" />
  <img src="https://img.shields.io/badge/Hypervisor-VirtualBox-894ba9?style=for-the-badge&logo=virtualbox&logoColor=white" />
</p>


## Project Overview
This repository contains a comprehensive, three-part technical lab series simulating a real-world enterprise IT environment. The project moves from raw infrastructure deployment to advanced Identity and Access Management (IAM), concluding with a hands-on Help Desk ticketing simulation.

**The Goal:** To build, secure, and manage a corporate network from the ground up, demonstrating proficiency in systems administration, network security, and technical support workflows.


## Core Tech Stack & Competencies
*   **Operating Systems:** Windows Server 2025 (Datacenter), Windows 11 Enterprise
*   **Directory Services:** Active Directory Domain Services (AD DS)
*   **Networking:** DNS, DHCP, Static IPv4 Addressing, NAT Networking
*   **Security & Policy:** Group Policy Objects (GPO), RBAC (Role-Based Access Control), Least Privilege, Account Lockout Policies
*   **Virtualization:** Oracle VirtualBox (Type-2 Hypervisor)
*   **IT Operations:** Disaster Recovery (Snapshots), Documentation, Troubleshooting


## Project Structure

### [Part 1: Windows Server & Infrastructure Build](./part-1-infrastructure/)
**Focus: The Foundation.** 
*   Architected an isolated virtual network environment.
*   Deployed **Windows Server 2025** as a Primary Domain Controller.
*   Provisioned a Windows 11 managed endpoint.
*   **Key Outcome:** A fully functional, stable environment with verified internal/external connectivity and disaster recovery fail-safes.

### [Part 2: Identity & Access Management (Active Directory/GPO)](./part-2-active-directory/)
**Focus: Security & Governance.**
*   Designed a scalable **Organizational Unit (OU)** hierarchy.
*   Implemented **Role-Based Access Control (RBAC)** for HR, Finance, and IT departments.
*   Deployed **Group Policy Objects (GPOs)** to harden endpoints (restricting CMD/Control Panel) and enforce corporate compliance.
*   **Key Outcome:** A secured domain where user permissions are automated based on their job function, significantly reducing the attack surface.

### [Part 3: Help Desk Operations & Ticketing](./part-3-helpdesk-tickets/) *(In Progress)*
**Focus: The User Experience.**
*   Simulating real-world L1/L2 support scenarios.
*   Resolving common issues: Password resets, software deployment, and policy troubleshooting.
*   Utilizing ticketing workflows to document and track "Break/Fix" incidents.
*   **Key Outcome:** Demonstrating the ability to translate technical knowledge into professional end-user support.


## Key Technical Highlights

### Security Hardening
I didn't just build a network; I secured it. By applying the **Principle of Least Privilege (PoLP)**, I ensured that standard users cannot access system-level tools, while "IT Support" users maintain the access needed to perform their duties.

### Troubleshooting & Resilience
Throughout this lab, I resolved critical "low-level" conflicts, including:
*   **Hypervisor Optimization:** Solving "Black Screen" boot errors by managing Hyper-V/Core Isolation conflicts at the host firmware level.
*   **Network Logic:** Rectifying authentication errors caused by VM mismatches, proving a methodical approach to the OSI model.

### Documentation & Governance
Each phase of this project includes a detailed **Implementation Log**. I treat these logs as professional internal documentation, ensuring that every configuration change is auditable and repeatable, a vital skill in any enterprise IT team.


## Contact & Connect
*   **LinkedIn:** [Your LinkedIn Profile Link]
*   **Email:** [Your Professional Email]


