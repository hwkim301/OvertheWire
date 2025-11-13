## Level29->Level30


```bash
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
```


This time, the `README` file doesn't contain the password.


```
cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```


Here's the result of `git log`, you can see that there is a previous commit. 


```
git log
commit b879c94bd4641ebb8b5470258b3a41debb25f7c2 (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Oct 14 09:26:20 2025 +0000

    fix username

commit 358fb1e671f460043ff5bd372e8d87e228dc148d
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Oct 14 09:26:20 2025 +0000

    initial commit of README.md
```

```
git checkout 358fb1e671f460043ff5bd372e8d87e228dc148d
Note: switching to '358fb1e671f460043ff5bd372e8d87e228dc148d'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 358fb1e initial commit of README.md
```


Sadly, checking out and going back to the previous commit and reading the `README` file doesn't show the password at all.


```
cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit29
- password: <no passwords in production!>
```


Now we'll have to use other git commands. 


This time we can use the `git branch` command.


For more information you should read [this](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell).


```
git branch -a
* (HEAD detached at 358fb1e)
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```


Then try checking out to other branches, as try reading the `README` file.


```bash 
git checkout remotes/origin/dev
```


```
cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```