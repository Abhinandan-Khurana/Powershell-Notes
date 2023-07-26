# Powershell Notes
## PowerShell Cmdlets

A cmdlet is a Powershell command with a predefined function, similar to an operator in a programming language.

- There are system, custom and user cmdlets.
- Output : as an object or array of objects.
- can use pipes to get data for analysis or transfer to another cmdlet.
- Case-insensetive
- use semicolon (;) to use multiple cmdlets in single string

A cmdlet always consists of a verb, e.g.,
- **Get** - To get something
- **Set** - To define something
- **Start** - To run something
- **Stop** - To stop a running task
- **Out** - To output something
- **New** - To create something

Example - 

- **Get-Process** - Shows the processes currently running on your computer.
![[Get-Process.png]]
- **Get-Service** - Shows the list of services with their status
- **Get-Content** — Shows the content of the file you specify (for example, Get-Content C:\Windows\System32\drivers\etc\hosts)
