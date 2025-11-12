### Level22->Level23


```bash 
ssh -p 2220 bandit21@bandit.labs.overthewire.org
```


The description tells us to check the `/etc/cron.d` directory again. 


```bash
cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```


Here's the shellscript. 


```bash
cat /usr/bin/cronjob_bandit23.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```


In order to understand the shellscript you need to know what the variable `whoami`, `myname` and `mytarget` is. 


Then you'll be able to get the password since it redirects it using `cat`.


The `whoami` command returns who you're logged in as, we are currently `bandit22` but, since we want to get the password of `bandit23`. 


It would be a good idea to set myname to `bandit23`.


The intimidating part is figuring out the value of `mytarget` because it pipes stuff twice with `md5sum` and the `cut` command. 


The thing is you don't have to understand each command, although it's best to understand.


We can just substitute `bandit23` to myname. 


```bash 
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```

Since the value of `mytarget` is the directory under `/tmp` that holds the password we can read it with `cat`. 


```bash 
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```


When I first solved this level I got stuck, I though passing `bandit22` would give me the password since my username is `bandit22`. 
