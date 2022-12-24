# Common Linux Commands

| Command | Description |Usage|
|------------ | ------------|------------|
| echo | Output any text that we provide |`echo "Hello Friend!"`|
| whoami | Find out what user we're currently logged in as! |`whoami`|
|ls|listing|`ls -lah`|
|cd |change directory|`cd ..`|
|cat |concatenate|`cat file.txt`|
|pwd |print working directory|`pwd`|
|find|find a file by name|`find -name *.txt`|
|grep|search file contents|`grep "10.10.10.10" file.txt`|
|ssh|secure shell |`ssh username@MACHINE_IP`|
|touch|Create file|`touch file.txt`|
|mkdir|Create a folder|`mkdir pics`|
|cp| copy a file or folder|`cp file.txt file1.txt`|
|mv|move a file or folder|`mv file.txt /home/file.txt`|
|rm|Remove a file or folder|`rm file.txt`|
|su|Switch users|`su user2`|
|nano/vim|Terminal text editors|`nano file.txt`|
|wget/curl|Download files|`wget http://127.0.0.1:8000/file.txt`|
|SCP|Copy files over ssh|`scp file.txt linux@10.10.10.10:/home` or `scp linux@192.168.1.30:/home/file.txt file.txt`| 
|HTTPServer|Serve the files in the directory|`python3 -m  http.server <PORT>`
|ps|View running processes|`ps aux`|
|kill|Kill a running proccess|`kill <ID>`|
|systemctl|Interact with the systemd process/daemon|`systemctl [option] [service]` `Start Stop Enable Disable`|
|ifconfig|Show network address settings|`ifconfig`|

# Operators

|Symbol / Operator|Description|
|------------| ------------|
|&|This operator allows you to run commands in the background of your terminal|
|&& |This operator allows you to combine multiple commands together in one line of your terminal|
|>|This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere|
|>>|This operator does the same function of the `>` operator but appends the output rather than replacing (meaning nothing is overwritten)|

Find Linux OS

`cat /etc/os-release`
`lsb_release -a`
`hostnamect`

Type the following command to find Linux kernel version:
`uname -r`



#commands