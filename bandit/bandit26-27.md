## Level26->Level27

Another setuid binary is given again.


```bash 
file bandit27-do 
bandit27-do: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=35d353cf6d732f515a73f50ed205265fe1e68f90, for GNU/Linux 3.2.0, not stripped
```


```bash
ls -al bandit27-do 
-rwsr-x--- 1 bandit27 bandit26 14884 Oct 14 09:26 bandit27-do
```


Pretty similar to [level19](https://github.com/hwkim301/OvertheWire/blob/master/bandit/bandit19-20.md).


```
./bandit27-do cat /etc/bandit_pass/bandit27
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```
