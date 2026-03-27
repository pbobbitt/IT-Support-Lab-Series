| Command line input | Context / Use Case |
| :--- | :--- |
| **whoami** | Verified current logged-in domain user context. |
| **whoami /groups** | Verified group memberships for the current user session. |
| **gpupdate /force** | Forced immediate application of new Group Policies without waiting for the refresh interval. |
| **gpresult /r** | Generated a summary report of applied policies on the client machine for auditing. |
| **$path = "$home\Desktop\TestFile.dat"; $size = 101MB; $file = [System.IO.File]::Create($path); $file.SetLength($size); $file.Close()** | PowerShell script used to generate a 101MB dummy file to test FSRM folder quotas. |
| **$path = "$home\Desktop\fake video.mp4"; $size = 1MB; $file = [System.IO.File]::Create($path); $file.SetLength($size); $file.Close()** | PowerShell script used to generate a 1MB .mp4 file to test FSRM file screening policies. |
| **Import-Csv <Path> \| ForEach-Object { New-ADUser ... }** | Automated the mass creation of 100 users and assigned them to departmental security groups. |
| **Get-ADGroupMember -Identity "SG_IT_Support" \| Move-ADObject -TargetPath <OU_Path>** | Bulk moved IT staff from the standard Users OU to the Admins OU to bypass GPO restrictions. |
| **HKLM\...\Printers\PointAndPrint\RestrictDriverInstallationToAdministrators = 0** | Registry edit to allow non-admin users to install the shared network printer driver. |
| **Win + R -> \\\\WS2025-DC01.lab.local** | Manual network handshake test to verify SMB access and DNS resolution. |
