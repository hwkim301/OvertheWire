First you need to connect with `ssh`. 


Here's what the man page description for `ssh` is .


```
DESCRIPTION
ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine.  It is intended  to  pro‐
vide  secure  encrypted  communications  between  two untrusted hosts over an insecure network.  X11 connections, arbitrary TCP ports and
Unix-domain sockets can also be forwarded over the secure channel.

ssh connects and logs into the specified  destination,  which  may  be  specified  as  either  [user@]hostname  or  a  URI  of  the  form
ssh://[user@]hostname[:port].  The user must prove their identity to the remote machine using one of several methods (see below).

If  a command is specified, it will be executed on the remote host instead of a login shell.  A complete command line may be specified as
command, or it may have additional arguments.  If supplied, the arguments will be appended to the command, separated by spaces, before it
is sent to the server to be executed.
```


In short it allows you to connect to other remote computers.


When you `ssh` to the remote machine it, you need to enter the password for this level(bandit0).


The `-p` in `ssh` means port. So were connecting to port number 2220. 


```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org

backend: gibson-0
bandit0@bandit.labs.overthewire.org's password: 
```


Entering the password will take you to the next level.