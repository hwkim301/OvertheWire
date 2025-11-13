## Level2 -> Level3 


It says there isn't anything on the page again. 


This time even when checking the page source there doesn't seem to be any meaningful hints.


There's a fishy `html` comment in the page source though. 


```html 
<!-- No more information leaks!! Not even Google will find it this time... -->
```


If it's your first time solving these problems. It will be pretty much impossible to solve it on your own without reading writeups.


I'll just give the answer right away. 


You need to enter **[robots.txt](https://en.wikipedia.org/wiki/Robots.txt)** at the end of the URL like this.


http://natas3.natas.labs.overthewire.org/robots.txt


Well, what exactly is `robots.txt`? 


`robots.txt` is a standard by used by websites to indicate web crawlers and web robots which parts of the website they are allowed to visit. 


It's a pretty tricky concept, but in short in determines which part of the website web crawlers are allowed to visit. 


**[Web crawlers](https://en.wikipedia.org/wiki/Web_crawler)** are used for indexing, which literally means the index of a book where we can find a certain content easily, in this case however it would be applied to websites. 


Anyways when visiting the [robots.txt](http://natas3.natas.labs.overthewire.org/robots.txt) you can see some text. 


```
User-agent: *
Disallow: /s3cr3t/
```


`robots.txt` didn't allow web crawlers to access the `/s3cr3t/` directory. 


Since `/s3cr3t/` is leet for secret, I'm 99% positive that the password's there. 


Let's change the directory to [/s3cr3t/](http://natas3.natas.labs.overthewire.org/s3cr3t/).


Inside the `/s3cr3t/` directory is a [users.txt](http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt) file. 


```
natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
```


After solving the challenge, I wonder what the `User-agent` means. 


I've read a couple of explanations on what `User-agent` is but it's still confusing to me. 