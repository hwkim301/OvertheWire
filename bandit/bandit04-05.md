### Level4-> Level5

Login to `bandit4` with the previous password. 


```bash 
ls
inhere
```


It's almost identical to the previous level, but in this level you need to find the only human-readable file. 


Out of the 9 files only one of them is an ASCII text file and the rest are binaries. 


```bash
cd inhere/
ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```


You can check the type of a file using the `file` command. 


At first I passed 9 arguments to the `file` command to manually inspect which one was the imposter, but typing all of the file names made my hands hurt a bit. 


Plus I needed to type `./` since the files started with a dash. 


```bash
file ./-file00 ./-file01 ./-file02 ./-file03 ./-file04 ./-file05 ./-file06 ./-file07 ./-file08 ./-file09
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```


```bash
cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```


I think it's perfectly fine to get the password like this, but I wondered if there were any better ways and found this. 


https://stackoverflow.com/questions/9806944/grep-only-text-files 


With the grep `-r` recursively `-I`(ignore binary) option you don't need to manually inspect all 9 files sweet!


```bash
grep -rI .
-file07:4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```