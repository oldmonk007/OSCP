```
ssh2john id_rsa > ssh.hash
```
add  \[List.Rules:sshRules] at starting of rules file

sudo sh -c 'cat /home/kali/passwordattacks/ssh.rule >> /etc/john/john.conf'

john --wordlist=ssh.passwords --rules=sshRules ssh.hash
