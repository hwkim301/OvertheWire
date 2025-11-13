## Level31->Level32


```bash 
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
```


Here's the `README` file, according to the `README` file we need to `git push` to the remote repository. 


```
cat README.md 
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```


You need to push the `key.txt` and the content of the `key.txt` should be `'May I come in?'`.


```bash 
echo 'May I come in?' > key.txt
```


To upload a file to a remote repository the following steps are the usual procedure. 


1. git add 


The `git add` command sends files to the staging area. 


2. git commit 


The `git commit` command permanently store changes made to the files we selected using git add as a node in the git tree.


3. git push 


The `git push` command copies the local commits that do not exist in the remote repository to the remoe repository.


https://www.reddit.com/r/learnprogramming/comments/6g3eja/what_are_git_add_and_git_commit_doing_and_how_are/

https://stackoverflow.com/questions/26005031/what-does-git-push-do-exactly


However when you run `git push` you'll get an error.


``` 
git add key.txt 
The following paths are ignored by one of your .gitignore files:
key.txt
hint: Use -f if you really want to add them.
```


It looks like the `.gitignore` file is blocking us from adding the `key.txt` we need to push. 


A `.gitignore` file tells git which files not to track. 


https://stackoverflow.com/questions/27850222/what-is-gitignore


The `.gitignore` file currently doesn't track any txt files. 


```bash
cat .gitignore 
*.txt
```


I got rid of the `.gitignore `file 


```bash
rm .gitignore
```


Now we can git add `key.txt` without any problems.


```bash
git add key.txt 
```


Then you'll be able to `git commit` the file. 


```bash
git commit -m 'push key.txt to remote'
```


At last, `git push` to `origin master`. 


```bash
git push origin master
```


Although we failed to push `key.txt` it returns the password for the next level using ASCII text. 


```
git push origin master
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit31-git@bandit.labs.overthewire.org's password: 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 329 bytes | 329.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K 
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
To ssh://bandit.labs.overthewire.org:2220/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit.labs.overthewire.org:2220/home/bandit31-git/repo'
```