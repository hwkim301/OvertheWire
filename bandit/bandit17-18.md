## Level17-> Level18


```bash 
ssh -p 2220 -i bandit16.key bandit17@bandit.labs.overthewire.org
```


This time the password is the only non-duplicate line between `passwords.old` and `passwords.new`.


The `diff` command shows the differences between files. 


```bash
diff passwords.old passwords.new
42c42
< BMIOFKM7CRSLI97voLp3TD80NAq5exxk
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```


Understanding diff's output is kind of hard.


According to [this post](https://unix.stackexchange.com/questions/81998/understanding-of-diff-output) the `< `denotes lines in the first file (passwords.old) and the `>` denotes lines in the second file (passwords.new).


The `42c42` means that the 42nd line in the first file changed to the 42nd line in the second file.


Using `-u` (unified) shows as if the two files were a single file. 


```bash
diff -u passwords.old passwords.new
--- passwords.old       2025-10-14 09:26:06.650645470 +0000
+++ passwords.new       2025-10-14 09:26:06.654505233 +0000
@@ -39,7 +39,7 @@
gLZVUZRqJJJUWLKbeP8Lokwq6CbFCyxG
boG62bCXn3U4gPugAPZMLQ9PtfdX9TMV
hnGGKfEtEGm7NwcHFmxZzubaJ5LrXbbR
-BMIOFKM7CRSLI97voLp3TD80NAq5exxk
+x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
87QCHMmaVMEz51K7aJvhbOqSR3OzdNKg
vuUCNxwqGpcAZtNaym57PCbxh3iWPmEv
lsUfIWgGXpNmnOuu7cR0PZXo2PJ6knhU
```


The line that starts with `-` is a different line that `passwords.old` has and the line that starts with a `+` is a line that only `passwords.new` has. 


So the password that's only in `passwords.new` is `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`.


Read the post below if you want to know the difference between `diff` and `git diff`.


https://unix.stackexchange.com/questions/356652/is-git-diff-related-to-diff