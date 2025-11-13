## Level25->Level26


```bash 
ssh -p 2220 bandit25@bandit.labs.overthewire.org
```

A sshkeyfile (bandit26.sshkey) is given, since we can't `ssh` from the bandit itself we need to copy the ssh key locally 
then ssh.  


Change the permissions for the ssh key or else you'll get complaints from bandit. 


Bandit will nag you for giving way too much permission for the ssh key file. 


```bash
chmod 400 bandit26.sshkey
```


`ssh` into `bandit26` using the ssh key.


```bash 
ssh -p 2220 -i bandit26.sshkey bandit26@bandit.labs.overthewire.org
```

For some reason, bandit automatically closes the connection when you `ssh` into it. 


Since it constantly blocks us from sshing let's try `bandit25` instead. 


```bash 
ssh -p 2220 bandit25@bandit.labs.overthewire.org
```


The command below shows what the default shell is when we login.


Unlike `bandit25`, `bandit26` doesn't use `bash` it uses something else showtext `(/usr/bin/showtext)`. 


```bash 
cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext

cat /etc/passwd | grep bandit25
bandit25:x:11025:11025:bandit level 25:/home/bandit25:/bin/bash
```


Let's check out what this `showtext` is.


It's running a custom shellscript by loading `text.txt` and exporting it as a custom shell.


When using the `more` command it only shows a tiny part of the shell, that's why it probably didn't show the full terminal.


```bash 
cat /usr/bin/showtext 
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```


So in order for the `more` command to show the output on your terminal, resize your terminal and make it really small.


Now when the shell is running the `more` command, type `v` this will invoke `vim`. 


Now that we are running `vim` we can then type `:set shell=/bin/bash`, and this will set the system's shell to `bash`.


Then type `:shell` in `vim`, this will open the default shell on the Linux machine. 


Let's check the `uid` or the user, you can check that it's `bandit26`. 


```bash 
id
uid=11026(bandit26) gid=11026(bandit26) groups=11026(bandit26)
```


Since the `uid` or `RUID` is `bandit26` we can read the password for `bandit26`. 


```bash 
cat /etc/bandit_pass/bandit26
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ

echo $0
/bin/bash
```


You can check which shell the system is using via the shell variable `$0`.