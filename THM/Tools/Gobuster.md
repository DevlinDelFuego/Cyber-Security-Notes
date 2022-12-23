# Gobuster

Type the following command into the terminal to find potentially hidden pages on FakeBank's website using GoBuster (a command-line security application).  

GoBuster command to brute-force website pages
```bash
ubuntu@tryhackme:~/Desktop$ gobuster -u http://fakebank.com -w wordlist.txt dir  ===================================================== 
Gobuster v2.0.1 
=====================================================
[+] Mode         : dir 
[+] Url/Domain   : http://fakebank.com/ 
[+] Threads      : 10 
[+] Wordlist     : wordlist.txt 
[+] Status codes : 200,204,301,302,307,403 
[+] Timeout      : 10s 
===================================================== 
2022/04/11 18:23:28 Starting gobuster ===================================================== 
/images (Status: 301) /DIRECTORY_NAME_OUTPUT (Status: 200) ===================================================== 
2022/04/11 18:23:38 Finished 
=====================================================
```

In the command above, `-u` is used to state the website we're scanning, `-w` takes a list of words to iterate through to find hidden pages.

#Tools