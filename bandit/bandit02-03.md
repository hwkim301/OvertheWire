## Level2->Level3


Login to bandit2 with the previous password. 


```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```


The password is stored in `--spaces in this filename--` which starts with `--`.


```bash 
ls
--spaces in this filename--
```


Like before, the `cat` command cannot read the file `--`.


It can't read the file `--` because, the double-dash is a standard convention in command-line interfaces to signal the end of the command-line options. 


```bash
cat --spaces in this filename--
cat: unrecognized option '--spaces'
Try 'cat --help' for more information
```


Using the relative path like we did in the previous level let's you read the file. 


You can see that the he spaces in the filename are escaped to `\`.


```bash 
cat ./--spaces\ in\ this\ filename-- 
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```