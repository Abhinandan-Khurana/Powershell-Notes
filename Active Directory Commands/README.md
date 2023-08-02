# Active Directory PowerShell Commands

## Table of Contents -

- [Active Directory Commands](#Active_Directory_Commands)
- [Windows Server & Client Commands](#Windows_Server_&_Client_Commands)
- [Basic Powershell Commands](#Basic_Powershell_Commands)
- [Misc](#Misc)


### Active_Directory_Commands

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

#### AD User Commands

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

#### AD Group Commands

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

#### AD Computer Commands

25. Get All Computers

```powershell
Get-ADComputer -Filter *
```
