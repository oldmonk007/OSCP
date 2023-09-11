Rinse and Repeat

net user /domain
net user jeffadmin /domain
net group /domain
net group "Sales Department" /domain

```
LDAP://HostName[:PortNumber][/DistinguishedName]
```

```
Distinguished Name
CN=Stephanie,CN=Users,DC=corp,DC=com
```

```
function LDAPSearch {
    param (
        [string]$LDAPQuery
    )


# Store the domain object in the $domainObj variable
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

# Store the PdcRoleOwner name to the $PDC variable
$PDC = $domainObj.PdcRoleOwner.Name

# Store the Distinguished Name variable into the $DN variable
$DN = ([adsi]'').distinguishedName

$LDAP = "LDAP://$PDC/$DN"

$direntry = New-Object System.DirectoryServices.DirectoryEntry($LDAP)

#$dirsearcher = New-Object System.DirectoryServices.DirectorySearcher($direntry)

$dirsearcher = New-Object System.DirectoryServices.DirectorySearcher($direntry, $LDAPQuery)

return $dirsearcher.FindAll()

}
<#
#Filter for users
$dirsearcher.filter="samAccountType=805306368"

#$dirsearcher.FindAll()

$result = $dirsearcher.FindAll()

Foreach($obj in $result)
{
    Foreach($prop in $obj.Properties)
    {
        $prop
    }

    Write-Host "-------------------------------"
}

#>

LDAPSearch -LDAPQuery "(samAccountType=805306368)"
LDAPSearch -LDAPQuery "(objectclass=group)"

foreach ($group in $(LDAPSearch -LDAPQuery "(objectCategory=group)")) {$group.properties | select {$_.cn}, {$_.member}}

$sales = LDAPSearch -LDAPQuery "(&(objectCategory=group)(cn=Sales Department))"

$sales.properties.member
```

### Powerview

Import-Module .\PowerView.ps1
Get-NetDomain
Get-NetUser
Get-NetUser | select cn
Get-NetUser | select cn,pwdlastset,lastlogon
Get-NetGroup | select cn
Get-NetGroup "Sales Department" | select member
Get-NetComputer
Find-LocalAdminAccess
Get-NetSession -ComputerName files04 -Verbose


.\PsLoggedon.exe \\files04

### Service Principal Names

setspn -L iis_service
Get-NetUser -SPN | select samaccountname,serviceprincipalname

### Object Permissions

Get-ObjectAcl -Identity stephanie
Convert-SidToName S-1-5-21-1987370270-658905905-1781884369-1104

Get-ObjectAcl -Identity "Management Department" | ? {$_.ActiveDirectoryRights -eq "GenericAll"} | select SecurityIdentifier,ActiveDirectoryRights

Get-ObjectAcl | ? {$_.ActiveDirectoryRights -eq "GenericAll"} | ? {$_.SecurityIdentifier -eq "S-1-5-21-976142013-3766213998-138799841-1109"}
### Domain Shares

Find-DomainShare

ls \\FILES04\docshare\docs\do-not-share

### Automated Enumeration

PingCastle
BloodHound

Import-Module .\SharpHound.ps1
Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\Users\stephanie\Desktop\ -OutputPrefix "corp audit"

neo4j start

```
match (a) -[r] -> () delete a, r

match (a) delete a
```
