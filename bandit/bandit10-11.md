### Level0-> Level11

Login to `bandit10` with the previous password. 


```bash 
ssh -p 2220 bandit10@bandit.labs.overthewire.org
```


The password is in `data.txt`, but it's `base64` encoded. 


What is base64 encoding? 


**[Base64]**(https://en.wikipedia.org/wiki/Base64) is a binary-text encoding that uses 64 characters a-z(26), A-Z(26), 0-9(10), '+', '/'  to encode data.


People use base64 encoding a lot to transmit binary data in text form. 


Most shells support the base64 command.


We can `base64` decode it then. 


The `-d` in `base64` stands for decode. 


```bash
cat data.txt | base64 -d 
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```