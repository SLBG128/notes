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
#### Syntax
- sC: Use default scripts when scanning
- sV: Discover what service is the port serving
- -P-: Scan for all ports 1-65535
- -v: verbose mode
- -vv: verboser verbose mode

## Web Directory Scanning
### gobuster cuz I like it
``` bash
gobuster dir -u <target-url> -w <path to wordlist>
```
*my wordlist = /opt/wordlists/dirbuster/directory-list-2.3-medium.txt
#### Syntax
- dir: directory mode
- -u: target url
- -w: wordlist
- -x: extension

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
