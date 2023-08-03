# Active Directory PowerShell Commands

---

## Table of Contents -

- [Active Directory Commands](#Active_Directory_Commands)
- [Windows Server & Client Commands](#Windows_Server_&_Client_Commands)
- [Basic Powershell Commands](#Basic_Powershell_Commands)
- [Misc](#Misc)

---

### Active_Directory_Commands -

1. View all Active Directory commands

```powershell
Get-Command -Module ActiveDirectory
```

2. Display Basic Domain Info

```powerhell
Get-AdDomain
```

3. Get all Domain Controllers by Hostname and Operating

```powershell
Get-ADDomainController -filter * | select hostname, operatingsystem
```

4. Get all Fine Grained Password Policies

```powershell
Get-ADFineGrainedPasswordPolicy -filter *
```

5. Get Domain Default Password Policy

```powerhell
Get-ADDefaultDomainPasswordPolicy
```

<hr>

#### AD User Commands -

6. Get User and List All Properties (attributes)

```powershell
Get-ADUser Username -Properties *
```

7. Get User and List Specific Properties

```powershell
Get-ADUser Username -Properties * | Select name, department, title
```

8. Get All Active Directory Users in Domain

```powershell
Get-ADUser -Filter *
```

9. Get All Users From a Specific OU [NOTE: OU --> the distinguished path of the OU]

```powershell
Get-ADUser -SearchBase “OU=MYADC Users,dc=ad,dc=example.com” -Filter *
```

10. Get AD Users by Name

```powershell
Get-AdUser -Filter {name -like "*L0u51f3r007*"}
```

11. Get All Disable User Accounts

```powershell
Search-ADAccount -AccountDisabled | select name
```

12. Disable User Account

```powershell
Disable-ADAccount -Identify Robin
```

13. Enable User Account

```powershell
Enable-ADAccount -Identify Robin
```

14. Get All Accounts with Password Set to Never Expire

```powershell
Get-ADUser -Filter * -Properties Name, PasswordNeverExpires | where {$_.passwordNeverExpires -eq "true"} | Select-Object DistinguishedName,Name,Enabled
```

15. Find All Locked User Accounts

```powershell
Search-ADAccount -LockedOut
```

16. Unlock User Account

```powershell
Search-ADAccount -LockedOut
```

17. List all Disabled User Accounts

```powershell
Search-ADAccount -AccountDisabled
```

18. Force Password Change at Next Login

```powershell
Set-ADUser -Identity Username -ChangePasswordAtLogon $true
```

19. Move a Single User to a New OU

```powershell
Move-ADObject -Identity "CN=Test-User (0001),OU=MYADC Users,DC=ad,DC=example,DC=com" -TargetPath "OU=HR,OU=MYADC Users,DC=ad,DC=EXAMPLE,DC=com"
```

<hr>

#### AD Group Commands -

20. Get All members Of A Security Group

```powershell
Get-ADGroupMember -identity “HR Full”
```

21. Get All Security Groups [NOTE: This will list all security groups in a domain]

```powershell
Get-ADGroup -Filter *
```

22. Add User to Group [NOTE: Change GROUP_NAME to the AD group you want to add users to.]

```powershell
ADD-ADGroupMember -Indentify GROUP_NAME -Members USER1,USER2
```

23. Export Users From a Group [NOTE: This will export group members to a CSV, change GROUP_NAME to the group you want to export.]

```powershell
Get-ADGroupMember -Identity “GROUP_NAME” | Select name | Export-csv -path C:\OutputGroupmembers.csv -NoTypeInformation
```

24. Get Group by keyword [NOTE: Find a group by keyword. Helpful if you are not sure of the name, change GROUP_NAME.]

```powershell
Get-ADGroup -Filter * | Where-Object [$_.name -Like "*GROUP_NAME*"]
```

<hr>

#### AD Computer Commands -

25. Get All Computers

```powershell
Get-ADComputer -Filter *
```

26. Get All Computers by Name

```powershell
Get-ADComputer -Filter * | Select name
```

27. Get All Computers from an OU

```powershell
Get-ADComputer -SearchBase "OU=DN" -Filter *
```

28. Get a Count of all Computers in Doamin

```powershell
Get-ADComputer -Filter * | Measure
```

29. Get all Win 10 Computers

```powershell
Get-AdComputer -Filter {OperatingSystem -Like "*Windows 10*"} -Property * | Select name,operatingsystem
```

30. Get a Count of All computers by Operating System

```powershell
Get-ADComputer -Filter "Name -like '*'" -Properties OperatingSystem | Group -Property OperatingSystem | Select Name,Count
```

31. Delete a single Computer

```powershell
Remove-ADComputer -Identify "USER04-SRV-01"
```

32. Delete a list of Computer Accounts

```powershell
Get-Content -Path C:\ComputerList.txt | Remove-ADComputer
```

33. Delete Computers From an OU

```powershell
Get-ADComputer -SearchBase "OU=DN" -Filter * | Remote-ADComputer
```

<hr>

#### Group Policy Commands -

34. Get all GPO related commands

```powershell
Get-Command -Module GroupPolicy
```

35. Get all GPOs in the Domain

```powershell
Get-GPO -All | Select DisplayName,gpostatus
```

36. Backup all GPOs in the Domain

```powershell
Backup-GPO -All -Path E:\GPObackup
```

<hr>

### Windows_Server_&_Client_Commands -

1. Get all Services

```powershell
Get-Service
```

2. Get all processes

```powershell
Get-Process
```

3. Display Network Adapters [NOTE: Gets detailed about the network adapter installed such as name,  status, speed and mac address.]

```powershell
Get-NetAdapter
```

4. Restart Remote Computers

```powershell
Restart-Computer -ComputerName "Sever01","Server02","localhost"
```

5. Get Last Boot time 

```powershell
$os = Get-WmiObject win32_operatingsystem $uptime = (Get-Date) - 
$os.ConvertToDateTime($os.LastBootUpTime) Write-Output ("Last boot: " + 
$os.ConvertToDateTime($os.LastBootUpTime))
```

You can also run this single line to get last boot time -

```powershell
systeminfo | more
```

6. Start a Remote Session [IMPORTANT]

```powershell
Enter-PSSession -ComputerName
```

7. Read the content of a file (Open a file) [NOTE: This example shows how to read the content of the windows firewall log file]

```powershell
Get-Content -Path "C:\WindowsSystem32logfilesfirewallpfirewall.log"
```

8. Copy and Paste Folders [NOTE: Use this command to copy an entire folder to another folder. This will copy the folder and all the sub folder/files. The -verbose command will display the results to the console.]

```powershell
Copy-Item E:\WindowsImageBackup\Exchange -Destination \\Server1\Backups\Exchange -Recursive -Verbose
```

<hr>

### Basic_Powershell_Commands -

1. Get Execution Policy

```powershell
Get-ExecutionPolicy
```

2. Set Execution Policy to Unristricted

```powershell
Set-ExecutionPolicy Unrestricted
```

3. Show Powershell Version

```powershell
$PSVersionTable
```

4. Get help for a Command

```powershell
Get-Help COMMAND_NAME
```

5. Search Get-Help [NOTE: Use this to search the help files. This is useful if you don’t know the command or want to see if one exists.]

```powershell
Get-Help *keyword*
```

6. Get Installed Modules

```powershell
Get-InstalledModules
```

7. List all available Moules

```powershell
Get-Module -ListAvailable
```

8. Export Results to CSV

```powershell
Get-ADUSer Username -Properties * | Select name,department,title | Export-CSV C:\user.csv
```

9. Display available commands

```powershell
Get-Command
```

10. Find new Module

```powershell
Find-Module *ntfs*
```

11. Install new Module [NOTE: Installs modules from https://www.powershellgallery.com/ , I found a module called NTFSSecurity, to install it I run this command]

```powershell
Install-Module NTFSSecurity
```

---


### Misc -

1. Get A List of All Office 365 Users

```powershell
Get-MsolUser | Select DisplayName,City,Department,ObjectID
```

2. Get Full mailbox details

```powershell
Get-Mailbox email-address | fl
```

3. Get Calendar Permissions

```powershell
Get-MailboxFolderPermission username:calendar
```

4. Enable Remote Mailbox (Hybrid Environment)
Use this command if you have an existing on-premise user that needs an office 365 mailbox. There are other ways to do this but this creates all the attributes in the AD account.

NOTE: Replace the username and the tenant fields

```powershell
Enable-RemoteMailbox username -RemoteRoutingAddress "username@tenant.mail.onmicrosoft.com"
```
