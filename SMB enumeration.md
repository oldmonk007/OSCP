
smbclient -L //10.10.11.175/
smbclient -U ' ' //10.10.11.175/Shares

crackmapexec smb 192.168.225.242 -u user.txt -p pass.txt --continue-on-success

crackmapexec smb 192.168.225.242 -u john -p "dqsTwTpZPn#nL" --shares