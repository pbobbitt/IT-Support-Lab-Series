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


# PowerShell Scripts 

##  **Powershell Quota Test Script (101MB File):**   
Used to verify that the 100MB limit on the Finance folder correctly blocks oversized transfers.

```powershell
$path = "$home\Desktop\TestFile.dat"
$size = 101MB
$file = [System.IO.File]::Create($path)
$file.SetLength($size)
$file.Close()
```

##   **Powershell File Screening Script (1MB .mp4 File):** 

Used to verify that unauthorized file types are blocked even when the user has remaining storage quota.**
    
```powershell
$path = "$home\Desktop\fake video.mp4"
$size = 1MB
$file = [System.IO.File]::Create($path)
$file.SetLength($size)
$file.Close()
```

##   **Mass CSV inport**
This script also handled assigning each new user to their correct departmental Security Group (`SG_Finance`, `SG_HR`, or `SG_IT_Support`) based on the data in the CSV file.
      ```powershell
      # 1. Define where the user list is
      $csvPath = "C:\Users\Administrator\Documents\NewUsers.csv"

      # 2. Loop through every person in that list
      Import-Csv $csvPath | ForEach-Object {
          
          # Set a default password (For this lab they will not have to change it at first login)
          $Password = ConvertTo-SecureString "Testlab1" -AsPlainText -Force
          
          # 3. Create the User in the Lab_Users OU
          New-ADUser -Name "$($_.Firstname) $($_.Lastname)" `
                     -GivenName $_.Firstname `
                     -Surname $_.Lastname `
                     -SamAccountName $_.Username `
                     -UserPrincipalName "$($_.Username)@lab.local" `
                     -Path "OU=Lab_Users,OU=Lab_Production,DC=lab,DC=local" `
                     -AccountPassword $Password `
                     -ChangePasswordAtLogon $false `
                     -Enabled $true
                     
          # 4. Map them to their Security Group based on the CSV "Department" column
          # Note: Groups are named SG_Finance, SG_HR, SG_IT_Support
          $groupName = "SG_$($_.Department)"
          
          try {
              Add-ADGroupMember -Identity $groupName -Members $_.Username
              Write-Host "Successfully added $($_.Username) to $groupName" -ForegroundColor Green
          } catch {
              Write-Host "Failed to add $($_.Username) to $groupName. Check if group exists." -ForegroundColor Red
          }
      }
      ```


##   **Move IT Users to Admin**
Automatically find all users in the `SG_IT_Support` group and move them to the `Lab_Admins` OU. 
      ```powershell
      # 1. Get all members of the IT Support group
      $ITMembers = Get-ADGroupMember -Identity "SG_IT_Support"

      # 2. Move each member to the Lab_Admins OU
      $ITMembers | ForEach-Object {
          Move-ADObject -Identity $_.DistinguishedName -TargetPath "OU=Lab_Admins,OU=Lab_Production,DC=lab,DC=local"
          Write-Host "Moved $($_.Name) to Lab_Admins OU" -ForegroundColor Cyan
      }
      ```
