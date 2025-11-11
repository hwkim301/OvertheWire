### Level8-> Level9


Login to `bandit8` with the previous password. 


```bash 
ssh -p 2220 bandit7@bandit.labs.overthewire.org
```


The password is in `data.txt`, and it's the only line of text that's unique in `data.txt`. 


The `sort` command will alphabetically sort the duplicates and then piping the result to the `uniq` will print the unique password.


`uniq -u` only prints unique lines.


```bash 
sort data.txt | uniq -u 
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```