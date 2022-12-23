# OSINT

There are also external resources available that can help in discovering information about your target website; these resources are often referred to as OSINT or (Open-Source Intelligence) as they're freely available tools that collect information:

## Google Hacking / Dorking

Google hacking / Dorking utilizes Google's advanced search engine features, which allow you to pick out custom content. You can, for instance, pick out results from a certain domain name using the **site:** filter, for example `(site:tryhackme.com)` you can then match this up with certain search terms, say, for example, the word admin `(site:tryhackme.com admin)` this then would only return results from the `tryhackme.com` website which contain the word admin in its content. You can combine multiple filters as well. Here is an example of more filters you can use:

|Filter|Example|Description|
|------------ | ------------| ------------|
|site|site:tryhackme.com|returns results only from the specified website address|  
|inurl|inurl:admin|returns results that have the specified word in the URL| 
|filetype|filetype:pdf|returns results which are a particular file extension|
|intitle|intitle:admin|returns results that contain the specified word in the title|

Go to [Google](https://www.google.com/) and use the search term `-site:www.tryhackme.com  site:*.tryhackme.com`, which should reveal a subdomain for tryhackme.com; use that subdomain to answer the question below.

More information about google hacking can be found here: [https://en.wikipedia.org/wiki/Google_hacking](https://en.wikipedia.org/wiki/Google_hacking)

## Wappalyzer

Wappalyzer (https://www.wappalyzer.com/) is an online tool and browser extension that helps identify what technologies a website uses, such as frameworks, Content Management Systems (CMS), payment processors and much more, and it can even find version numbers as well.

## Wayback Machine

The Wayback Machine (https://archive.org/web/) is a historical archive of websites that dates back to the late 90s. You can search a domain name, and it will show you all the times the service scraped the web page and saved the contents. This service can help uncover old pages that may still be active on the current website.

## GitHub

To understand GitHub, you first need to understand Git. Git is a version control system that tracks changes to files in a project. Working in a team is easier because you can see what each team member is editing and what changes they made to files. When users have finished making their changes, they commit them with a message and then push them back to a central location (repository) for the other users to then pull those changes to their local machines. GitHub is a hosted version of Git on the internet. Repositories can either be set to public or private and have various access controls. You can use GitHub's search feature to look for company names or website names to try and locate repositories belonging to your target. Once discovered, you may have access to source code, passwords or other content that you hadn't yet found.

## S3 Buckets
S3 Buckets are a storage service provided by Amazon AWS, allowing people to save files and even static website content in the cloud accessible over HTTP and HTTPS. The owner of the files can set access permissions to either make files public, private and even writable. Sometimes these access permissions are incorrectly set and inadvertently allow access to files that shouldn't be available to the public. The format of the S3 buckets is http(s)://{name}.s3.amazonaws.com where {name} is decided by the owner, such as tryhackme-assets.s3.amazonaws.com. S3 buckets can be discovered in many ways, such as finding the URLs in the website's page source, GitHub repositories, or even automating the process. One common automation method is by using the company name followed by common terms such as {name}-assets, {name}-www, {name}-public, {name}-private, etc.

## What are wordlists?

Wordlists are just text files that contain a long list of commonly used words; they can cover many different use cases. For example, a password wordlist would include the most frequently used passwords, whereas we're looking for content in our case, so we'd require a list containing the most commonly used directory and file names. An excellent resource for wordlists that is preinstalled on the THM AttackBox is [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) which Daniel Miessler curates.


## Automation Tools

Although there are many different content discovery tools available, all with their features and flaws, we're going to cover three which are preinstalled on our attack box, ffuf, dirb and gobuster.


On the AttackBox execute the following three commands, targeting the Acme IT Support website and see what results you get.


### Using ffuf:
``` shell   
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://MACHINE_IP/FUZZ   
```  

### Using dirb:
```shell   
user@machine$ dirb http://MACHINE_IP/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
``` 

### Using Gobuster:
```shell 
user@machine$ gobuster dir --url http://MACHINE_IP/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

### Using Sublist3r:
```shell 
user@thm:~$ ./sublist3r.py -d acmeitsupport.thm
```


#osint #tools #web