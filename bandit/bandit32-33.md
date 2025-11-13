## Level32->Level33


Now we're back to sshing to the remote server, no more git cloning. 


```bash
ssh -p 2220 bandit32@bandit.labs.overthewire.org
```


This time the shell is an uppercase shell that interprets all the commands as CAPs.


```bash
WELCOME TO THE UPPERCASE SHELL
>> 
```


Since the shell transforms all the commands to capitals we can't use the uppercase shell.


```bash
>> cat /etc/bandit_pass/bandit32
sh: 1: CAT: Permission denied
```


In shell scripting we can use the `$0` variable to invoke the default shell. 


https://unix.stackexchange.com/questions/280454/what-is-the-meaning-of-0-in-the-bash-shell


You can see how executing `$0` gave us a `$` sign. 


```bash
>> $0
$ 
```

The default shell bandit uses is the Bourne Shell. 


```bash
echo $0
sh
```


Since our `uid` is `bandit33` we have the permissions to read the password for `bandit33`. 


```bash
$ id
uid=11033(bandit33) gid=11032(bandit32) groups=11032(bandit32)
```


```bash
cat /etc/bandit_pass/bandit33
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```
