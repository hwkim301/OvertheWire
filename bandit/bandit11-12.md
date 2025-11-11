## Level11-> Level12

Login to `bandit11` with the previous password. 


```bash 
ssh -p 2220 bandit11@bandit.labs.overthewire.org
```

Since all lowercase and uppercase have been rotated by 13 positions we need to rotated it back again by 13 positions. 


Most people refer this as **[ROT-13](https://en.wikipedia.org/wiki/ROT13)**.


```bash
cat data.txt 
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```


The `tr` command(transliterate) in linux has the feature to change characters. 


`A-M` and `a-m` become `N-Z` and `n-z` but Just be careful that `N-Z` and `n-z` need to be rotated back to `A-M` and `a-m`. 


That's why theres an extra `A-M` and `a-m` at the end.


```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```