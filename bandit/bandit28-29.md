## Level28->Level29


You'll also get this error when deleting the repository of previous levels after git cloning. 


You get this prompt when you try to delete a file that is write-protected(read-only).


```bash 
rm -r repo/
override r--r--r-- hwkim301/staff for repo/.git/objects/pack/pack-0ff3d40def5e19d999887ad50b7aa6578b7bd2d6.pack?
```


If you don't want to see the prompt pop up you can use `rm -rf` which forces deletion.


Or you can give all the files in the  `/repo` directory write permission and then delete the files without forcing deletion.


```bash 
chmod -R u+w repo/
rm -r repo/ 
```


Another way would be entering `yes` after `rm -r` you can pipe it as well.


```bash 
yes | rm -r repo/
``` 


Lol I went down the rabbit hole again. 


```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
```


Here's the `README` file. 


```bash
cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```


The `README` file was the only file I could find in the `/repo` directory.


Git is a version control system in essence, we can go back in time to see how the files were modified in the past. 


The `git log` shows the logs of how the file has changed. 


```
git log
commit b0354c7be30f500854c5fc971c57e9cbe632fef6 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Tue Oct 14 09:26:19 2025 +0000

    fix info leak

commit d0cf2ab7dd7ebc6075b59102a980155268f0fe8f
Author: Morla Porla <morla@overthewire.org>
Date:   Tue Oct 14 09:26:19 2025 +0000

    add missing data

commit bd6bc3a57f81518bb2ce63f5816607a754ba730d
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Oct 14 09:26:18 2025 +0000
```


It looks like the previous commits contained the password. 


Someone probably updated the file so it wouldn't leak the password. 


Although, we can't see the password right now because the new commit patched the password, we can go back to previous commits using the `git checkout` command.


Since the second commit message is `add missing data` checking out to that commit will probably show us the password. 


```
git checkout d0cf2ab7dd7ebc6075b59102a980155268f0fe8f
Note: switching to 'd0cf2ab7dd7ebc6075b59102a980155268f0fe8f'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at d0cf2ab add missing data
```


Using the `cat` command reveals the password.


```
cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```
