OSCP A:

143 Aero:

Initial via https://github.com/b4ny4n/CVE-2020-13151.git

PE via "python /usr/bin/*asinfo* -v STATUS"  -> append py rev shell to file


144 Crystal:

Initial via .git repo on port 80
- use https://github.com/internetwache/GitTools to extract and check for secrets in the logs

PE via /opt/backup
- in sitebackup.zip there is a secret  (user chloe)
- use this secret to gain root


.145 Hermes

Initial via UDP Port 1978 -> use WifiMouse exploit

PE: check "reg query HKCU\Software\SimonTatham\PuTTY\Sessions /t REG_SZ /s"

MS01:

Initial via https://www.exploit-db.com/exploits/50801

 PE via PrintSpoofer.exe

MS02:

access via ecil-winrm as celia.almeda

PE via windows.old -> SAM and SYSTEM files

DC:

access via evil-winrm or psexec as tom_admin

OSCP B:

149 Kiero

Initial via UDP port 161  (https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp#enumerating-snmp)
- creds after commands willl be kiero:kiero -> access to ftp -> find key

PE via Dirty Cow Exploit

.150 Berlin

Initial via https://github.com/kljunowsky/CVE-2022-42889-text4shell  (https://www.youtube.com/watch?v=oTpoRW7_YbA&ab_channel=vulnmachines)

PE via https://github.com/IOActive/jdwp-shellifier


.151 Gust 

Initial via https://www.exploit-db.com/exploits/47799

PE via C:\program files\Kite\KiteService.exe


MSO1

Initial via impacket-smbserver -> catch hash (web_svc:Diamond1)
- set up route to internal network via ssh as web_svc (Special here and not as easy as in labs before... use ligolo or chisel)
- then put webshell in wwwroot on ftp and get revshell

PE: PrintSpoofer.exe
- use GetUserSPNs.py to get sql_svc:Dolphin1
- proxychains mssqlclient.py oscp.exam/sql_svc@10.10.x.148 -windows-auth
- enable_xp_cmdshell 
- revshell to MSO2

MSO2

access via sql rev shell
PE via PrintSpoofer.exe  (you have to tunnel traffic through MS01 as MS02 can´t reach kali)

post exploit: windows.old (SAM and SYSTEM)

DC

evil-winrm as tom_admin

OSCP C:

.155 Pascha:

Initial via https://github.com/blue0x1/mobilemouse-exploit/tree/main

PE via "C:\Program Files\MilleGPG5\GPGService.exe"

.156 Frankfurt:

Initial via UDP port 161 (dor
snmpwalk -c public -v1 192.168.189.156 NET-SNMP-EXTEND-MIB::nsExtendObjects)
- jack:3PUKsX98BMupBiCf
- check vesta login on port 8083 (Jack is username)
- add cron job there to gain RCE

PE via https://ssd-disclosure.com/ssd-advisory-vestacp-multiple-vulnerabilities/


.157 Charlie:

Initial via (https://www.exploit-db.com/exploits/50234) 
- cassie:cassie

PE via wildcard injection here: root cd /opt/admin && tar -zxf /tmp/backup.tar.gz *


MS01

initial via port 8000/partner/db -> find creds usable via ssh

PE: find admintool.exe -> will give you administrator:December31
- ssh as administrator

post exploit: C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt

MSO2:

access as admin via evil-winrm
- check windows.old 

DC

access as tom_admin