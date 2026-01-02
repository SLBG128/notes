# enumeration pre pen-testing
What to do in the begining of a pen-test

## Port Scanning
### nmap general
``` bash
nmap -sC -sV <target-url> -oN <output file>
```

### another example
```bash
nmap -A -v <target-url> -oN <output file>
```

### in case there are hidden ports like greater than 1000
``` bash
nmap -sC -sV <target-url> -oN <output file>
```
#### Syntax
- sC: Use default scripts when scanning
- sV: Discover what service is the port serving
- -A: Do whatever nmap can do
- -P-: Scan for all ports 1-65535, or use "," to specify port
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

### Faster Alternative: fuff 
``` bash
fuff -u <target-url> -w <path to wordlist>
```
> Note: "FUZZ" is used to specify where to brute force

### Alternative B: scan for parameter for .php like ?=
``` bash
dirsearch -u <target-url>
```

## Advance auto-scan
### nikto
``` bash
nikto -h "<target-url>"
```
Note: "http://" must be supplied
