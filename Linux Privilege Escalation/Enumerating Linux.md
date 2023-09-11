### File and User Privileges

everything is a file
3 categories user - owner, owner group, others group

### Manual Enumeration

**user context**
id
root id = 0
userid starts from 1000
/usr/sbin/nologin to block any remote or local login for service accounts

hostname

sudo permissions 
sudo -l

**OS release and version**

cat /etc/issue
cat /etc/os-release
uname -a

**Processes**

ps
ps aux

**Network Info**

ip a 
route
routel
netstat -anp
ss -anp

**Firewall**
cat /etc/iptables/rules.v4

**Scheduled Tasks**

ls -lah /etc/cron*
crontab -l

**Installed Applications**

dpkg -l

**Files with weak permissions**

find / -writable -type d 2>/dev/null
find / -writable -type f 2>/dev/null
find / -writable -type f 2>/dev/null -not -path "/var/www/*" -not -path "/proc/*"


**Mounted Drives**
cat /etc/fstab
mount

**Available Disks**

lsblk

**Kernel Modules**

lsmod
/sbin/modinfo libata

**setuid and setgid**
file runs with privileges of owner
find / -perm -u=s -type f 2>/dev/null


### Automated Enumeration

unix-privsec-check
LinEnum
LinPeas
