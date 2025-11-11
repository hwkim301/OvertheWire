### Level1->Level2

This time we login to bandit1 using `ssh` with the previous password 


```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```


There is a file named `-`, it's a dash.


```bash 
ls
-
```


I tried reading the file `-` with `cat -`, but it just hangs until it receives some keyboard input.  


The reason the `-` waits for keyboard input is because the hyphen acts as a special filename telling `cat` to read from its stdin, and not from a file on disk. 


Since there isn't any pipe feeding data, it waits until you type something from your keyboard.


However using the relative path to specify the filename let's you read the file.


```bash 
cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```