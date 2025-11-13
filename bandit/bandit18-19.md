## Level18->Level19


Fore some reason, you can't login to `bandit18` with the previous password. 


```bash 
ssh -p 2220 bandit18@bandit.labs.overthewire.org
```

Someone modified the `.bashrc` file which logs us out when we try to `ssh`. 


If you've never heard of `.bashrc` before read the posts below.


1. 

https://unix.stackexchange.com/questions/129143/what-is-the-purpose-of-bashrc-and-how-does-it-work 


2. 

https://www.reddit.com/r/archlinux/comments/i95ssb/what_exactly_is_bashrc_in_the_home_directory/


Here's the man page for `ssh`. 


You can use the `-t` option in `ssh` to specify a shell. 


``` 
-t Force  pseudo-terminal allocation.  This can be used to execute arbitrary screen-based programs on a remote machine, which can be very useful, e.g. when implementing menu services.  Multiple -t options force tty allocation, even if ssh has no local tty.
```


I logged in using the **[Bourne Shell](https://en.wikipedia.org/wiki/Bourne_shell)** because the shell is found on pretty much any *nix machine. 


```bash
ssh -p 2220 bandit18@bandit.labs.overthewire.org -t "/bin/sh"
```


Now we have logged in as `bandit18`.


```bash
id
uid=11018(bandit18) gid=11018(bandit18) groups=11018(bandit18)
```


The password is in the `readme` file. 


```bash
cat readme
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```