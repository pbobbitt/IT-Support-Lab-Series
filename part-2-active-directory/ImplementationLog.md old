
### Active Directory and Group Policy Lab Implementation Log

 This guide outlines the steps to build a foundational Active Directory structure, create users and groups, implement security policies, and validate the setup. 

 ### **Milestone 1: The Foundation (OU Hierarchy)** 

 **Goal:** Establish a logical Organizational Unit (OU) structure to move away from the default "Users" container. This is crucial for linking Group Policies later on. 

 **Why this is important:** OUs allow you to apply specific policies to different sets of users and computers. It is generally recommended to create your own OU structure rather than using the default containers, as Group Policy Objects (GPOs) cannot be directly applied to default containers. 

 **Steps:** 

 1. **Open Active Directory Users and Computers (ADUC):** This is typically found in the Administrative Tools on your server. 
 2. **Create a new OU:** Right-click on your domain name, select "New," and then "Organizational Unit." 
 3. **Name your OU:** Give it a clear and descriptive name, for example, `Lab_Production`. 
 4. **Create nested OUs:** Right-click on your newly created OU and create sub-OUs for different departments. For example: `Departments` > `IT`, `HR`, `Sales`. It is also a good practice to create a `Workstations` OU to hold computer objects. 

 ### **Milestone 2: Identity Creation (Users & Groups)** 

 **Goal:** Populate the OUs with user accounts and corresponding security groups. 

 **Action:** Create at least 3-4 unique user accounts and security groups, adhering to professional naming conventions. 

 **Steps:** 

 1. **Create Security Groups:** 
 * In ADUC, navigate to the appropriate departmental OU (e.g., `IT`). 
 * Right-click, select "New," and then "Group." 
 * Name your groups with a consistent prefix, such as `SG-IT-Staff`, `SG-HR-Staff`, etc. 
 * Ensure the "Group scope" is set to "Global" and "Group type" is "Security." 
 2. **Create User Accounts:** 
 * Within the same departmental OU, right-click, select "New," and then "User." 
 * Follow professional naming conventions, such as `j.doe` for the user logon name. 
 * Assign a temporary password and select the option for the user to change it at next logon. 
 3. **Add Users to Groups:** 
 * Open the properties of each user account. 
 * Go to the "Member Of" tab and add them to their respective security group (e.g., add `j.doe` to `SG-IT-Staff`). 

 ### **Milestone 3: Desktop Security (Group Policy Objects)** 

 **Goal:** Create and link GPOs to your OUs to enforce security policies. 

 **Suggested Policies:** 

 * **Account Lockout Policy:** This policy helps prevent brute-force attacks by locking out an account after a certain number of failed login attempts. 
 * **Desktop Restriction:** This policy can prevent users in specific departments from accessing certain system settings, like the Control Panel. 
 * **Interactive Logon:** This displays a legal notice or warning banner that users must acknowledge before logging in. 

 **Steps:** 

 1. **Open Group Policy Management Console (GPMC).** 
 2. **Create and Link a GPO:** 
 * Right-click on the OU you want to apply the policy to (e.g., the `HR` OU) and select "Create a GPO in this domain, and Link it here...". 
 * Give the GPO a descriptive name, like `HR_Desktop_Restrictions`. 
 3. **Edit the GPO:** 
 * Right-click the newly created GPO and select "Edit." 
 * This will open the Group Policy Management Editor. 
 4. **Configure the Policies:** 
 * **Account Lockout Policy:** 
 * Navigate to: `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`. 
 * Configure the following settings: 
 * **Account lockout threshold:** 5 invalid logon attempts. 
 * **Account lockout duration:** 30 minutes. 
 * **Reset account lockout counter after:** 30 minutes. 
 * **Desktop Restriction (Prevent Control Panel Access):** 
 * Navigate to: `User Configuration > Policies > Administrative Templates > Control Panel`. 
 * Enable the "Prohibit access to Control Panel and PC settings" policy. 
 * **Interactive Logon (Legal Notice):** 
 * Navigate to: `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options`. 
 * Configure the following policies: 
 * `Interactive logon: Message title for users attempting to log on` 
 * `Interactive logon: Message text for users attempting to log on` 

 ### **Milestone 4: Client Migration** 

 **Goal:** Move your Windows 11 client machine from the default "Computers" container to your newly created `Workstations` OU. 

 **Why this is important:** Policies linked to an OU only affect the objects (users and computers) within that OU. 

 **Steps:** 

 1. **Open Active Directory Users and Computers.** 
 2. **Locate your computer:** Find your `W11-CL01` computer object in the "Computers" container. 
 3. **Move the computer object:** Right-click the computer object, select "Move," and then choose your `Workstations` OU as the destination. 

 ### **Milestone 5: The "L1 Support" Validation** 

 **Goal:** Log in as a standard user to verify that the implemented policies are active. 

 **Verification Steps:** 

 1. **Log into the Windows 11 client:** Use one of the standard user accounts you created (e.g., a user from the HR department). 
 2. **Check for the Interactive Logon banner:** The legal notice you configured should appear before you can enter your credentials. 
 3. **Verify GPO application with `gpresult`:** 
 * Open a Command Prompt. 
 * Run the command `gpresult /r`. This will display the Resultant Set of Policy (RSoP) for the user and computer. 
 * Look for your created GPOs in the output to confirm they have been applied. 
 4. **Test the desktop restriction:** 
 * Attempt to open the Control Panel. 
 * You should receive an "Access Denied" or similar message, confirming the policy is working.
