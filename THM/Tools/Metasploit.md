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

If you run a Nmap scan using the `db_nmap` shown below, all results will be saved to the database.








#tools #metasploit