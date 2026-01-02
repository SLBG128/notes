# Smol
> Author: W.

``` bash
export IP=10.48.174.120
```

## nmap port scan
``` bash
nmap -A -v 10.48.174.120 -oN nmap.log  
```
> Discovered open port at 22 and 80  

Note that the website redirects to www.smol.thm  
So we add 'www.smol.thm' to /etc/hosts

## web directory enumeration
``` bash
ffuf -w /opt/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://www.smol.thm/FUZZ  
```

We discovered some wordpress related directory, just like how the question stated, it is operated in wp  
Lets hop over to /wp-admin/ to see any fun stuff :3

## /wp-admin/
By pure luck and knowledge, I guessed admin as the username and it indeed is a valid username
```
Error: The password you entered for the username admin is incorrect. Lost your password?
```
> Good practice: never disclose too much information in login failure error message

### wp-scan time
``` bash 

```


-----

Q1: What is the user flag
```

```

Q2: What is the root flag
```

```