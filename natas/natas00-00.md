## Level0 

This is the first level of the natas wargames. 


When you enter the **[url](http://natas0.natas.labs.overthewire.org)** of the website in prompts you to enter the username and password.


After entering the username and password then it says you can find the password for the next level on this page. 


You'll have to inspect the page source of the website. 


There are multiple ways to do this.


1. Press Ctrl + u(Windows) or Command + Option + u(Mac)

This will show you the page source of the website. 


2. Add view-source in front on the url. 


```
view-source:http://natas0.natas.labs.overthewire.org/
```


3. Right click and click Inspect 


This will also show the source code of the website as well. 


You can find the comments in the `html` comments.


```html 
<!--The password for natas1 is 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq -->
```