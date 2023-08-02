# Active Directory PowerShell Commands

## Table of Contents -

- [Active Directory Commands](#Active Directory Commands)
- [Windows Server & Client Commands](#Windows Server & Client Commands)
- [Basic Powershell Commands](#Basic Powershell Commands)
- [Misc](#Misc)


### Active Directory Commands

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
