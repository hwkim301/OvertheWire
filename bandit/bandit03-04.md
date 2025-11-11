### Level3-> Level4

Login to `bandit3` with the previous password. 


```bash 
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```


The password is in a hidden file inside the `inhere` directory. 


```bash
ls
inhere
```


Just running `ls` without any options will not show you the hidden files, but passing the `ls -l` option will. 


```bash
cd inhere/

ls -al
total 12
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 14 09:26 ...Hiding-From-You
```

This looks like the password `file ...Hiding-From-You`

```
cat ...Hiding-From-You 
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ