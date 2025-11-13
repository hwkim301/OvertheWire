## Level7-> Level8

Login to `bandit7` with the previous password. 


```bash 
ssh -p 2220 bandit7@bandit.labs.overthewire.org
```


This time the password is in `data.txt` next to the word millionth. 


A simple `grep` command will magically show you the password.


```bash 
cat data.txt | grep millionth
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
