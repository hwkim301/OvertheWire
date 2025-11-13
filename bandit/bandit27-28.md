## Level27->Level28


From Level27 you need to `git clone` the remote repository using `ssh`. 


I've never used `git clone` with `ssh` before so it was a bit tricky for especially, I had some trouble where to write the port number. 


```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

When cloning the remote repository locally, you'll find a directory named `repo`.


Inside it is a `README` file. 


Let's see the contents of the `README` file using `cat`. 


```bash
cat README 
The password to the next level is: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```