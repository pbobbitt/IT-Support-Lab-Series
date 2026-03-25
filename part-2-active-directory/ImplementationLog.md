
### Implementation Log

 ### **Milestone 1: The Foundation (OU Hierarchy)** 

 **Goal:** Establish a logical Organizational Unit (OU) structure to move away from the default "Users" container. This is crucial for linking Group Policies later on. 

 **Why this is important:** OUs allow you to apply specific policies to different sets of users and computers. It is generally recommended to create your own OU structure rather than using the default containers, as Group Policy Objects (GPOs) cannot be directly applied to default containers. 

 **Steps:** 

**Create a new OU:** 

**Create nested OUs:**

 ### **Milestone 2: Identity Creation (Users & Groups)** 

 **Goal:** Populate the OUs with user accounts and corresponding security groups. 

 **Action:** Create at least 3-4 unique user accounts and security groups, adhering to professional naming conventions. 

 **Steps:** 

 1. **Create Security Groups:** 

 2. **Create User Accounts:** 

 3. **Add Users to Groups:** 


 ### **Milestone 3: Desktop Security (Group Policy Objects)** 

 **Goal:** Create and link GPOs to your OUs to enforce security policies. 

 **Suggested Policies:** 

 * **Account Lockout Policy:** This policy helps prevent brute-force attacks by locking out an account after a certain number of failed login attempts. 
 * **Desktop Restriction:** This policy can prevent users in specific departments from accessing certain system settings, like the Control Panel. 
 * **Interactive Logon:** This displays a legal notice or warning banner that users must acknowledge before logging in. 

 **Steps:** 

 1. **Open Group Policy Management Console (GPMC).** 
 2. **Create and Link a GPO:** 
 3. **Edit the GPO:**  
 4. **Configure the Policies:** 
 * **Account Lockout Policy:** 

 * **Account lockout threshold:**
 * **Account lockout duration:**
 * **Reset account lockout counter after:**
 * **Desktop Restriction (Prevent Control Panel Access):** 
 * Enable the "Prohibit access to Control Panel and PC settings" policy. 
 * **Interactive Logon (Legal Notice):** 
 * Configure the following policies:
 * 

 ### **Milestone 4: Client Migration** 

 **Goal:** Move your Windows 11 client machine from the default "Computers" container to your newly created `Workstations` OU. 

 **Why this is important:** Policies linked to an OU only affect the objects (users and computers) within that OU. 

 **Steps:** 

 

 ### **Milestone 5: The "L1 Support" Validation** 

 **Goal:** Log in as a standard user to verify that the implemented policies are active. 

 **Verification Steps:** 

 1. **Log into the Windows 11 client:** Use one of the standard user accounts you created (e.g., a user from the HR department). 
 2. **Check for the Interactive Logon banner:** The legal notice you configured should appear before you can enter your credentials. 
 3. **Verify GPO application with `gpresult`:** 
 4. **Test the desktop restriction:** 
