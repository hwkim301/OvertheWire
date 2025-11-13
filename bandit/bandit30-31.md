## Level30->Level31


```bash 
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
```


There isn't much you can do with the `README.md` file.



``` 
cat README.md 
just an epmty file... muahaha
```


Let's try some other git commands like `git log` and `git show`.


```
git log
commit d604df2303c973b8e0565c60e4c29d3801445299 (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Oct 14 09:26:28 2025 +0000
```


```
git show
commit d604df2303c973b8e0565c60e4c29d3801445299 (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Oct 14 09:26:28 2025 +0000

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..029ba42
--- /dev/null
+++ b/README.md
@@ -0,0 +1 @@
+just an epmty file... muahaha
```


Running other commands won't lead you to the password and since it's getting a bit frustrating  I'll just tell you the answer right away. 


You need to use the `git tag` command. 


What is a **git tag**? 


According to **[Reddit](https://www.reddit.com/r/git/comments/1cgt7v3/what_are_tags/)**, a tag is a label that points to a commit that doesn't move. 


```bash 
git tag
secret
```


By using the `git show` command you can get the password.


```bash 
git show secret
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```


Here's a detailed explanation on `git tag` and `git show` and how to interpret the output of `git diff`


1. git tag 


https://stackoverflow.com/questions/1457103/how-is-a-tag-different-from-a-branch-in-git-which-should-i-use-here


2. git show 


https://git-scm.com/docs/git-show


3. git diff 


https://stackoverflow.com/questions/2529441/how-to-read-the-output-from-git-diff