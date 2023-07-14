### Nmap Scanning

- sudo nmap -sS 192.168.50.149
- nmap -sT 192.168.50.149
- sudo nmap -sU 192.168.50.149
- nmap -sn 192.168.50.1-253
- nmap -v -sn 192.168.50.1-253 -oG ping-sweep.txt
- grep Up ping-sweep.txt | cut -d " " -f 2
- nmap -p 80 192.168.50.1-253 -oG web-sweep.txt
- grep open web-sweep.txt | cut -d" " -f2
- nmap -sT -A --top-ports=20 192.168.50.1-253 -oG top-port-sweep.txt
- nmap --script http-headers 192.168.50.6   #/usr/share/nmap/scripts 
- nmap --script-help http-headers

### Powershell scanning

- Test-NetConnection -Port 445 192.168.50.151
```
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null
```
