# Gobuster

Download GoBuster [here](https://github.com/OJ/gobuster), or if you're on Kali Linux 2020.1+ run sudo apt-get install gobuster

To get started, you will need a wordlist for GoBuster (which will be used to quickly go through the wordlist to identify if there is a public directory available. If you are using [Kali Linux](https://tryhackme.com/room/kali) you can find many wordlists under `/usr/share/wordlists`.

```shell
gobuster dir -u http://<ip>:3333 -w <word list location>
```

| GoBuster            | Description                               |
| ------------------- | ----------------------------------------- |
| `-e`                | Print the full URLs in your console       |
| `-u`                | The target URL                            |
| `-w`                | Path to your wordlist                     |
| `-U and -P`         | Username and Password for Basic Auth      |
| `-p <x>`            | Proxy to use for requests                 |
| `-c <http cookies>` | Specify a cookie for simulating your auth |

```shell
gobuster dir -u http://10.10.10.10 -q -w /usr/share/wordlists/dirb/big.txt -t 250 -x txt,php,html,cgl,js,py,sh,css

```

```shell
gobuster dir -u http://10.10.85.55:49663  -q -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 250 
```








#tools