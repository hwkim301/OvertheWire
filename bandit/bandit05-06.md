### Level5-> Level6


Login to `bandit5` with the previous password. 


```bash 
ssh -p 2220 bandit5@bandit.labs.overthewire.org
```

This time you need to find a file that's human readable, `1033` bytes in size and not executable in the `inhere` directory. 


Yikes, there's a lot of directories. 


Manually inspecting each file seems like a nightmare. 


```bash
cd inhere/ 
ls
maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
```


I'll give the answer to the problem right away, because this one's a bit hard. LOL


```bash
find -type f ! -executable -size 1033c
```


You can use the `find` command with `-type f` to specify only files, `! -executable` to select non executable files, and `-size 1033c` to select files that are exactly `1033` bytes.


If you pass a `-` in front of 1033c you will select files smaller or equal to `1033` so do not pass a dash before `1033`.


```bash 
find -type f ! -executable -size 1033c
./maybehere07/.file2
```


Found the password. 

```bash 
cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```


I got the password but I didn't use one of the clues from the website that the file was human-readable. 


Well to use that information you can run `file` right after the command above. 


By passing the `-exec file {} + ` it will run the `file` command on the file. 


```bash 
find -type f ! -executable -size 1033c -exec file {} + | grep ASCII 
./maybehere07/.file2: ASCII text, with very long lines (1000)
```