### Level0-> Level11

Login to `bandit10` with the previous password. 


```bash 
ssh -p 2220 bandit10@bandit.labs.overthewire.org
```


The password is in `data.txt`, but it's `base64` encoded. 


We can `base64` decode it then. 


The `-d` in `base64` stands for decode. 


```bash
cat data.txt | base64 -d 
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```