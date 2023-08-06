#### Security Identifier
S-R-X-Y
String is SID - revision, is always 1 - authority, usually 5 -  sub authority

```
S-1-0-0                       Nobody        
S-1-1-0	                      Everybody
S-1-5-11                      Authenticated Users
S-1-5-18                      Local System
S-1-5-domainidentifier-500    Administrator
```
Access Token
#### Mandatory Integrity Control
System
High
Medium
Low

User Account Control

### Situational Awareness

```
- Username and hostname
	Get-LocalUser
- Group memberships of the current user
	Get-LocalGroup
- Existing users and groups
	Get-LocalGroupMember adminteam
	Get-LocalGroupMember Administrators
- Operating system, version and architecture
	systeminfo
- Network information
	ipconfig /all
	route print
	netstat -ano
- Installed applications
	Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname 
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname
- Running processes
	Get-Process
```

```

```
