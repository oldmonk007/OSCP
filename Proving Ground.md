### 8,9
- [x] helpdesk
- Direct exploit for manageengine in metasploit
- [ ] hetemit
- [ ] apex
- [x] xposedapi
- [x] reconstruction
- [x] slort
- [x] payday
- [x] uc404

### 10,11
- [ ] butch
- [ ] hepet
- [ ] hawat
- [ ] pebbles
- [ ] megavolt

### 12,13
- [ ] kevin
- [ ] shifty
- [ ] twiggy

### 14,15
- [ ] authby
- [ ] nickel
- [ ] phobos

### 16,17
- [ ] morbo
- [ ] nibbles
- [ ] billyboss
- [ ] escape

### 18
- [ ] nukem

### 19,20
- [ ] splodge
- [ ] internal
- [ ] wombo

### tre

found poprt 80 and 8082
gobuster 80 with common gace nothing except cms
gobuster with big gave mantis and adminer
gobuster on mantis gave config in which a.txt was present and mysql password was present
logged into mysql with this password and in user table got password of tre
ssh with tre got shell
no suid or sudo -l
one file writeable /usr/bin/check-system
wrote chmod +s /usr/bin/bash
restarted sudo shutdown -r now
/usr/bin/bash -p gave root shell




