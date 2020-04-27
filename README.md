# WmiExec.ps1
Remote execution tools for Windows that rely only on WMI and PowerShell.

Execute console commands remotely ***and*** capture stdout/stderr streams without relying on PowerShell Remoting, WinRM or PsExec.

## Examples


[Blog post and video about this technique.](https://systemfrontier.com/blog/running-remote-commands-and-actually-getting-the-output-using-only-wmi/)

The below shows you how WmiExec can accept the command string as value from the pipeline.

```powershell
PS C:\ "Get-ChildItem C:\" | .\WmiExec.ps1 -ComputerName "hostname"
Running the below command on: SIN-L00133...
Get-ChildItem C:\
PID: 5580 - Waiting for remote command to finish...
PID: 5580 - Waiting for remote command to finish...
Result...


    Directory: C:\


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       28.06.2018     15:16                PerfLogs
d-r---       09.09.2019     15:19                Program Files
d-r---       07.10.2019     08:36                Program Files (x86)
d-r---       10.10.2019     10:51                Users
d-----       10.10.2019     16:00                Windows
```

The below shows you the object type that is returned.

```powershell
PS C:\ $result = .\WmiExec.ps1 -ComputerName "hostname" -Command "Get-ChildItem C:\"
Running the below command on: hostname...
Get-ChildItem C:\
PID: 5580 - Waiting for remote command to finish...
PID: 5580 - Waiting for remote command to finish...
Result...
PS C:\ $result.GetType()

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     True     String                                   System.Object
```

Twitter
https://twitter.com/OneScripter

Do even more cool stuff like create web GUIs for your PowerShell scripts that leverage RBAC, using System Frontier.
https://systemfrontier.com/powershell
