### Level9-> Level10

Login to `bandit9` with the previous password. 


```bash 
ssh -p 2220 bandit9@bandit.labs.overthewire.org
```

This time you need to find one of the human-readable strings that start with `"="` in `data.txt`. 


```bash
file data.txt 
data.txt: data
```


The `strings` command shows the strings in a file. 


You can run `strings` on `data.txt` and then use `grep "="` with a pipe to capture strings that start with `"="`. 



```bash
strings data.txt | grep "="
FB`=
c\5D=
========== the
?/=l
=Uc1
=vG*2P
========== password
k=ezG
E========== is
=%r_
.?=Dm
O&A=n
5========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
=*^Y
=L3jT
q<=,
'QHE=
+=NBf
```

It looks like `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey` is the password.