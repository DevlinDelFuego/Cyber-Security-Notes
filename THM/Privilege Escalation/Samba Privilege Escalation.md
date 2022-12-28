# Samba Privilege Escalation

Nmap has the ability to run to automate a wide variety of networking tasks. There is a script to enumerate shares!

```shell
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.10.10
```

On most distributions of Linux smbclient is already installed. Lets inspect one of the shares.

```shell
smbclient //<ip>/anonymous
```

You can recursively download the SMB share too. Submit the username and password as nothing.

```shell
smbget -R smb://<ip>/anonymous
```

In our case, port 111 is access to a network file system. Lets use nmap to enumerate this.

```shell
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.10.10
```

