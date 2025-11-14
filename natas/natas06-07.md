## Level6 -> Level7


Two links (`Home` and `About`) are given.


If you're a keen person you'll notice that the url changes when you clink on either of the links.


It will change like this. 


```
http://natas7.natas.labs.overthewire.org/


http://natas7.natas.labs.overthewire.org/index.php?page=home 


http://natas7.natas.labs.overthewire.org/index.php?page=about
```


You'll also notice that the `/index.php?page=link_name` was added at the end.


The value that starts right after the ? is called a **[query string](https://en.wikipedia.org/wiki/Query_string)**.


It's used to specify parameters in a url. 


Now let's check the source code to see if any hints exist.


There is a html comment like this. 


```html  
<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
```


The hint tells us that the password is in `/etc/natas_webpass/natas8`. 


Since `?page=home` shows the home page and vice versa for about, what would happend if we changed it to `/etc/natas_webpass/natas8`? 


Wouldn't that reveal the password? 


Let's give it a shot. 


```html 
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```


If you change the url you'll see the password.


```
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
```