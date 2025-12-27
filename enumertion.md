# enumeration pre pen-testing

## Port Scanning
### nmap general
``` bash
nmap -sC -sV <target-url> -oN <output file>
```

### in case there are hidden ports like greater than 1000
``` bash
nmap -sC -sV <target-url> -oN <output file>
```

## Web Directory Scanning
### gobuster cuz I like it
``` bash
gobuster dir -u <target-url> -w <path to wordlist>
```
*my wordlist = /opt/wordlists/dirbuster/directory-list-2.3-medium.txt

### IF: scan for parameter for .php like ?=
``` bash
dirsearch -u <target-url>
```

## Advance auto-scan
### nikto
``` bash
nikto -h "<target-url>"
```
Note: "http://" must be supplied
