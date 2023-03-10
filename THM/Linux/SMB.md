# SMB

Map
```shell
smbmap -H <ip>
```

Connect
```shell
smbclient //<ip>/<share name>
```

```shell
smbclient -L \\\\<ip>\\
```

```shell
smbclient \\\\<ip>\\<share>
```

```
Usage: 
smbclient [-?EgqBNPkV] [-?|--help] [--usage] 
[-M|--message=HOST] 
[-I|--ip-address=IP] 
[-E|--stderr]
[-L|--list=HOST] 
[-T|--tar=<c|x>IXFvgbNan] 
[-D|--directory=DIR] 
[-c|--command=STRING]
[-b|--send-buffer=BYTES] 
[-t|--timeout=SECONDS] 
[-p|--port=PORT] 
[-g|--grepable] 
[-q|--quiet]
[-B|--browse] 
[-d|--debuglevel=DEBUGLEVEL] [--debug-stdout] 
[-s|--configfile=CONFIGFILE]
[--option=name=value] 
[-l|--log-basename=LOGFILEBASE] 
[--leak-report] [--leak-report-full]
[-R|--name-resolve=NAME-RESOLVE-ORDER] 
[-O|--socket-options=SOCKETOPTIONS]
[-m|--max-protocol=MAXPROTOCOL] 
[-n|--netbiosname=NETBIOSNAME] [--netbios-scope=SCOPE]
[-W|--workgroup=WORKGROUP] [--realm=REALM] 
[-U|--user=[DOMAIN/]USERNAME[%PASSWORD]] 
[-N|--no-pass]
[--password=STRING] 
[--pw-nt-hash] 
[-A|--authentication-file=FILE] 
[-P|--machine-pass]
[--simple-bind-dn=DN] 
[--use-kerberos=desired|required|off] 
[--use-krb5-ccache=CCACHE]
[--use-winbind-ccache] 
[--client-protection=sign|encrypt|off] 
[-k|--kerberos] 
[-V|--version]
[OPTIONS] service <password>

```