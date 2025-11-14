## Level5 -> Level6


Now the web page as a submit button for secrets. 


It also has a link when clicking will show the source-code.


Here's the source code. 


```php
<?

include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
?>
```


The web page is written in **[PHP](https://en.wikipedia.org/wiki/PHP)**.


According to the source code, if we submit `$secret` it will print the password. 


Since the php code include `includes/secret.inc` it would be a good idea to check that file.


After changing the url to [includes/secret.inc](http://natas6.natas.labs.overthewire.org/includes/secret.inc).


It shows you the `$secret` value.  


```php 
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```


Copy the `$secret` value without the `""` and submit it as the secret. 


The web page changes and you'll get the password for the next level.


```html 
Access granted. The password for natas7 is bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
```


You can still solve the challenges without knowing PHP, but I recommend that you should study PHP before or after you solve the levels. 


If you read php books and study php you'll be able to answer questions below with ease. 


### 1. What is a .inc in php?


https://stackoverflow.com/questions/7129842/what-is-an-inc-and-why-use-it


### 2. Why does php use $ in variables? 


https://stackoverflow.com/questions/3073812/why-php-variables-start-with-a-sign-symbol


### 3. What is $_POST in php? 


https://stackoverflow.com/questions/1039797/what-is-the-purpose-of-post 


### 4. Why does php start with a <? 


https://www.reddit.com/r/PHP/comments/1mprxiw/why_should_a_php_file_always_start_with_that_ugly/ 


It will also improve your understanding on what the challenges are asking you to do. 


A lot of ctfers will Google stuff when they are stuck and they'll find a way to just pass the level.


Most of them learn php on the fly, but I think it's a terrible idea. 


Read php books or books explaining how HTTP works while you're solving these challenges.