### Level21->Level22


```bash 
ssh -p 2220 bandit21@bandit.labs.overthewire.org
```

The level description tells you to check the `/etc/cron.d` directory to figure out what commands are being executed. 


I'm not familiar with **[crons](https://en.wikipedia.org/wiki/Cron)** so had to understand what crons are before solving the challenge. 


Basically a cron is a shell command that runs a shell script or command at periodically at a fixed time, date, or interval. 


I guess they are located in `/etc/cron.d`.


Then let's have a look at `/etc/cron.d`. 


```bash
cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```


It runs a shellscript in the background and sends the output to `/dev/null`. 


Let's check what commands the shellscript is actually executing. 


```bash 
cat /usr/bin/cronjob_bandit22.sh 
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```


It changes the permission of a directory under `/tmp` and redirects the password for `bandit22` to it.


Just reading the folder under `/tmp` will grant you the password.


```bash 
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```


If you're interested here's an explanation on why there's a `.d` at the end of `/etc/cron.d`. 


https://stackoverflow.com/questions/26333318/what-does-d-mean-in-etc-cron-d