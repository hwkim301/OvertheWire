## Level6-> Level7


Login to `bandit6` with the previous password. 


```bash 
ssh -p 2220 bandit6@bandit.labs.overthewire.org
```


This level wants you to locate a file somewhere on the server that is owned by user `bandit7`, owned by group `bandit 6` and is `33` bytes in size. 


I'll give the answer to the problem right away, because this one is even harder than the last level.  


You'll need to search the entire root file system(`/`).


By passing `-user` and `-group` we can specify which user and group owns the file.


However, when running the command  below you'll probably get a whole bunch of errors saying permission denied. 


The command seems to be legit, but somehow it just continuously spits out errors. 


```bash
find / -type f -user bandit7 -group bandit6 -size 33c
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
...
```


Since there are so many `Permission denied` we need to filter them. 


One way of filtering these errors is to redirect them to a trash-can.


Linux systems typically refer `/dev/null` as their trash can. 


An important part when redirecting is that there shouldn't be any spaces between the `fd` and the redirection operator(`>`). 


```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2> /dev/null
/var/lib/dpkg/info/bandit7.password
```


```bash
cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```
