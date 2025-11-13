## Level19->Level20


Login to `bandit19` with the previous password. 


```bash 
ssh -p 2220 bandit19@bandit.labs.overthewire.org
```

Now you'll need to use a `setuid` binary to read the password.


```bash 
ls -al bandit20-do 
-rwsr-x--- 1 bandit20 bandit19 14884 Oct 14 09:26 bandit20-do

./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do whoami
```


What is setuid?


Recall the fact that Linux has 3 groups? specifically user, group and others. 


The permission for the `bandit20-do` binary looks like this.


```bash 
-rwsr-x--- 1 bandit20 bandit19 14884 Oct 14 09:26 bandit20-do
```


`bandit20` is the owner, it can read, write to the file. 


But it has the setuid bit (s) set. 


Our goal is to read `/etc/bandit_pass/bandit20`. 


However `bandit20` is the only user other than root that has permission to read the file.


```bash
ls -al /etc/bandit_pass/bandit20
-r-------- 1 bandit20 bandit20 33 Oct 14 09:25 /etc/bandit_pass/bandit20
```


Sadly we are `bandit19`, which makes it impossible to read `/etc/bandit_pass/bandit20`. 


```bash
id
uid=11019(bandit19) gid=11019(bandit19) groups=11019(bandit19)
```


To read `/etc/bandit_pass/bandit20` we need the have the uid of `bandit20`. 


There isn't a way to set the `uid` to `bandit20`, however when a setuid bit is set, *nix systems elevate privileges so that even though we don't have the `uid` of `bandit20` it allows us to have privileges of the program's owner (bandit20). 


The `uid` when you run the command id is called **RUID**(Real User ID), you get this `uid` when you login to your *nix system. 


Also if a setuid bit isn't set this never changes. 


However when you run a setuid binary the process changes its **EUID**(Effective User ID) which was the same as **RUID**(bandit19) to the owner of the special binary executable, which in our case is `bandit20`.


Therefore if we use the setuid binary we can read `/etc/bandit_pass/bandit20` as if we are `bandit20` although we aren't.


```bash
./bandit20-do cat /etc/bandit_pass/bandit20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```


Setuid, especially **setuid(0)** is used a lot, because since `0` is the `uid` for `root`, running a setuid(0) file grants us escalated privileges as if we were root although we're not, which can cause some damage to the system by tinkering on files only root should have permission to.


Read the posts below to get a better understanding and personally understanding uid,ruid,euid and stuff like these are hard. 


Barely any Linux books explain it. 


https://unix.stackexchange.com/questions/191940/difference-between-owner-root-and-ruid-euid

https://stackoverflow.com/questions/32455684/difference-between-real-user-id-effective-user-id-and-saved-user-id
