### Milestone 1: Structural Foundation (OU Hierarchy)
*Focus: Organizing the Active Directory environment for scalability.*

1.  **Create a Top-Level Organizational Unit (OU).**
2.  **Create Sub-OUs for Departments (Users).**
3.  **Create a Sub-OU for Security Groups.**
4.  **Create a Sub-OU for Managed Workstations.**



### Milestone 2: Identity & Access Management (Users & Groups)
*Focus: Populating the directory with objects and assigning roles.*

1.  **Create at least three unique Domain User accounts.**
2.  **Configure initial User Password settings and account properties.**
3.  **Create Security Groups corresponding to your Department OUs.**
4.  **Assign Users to their respective Security Groups.**



### Milestone 3: Asset Migration (Client Integration)
*Focus: Bringing the workstation under the management of your new OUs.*

1.  **Locate the Windows 11 computer object in the default container.**
2.  **Move the computer object into the newly created Workstations OU.**
3.  **Verify the move within Active Directory Users and Computers (ADUC).**



### Milestone 4: Policy Enforcement (GPOs)
*Focus: Defining the "Business Rules" through Group Policy.*

1.  **Create a new Group Policy Object (GPO) for Account Security** (e.g., Lockout Policy).
2.  **Create a GPO for Desktop Restrictions** (e.g., Prohibiting Control Panel or CMD).
3.  **Create a GPO for "Quality of Life" or Branding** (e.g., Interactive Logon Banner or Wallpaper).
4.  **Link each GPO to the appropriate OU in the Group Policy Management Console (GPMC).**



### Milestone 5: Validation & L1 Support Testing
*Focus: Verifying that your administrative changes are active on the endpoint.*

1.  **Perform a "Force Update" of policies on the Client Machine.**
2.  **Log in as a Standard User and verify successful authentication.**
3.  **Test the GPO restrictions** (e.g., attempt to open a prohibited setting).
4.  **Generate a formal GP Result report on the client to confirm policy application.**
